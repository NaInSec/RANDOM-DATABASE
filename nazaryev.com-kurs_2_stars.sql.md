```bash

/*Левенштейн*/
CREATE OR REPLACE FUNCTION ld (
  as_src_i                         IN VARCHAR2
, as_trg_i                         IN VARCHAR2
)
RETURN NUMBER
DETERMINISTIC
AS
  ln_src_len                       PLS_INTEGER := NVL(LENGTH(as_src_i), 0);
  ln_trg_len                       PLS_INTEGER := NVL(LENGTH(as_trg_i), 0);
  ln_hlen                          PLS_INTEGER;
  ln_cost                          PLS_INTEGER;
  TYPE t_numtbl IS TABLE OF PLS_INTEGER INDEX BY BINARY_INTEGER;
  la_ldmatrix                         t_numtbl;

BEGIN
  IF (ln_src_len = 0)
  THEN
    RETURN ln_trg_len;
  ELSIF (ln_trg_len = 0)
  THEN
    RETURN ln_src_len;
  END IF;

  ln_hlen := ln_src_len + 1;
  FOR h IN 0 .. ln_src_len
  LOOP
    la_ldmatrix(h) := h;
  END LOOP;

  FOR v IN 0 .. ln_trg_len
  LOOP
    la_ldmatrix(v * ln_hlen) := v;
  END LOOP;

  FOR h IN 1 .. ln_src_len
  LOOP
    FOR v IN 1 .. ln_trg_len
    LOOP
      IF (SUBSTR(as_src_i, h, 1) = SUBSTR(as_trg_i, v, 1))
      THEN
        ln_cost := 0;
      ELSE
        ln_cost := 1;
      END IF;
      la_ldmatrix(v * ln_hlen + h) :=
         LEAST(
           la_ldmatrix((v - 1) * ln_hlen + h    ) + 1
         , la_ldmatrix( v      * ln_hlen + h - 1) + 1
         , la_ldmatrix((v - 1) * ln_hlen + h - 1) + ln_cost
         )
      ;
    END LOOP;
  END LOOP;
  RETURN la_ldmatrix(ln_trg_len * ln_hlen + ln_src_len);
END ld;
/

DECLARE
A NUMBER;
BEGIN
A:=ld('triim','troom');
DBMS_OUTPUT.ENABLE;
DBMS_OUTPUT.PUT_LINE(A);
END;
/

SELECT ld('Россия','Роисся') FROM DUAL;

/*Джаро-Винклер*/
CREATE OR REPLACE FUNCTION jws 
  (p_string1     IN VARCHAR2,
   p_string2     IN VARCHAR2)
  RETURN            NUMBER
  DETERMINISTIC
AS
  v_closeness       NUMBER := 0;
  v_temp            VARCHAR2 (32767);
  v_comp1           VARCHAR2 (32767);
  v_comp2           VARCHAR2 (32767);
  v_matches         NUMBER := 0; 
  v_char            VARCHAR2 (1);
  v_transpositions  NUMBER := 0;
  v_d_jaro          NUMBER := 0;
  v_leading         NUMBER := 0;
  v_d_winkler       NUMBER := 0;
  v_jws             NUMBER := 0;
BEGIN
  -- check for null strings:
  IF p_string1 IS NULL OR p_string2 IS NULL THEN 
    RETURN 0;
  END IF;
  -- closeness:
  v_closeness := (GREATEST (LENGTH (p_string1), LENGTH (p_string2)) / 2) - 1;
  -- find matching characters and transpositions within closeness:
  v_temp := p_string2;
  FOR i IN 1 .. LENGTH (p_string1) LOOP
    IF INSTR (v_temp, SUBSTR (p_string1, i, 1)) > 0 THEN
      v_char := SUBSTR (p_string1, i, 1);
      IF ABS (INSTR (p_string1, v_char) - INSTR (p_string2, v_char)) <= v_closeness THEN
        v_comp1 := v_comp1 || SUBSTR (p_string1, i, 1);
        v_temp := SUBSTR (v_temp, 1, INSTR (v_temp, SUBSTR (p_string1, i, 1)) - 1)
               || SUBSTR (v_temp, INSTR (v_temp, SUBSTR (p_string1, i, 1)) + 1);
      END IF;
    END IF;    
  END LOOP;
  v_temp := p_string1;
  FOR i IN 1 .. LENGTH (p_string2) LOOP
    IF INSTR (v_temp, SUBSTR (p_string2, i, 1)) > 0 THEN
      v_char := SUBSTR (p_string2, i, 1);
      IF ABS (INSTR (p_string2, v_char) - INSTR (p_string1, v_char)) <= v_closeness THEN
        v_comp2 := v_comp2 || SUBSTR (p_string2, i, 1);
        v_temp := SUBSTR (v_temp, 1, INSTR (v_temp, SUBSTR (p_string2, i, 1)) - 1)
               || SUBSTR (v_temp, INSTR (v_temp, SUBSTR (p_string2, i, 1)) + 1);
      END IF;
    END IF;    
  END LOOP;
  -- check for null strings:
  IF v_comp1 IS NULL OR v_comp2 IS NULL THEN 
    RETURN 0;
  END IF;
  -- count matches and transpositions within closeness:
  FOR i IN 1 .. LEAST (LENGTH (v_comp1), LENGTH (v_comp2)) LOOP
    IF SUBSTR (v_comp1, i, 1) = SUBSTR (v_comp2, i, 1) THEN
      v_matches := v_matches + 1;
    ELSE
      v_char := SUBSTR (v_comp1, i, 1);
      IF ABS (INSTR (p_string1, v_char) - INSTR (p_string2, v_char)) <= v_closeness THEN
        v_transpositions := v_transpositions + 1;
        v_matches := v_matches + 1;
      END IF; 
    END IF;
  END LOOP;
  v_transpositions := v_transpositions / 2;
  -- check for no matches:
  IF v_matches = 0
    THEN RETURN 0;
  END IF;
  -- Jaro:
  v_d_jaro := ((v_matches / LENGTH (p_string1)) + 
               (v_matches / LENGTH (p_string2)) +
               ((v_matches - v_transpositions) / v_matches)) 
               / 3;
  -- count matching leading characters (up to 4):
  FOR i IN 1 .. LEAST (LENGTH (p_string1), LENGTH (p_string2), 4) LOOP
    IF SUBSTR (p_string1, i, 1) = SUBSTR (p_string2, i, 1) THEN
      v_leading := v_leading + 1;
    ELSE
      EXIT;
    END IF;
  END LOOP;
  -- Winkler:
  v_d_winkler := v_d_jaro + ((v_leading * .1) * (1 - v_d_jaro));
  -- Jaro-Winkler similarity rounded:
  v_jws := ROUND (v_d_winkler * 100);
  RETURN v_jws;
END jws;
/

WITH strings AS
(SELECT NULL       string1, NULL     string2 FROM DUAL UNION ALL
SELECT 'test'       string1, NULL     string2 FROM DUAL UNION ALL
SELECT NULL       string1, 'test'     string2 FROM DUAL UNION ALL
SELECT 'CRATE'      string1, 'TRACE'      string2 FROM DUAL UNION ALL
SELECT 'MARTHA'     string1, 'MARHTA'     string2 FROM DUAL UNION ALL
SELECT 'DWAYNE'     string1, 'DUANE'      string2 FROM DUAL UNION ALL
SELECT 'DIXON'      string1, 'DICKSONX'   string2 FROM DUAL UNION ALL
SELECT 'Dunningham' string1, 'Cunningham' string2 FROM DUAL UNION ALL
SELECT 'Abroms'     string1, 'Abrams'     string2 FROM DUAL UNION ALL
SELECT 'Lampley'    string1, 'Campley'    string2 FROM DUAL UNION ALL
SELECT 'Jonathon'   string1, 'Jonathan'   string2 FROM DUAL UNION ALL
SELECT 'Jeraldine'  string1, 'Gerladine'  string2 FROM DUAL UNION ALL
SELECT 'test'       string1, 'blank'      string2 FROM DUAL UNION ALL
SELECT 'everybody'  string1, 'every'      string2 FROM DUAL UNION ALL
SELECT 'a'        string1, 'aaa'        string2 FROM DUAL)
SELECT string1, string2,
    UTL_MATCH.JARO_WINKLER_SIMILARITY (string1, string2) oracle_jws,
      jws (string1, string2) my_jws
  FROM   strings
  ORDER  BY my_jws DESC
/


SELECT jws ('Барак Абама','Парап Апама') FROM DUAL;

-- Hamming Distance
CREATE OR REPLACE FUNCTION hd (
  as_src_i                         IN VARCHAR2
, as_trg_i                         IN VARCHAR2
)
RETURN NUMBER
DETERMINISTIC
AS
  ln_src_len                       PLS_INTEGER := NVL(LENGTH(as_src_i), 0);
  ln_trg_len                       PLS_INTEGER := NVL(LENGTH(as_trg_i), 0);
  ln_distance                      PLS_INTEGER := 0;
BEGIN
  IF (ln_src_len <> ln_trg_len)
  THEN
    RETURN NULL;
  END IF;

  IF (ln_src_len = 0)
  THEN
    RETURN ln_src_len;
  END IF;

  FOR i IN 1..ln_src_len
  LOOP
    IF (SUBSTR(as_src_i, i, 1) <> SUBSTR(as_trg_i, i, 1))
    THEN
      ln_distance := ln_distance + 1;
    END IF;
  END LOOP;
  RETURN ln_distance;
END hd;
/

DECLARE
A NUMBER;
BEGIN
A:=hd('triim','troom');
DBMS_OUTPUT.ENABLE;
DBMS_OUTPUT.PUT_LINE(A);
END;
/

SELECT hd('Россия','Роисся') FROM DUAL;

-- ЗАПРОС **
SELECT * FROM(
    WITH COUNTRY_NAMES AS
    (SELECT NAME FROM CITIZENSHIP)
    SELECT COUNTRY_NAMES.NAME, jws(COUNTRY_NAMES.NAME,'Rassiya') mjws
    FROM COUNTRY_NAMES
    ORDER BY mjws DESC
)
WHERE ROWNUM = 1;

SELECT SUR, EN_PR, CIT FROM
  (
  SELECT SUR, EN_PR, C.NAME CIT
  FROM CITIZENSHIP C
  JOIN
    (
    SELECT H.SURNAME SUR, EN_PR, H.CITIZENSHIP_ID CIT_ID
    FROM HUMANS H
    JOIN
    (
      SELECT HUMAN_ID H_ID, EN_PR FROM
      ENTRANTS E JOIN
        (
        SELECT P.ENTRANT_ID ENT_ID, LISTAGG(P.PROGRAM_ID,', ')
        WITHIN GROUP (ORDER BY P.ENTRANT_ID) AS EN_PR
        FROM PRIORITIES P 
        GROUP BY P.ENTRANT_ID
        )
        ON E.ID = ENT_ID
    )
    ON H.ID = H_ID
    )
  ON C.ID = CIT_ID
  )
WHERE CIT IN 
(
  SELECT NAME FROM(
    WITH COUNTRY_NAMES AS
    (SELECT NAME FROM CITIZENSHIP)
    SELECT COUNTRY_NAMES.NAME, jws(COUNTRY_NAMES.NAME,'Rassiya') mjws
    FROM COUNTRY_NAMES
    ORDER BY mjws DESC
)
WHERE ROWNUM = 1
);
```
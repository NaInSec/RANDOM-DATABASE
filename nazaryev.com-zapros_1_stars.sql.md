```bash

COLUMN EN_PR FORMAT A20;
COLUMN SURNAME FORMAT A10;
COLUMN NAME FORMAT A10;
COLUMN SUR FORMAT A10;
COLUMN CIT FORMAT A10;

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
WHERE CIT LIKE INITCAP(F_TRANSLATE('Hjcc%')); --'Росс%'

CREATE OR REPLACE FUNCTION F_TRANSLATE(WORD IN VARCHAR2) 
RETURN VARCHAR2
IS
	S VARCHAR2(20);
BEGIN
S:=UPPER(WORD);
S:=REPLACE(S,'F', 'А');
S:=REPLACE(S,',', 'Б');
S:=REPLACE(S,'D', 'В');
S:=REPLACE(S,'U', 'Г');
S:=REPLACE(S,'L', 'Д');
S:=REPLACE(S,'T', 'Е');
S:=REPLACE(S,'`', 'Ё');
S:=REPLACE(S,';', 'Ж');
S:=REPLACE(S,'P', 'З');
S:=REPLACE(S,'B', 'И');
S:=REPLACE(S,'Q', 'Й');
S:=REPLACE(S,'R', 'К');
S:=REPLACE(S,'K', 'Л');
S:=REPLACE(S,'V', 'М');
S:=REPLACE(S,'Y', 'Н');
S:=REPLACE(S,'J', 'О');
S:=REPLACE(S,'G', 'П');
S:=REPLACE(S,'H', 'Р');
S:=REPLACE(S,'C', 'С');
S:=REPLACE(S,'N', 'Т');
S:=REPLACE(S,'E', 'У');
S:=REPLACE(S,'A', 'Ф');
S:=REPLACE(S,'[', 'Х');
S:=REPLACE(S,'W', 'Ц');
S:=REPLACE(S,'X', 'Ч');
S:=REPLACE(S,'I', 'Ш');
S:=REPLACE(S,']', 'Ъ');
S:=REPLACE(S,'S', 'Ы');
S:=REPLACE(S,'M', 'Ь');
S:=REPLACE(S,'''', 'Э');
S:=REPLACE(S,'.', 'Ю');
S:=REPLACE(S,'Z', 'Я');
	RETURN S;
END;
/


DECLARE
BEGIN
  FOR r1 IN ( SELECT 'DROP ' || object_type || ' ' || object_name || DECODE ( object_type, 'TABLE', ' CASCADE CONSTRAINTS PURGE' ) AS v_sql
                FROM user_objects
               WHERE object_type IN ( 'TABLE', 'VIEW', 'PACKAGE', 'TYPE', 'PROCEDURE', 'FUNCTION', 'TRIGGER', 'SEQUENCE' )
               ORDER BY object_type,
                        object_name ) LOOP
    EXECUTE IMMEDIATE r1.v_sql;
  END LOOP;
END;
/

```
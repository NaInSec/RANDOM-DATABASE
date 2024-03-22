```bash

SELECT t.*,TO_CHAR(ДАТА, 'dd-mm-yyyy hh24:mi:ss') ДАТА,TO_CHAR(ВРЕМЯ, 'dd-mm-yyyy hh24:mi:ss') ВРЕМЯ,TO_CHAR(ДАТА_К, 'dd-mm-yyyy hh24:mi:ss') ДАТА_К,TO_CHAR(ВРЕМЯ_К, 'dd-mm-yyyy hh24:mi:ss') ВРЕМЯ_К 
FROM Н_СЕССИЯ t;
---------------
111111111111111111111111111111111111111111111111111

SELECT DISTINCT НАИМЕНОВАНИЕ 
FROM Н_ДИСЦИПЛИНЫ;   
+++++

222222222222222222222222222222222222222222222222222

SELECT ROUND(TO_DATE('2014/09/01', 'yyyy/mm/dd') - ДАТА_РОЖДЕНИЯ) 
FROM Н_ЛЮДИ 
WHERE ИД = (SELECT MAX(ИД) FROM Н_ЛЮДИ); 

посчитать в месяцах
SELECT ROUND(MONTHS_BETWEEN(TO_DATE('2014/09/01', 'yyyy/mm/dd'), ДАТА_РОЖДЕНИЯ)) 
FROM Н_ЛЮДИ 
WHERE ИД = (SELECT MAX(ИД) FROM Н_ЛЮДИ);

3333333333333333333333333333333333333333333333333333

SELECT ФАМИЛИЯ || ' ' || SUBSTR(ИМЯ,1,1) || '.' || SUBSTR(ОТЧЕСТВО,1,1) || '.' ЧЕЛОВЕК 
FROM Н_ЛЮДИ 
WHERE TO_CHAR(ДАТА_РОЖДЕНИЯ,'month') = 
	(SELECT TO_CHAR(ДАТА_РОЖДЕНИЯ,'month') 
	FROM Н_ЛЮДИ
	WHERE ИД = (SELECT MAX(ИД) FROM Н_ЛЮДИ));  
+++++
4444444444444444444444444444444444444444444444444444

SELECT ФАМИЛИЯ, ИМЯ, ОТЧЕСТВО, ИД 
FROM Н_ЛЮДИ 
WHERE ФАМИЛИЯ LIKE(
	SELECT SUBSTR((ФАМИЛИЯ),1,2) || '%' 
	FROM Н_ЛЮДИ WHERE ИД=(SELECT MAX(ИД) FROM Н_ЛЮДИ)) 
AND ROWNUM <= 75 
ORDER BY ФАМИЛИЯ DESC,ИМЯ DESC, ОТЧЕСТВО DESC;  
++++
5555555555555555555555555555555555555555555555555555
===========================
SELECT ФАМИЛИЯ, ИМЯ, ОТЧЕСТВО, ИД 
FROM Н_ЛЮДИ 
WHERE SUBSTR(ФАМИЛИЯ,1,1) NOT IN ('А','Б','З') AND SUBSTR(ИМЯ,1,1) NOT IN ('К','У'); 
+++

SELECT ФАМИЛИЯ, ИМЯ, ОТЧЕСТВО, ИД 
FROM Н_ЛЮДИ 
WHERE SUBSTR(ФАМИЛИЯ,1,1) <> 'А' AND SUBSTR(ФАМИЛИЯ,1,1) <> 'Б' AND SUBSTR(ФАМИЛИЯ,1,1) <> 'З' AND SUBSTR(ИМЯ,1,1) <> 'К' AND SUBSTR(ИМЯ,1,1) <> 'У'; 
+++
66666666666666666666666666666666666666666666666666666
===========================

SELECT COUNT(DISTINCT ИД)
FROM Н_ЛЮДИ
WHERE ИМЯ = (
	SELECT ИМЯ FROM Н_ЛЮДИ
	WHERE ИД = (
		SELECT min(ИД) 
		FROM Н_ЛЮДИ));
------
77777777777777777777777777777777777777777777777777777
===========================
SELECT ОЦЕНКА*2 
FROM Н_ВЕДОМОСТИ 
WHERE ЧЛВК_ИД = (
		SELECT MAX(ЧЛВК_ИД) 
		FROM Н_ВЕДОМОСТИ) 
AND REGEXP_LIKE(ОЦЕНКА, '^[0-9]+$') AND ОЦЕНКА NOT IN ('99');

WITH t AS (SELECT '99' str FROM dual)
SELECT str
FROM t
WHERE REGEXP_LIKE(str, '^[0-9]+$');
А5-----
88888888888888888888888888888888888888888888888888888
===========================
SELECT SUM(ОЦЕНКА), Н_ЛЮДИ.ФАМИЛИЯ 
FROM Н_ВЕДОМОСТИ 
JOIN Н_ЛЮДИ ON Н_ВЕДОМОСТИ.ЧЛВК_ИД=Н_ЛЮДИ.ИД 
WHERE ЧЛВК_ИД IN (
	SELECT ИД FROM Н_ЛЮДИ 
	WHERE ИД>(SELECT AVG(ИД) FROM Н_ЛЮДИ) AND ROWNUM <=7) 
AND REGEXP_LIKE(ОЦЕНКА, '^[0-9]+$') AND ОЦЕНКА NOT IN ('99') 
GROUP BY Н_ЛЮДИ.ИД, Н_ЛЮДИ.ФАМИЛИЯ;
А5---- уникальный человек
99999999999999999999999999999999999999999999999999999
============================
SELECT * FROM Н_ОЦЕНКИ, Н_ТИПЫ_ВЕДОМОСТЕЙ, Н_ВИДЫ_РАБОТ, Н_СВОЙСТВА_ВР;
++++++
10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 
============================
SELECT AVG(ОЦЕНКА), ФАМИЛИЯ, ИМЯ, ОТЧЕСТВО 
FROM Н_ВЕДОМОСТИ 
JOIN Н_ЛЮДИ ON Н_ВЕДОМОСТИ.ЧЛВК_ИД=Н_ЛЮДИ.ИД 
WHERE ЧЛВК_ИД IN (
	SELECT ИД FROM Н_ЛЮДИ 
	WHERE ИД>(SELECT AVG(ИД) FROM Н_ЛЮДИ) AND ROWNUM <=7) 
AND REGEXP_LIKE(ОЦЕНКА, '^[0-9]+$') AND ОЦЕНКА NOT IN ('99') 
GROUP BY ЧЛВК_ИД, ФАМИЛИЯ, ИМЯ, ОТЧЕСТВО;
++++
11 11 11 11 11 11 11 11 11 11 11 11 11 11 11 11 11 11
===========================
SELECT ФАМИЛИЯ, ИМЯ, ОТЧЕСТВО 
FROM Н_ЛЮДИ 
WHERE ИД IN (
	SELECT ЧЛВК_ИД 
	FROM Н_ВЕДОМОСТИ 
	WHERE ОЦЕНКА IN('3','4') AND ДАТА BETWEEN TO_DATE('2011/09/01', 'yyyy/mm/dd') AND TO_DATE('2014/07/20', 'yyyy/mm/dd') 
	GROUP BY ЧЛВК_ИД) 
ORDER BY ФАМИЛИЯ, ИМЯ, ОТЧЕСТВО;
++++
13 13 13 13 13 13 13 13 13 13 13 13 13 13 13 13 13 13 
===========================
WITH t AS (SELECT   (SELECT ИД FROM Н_ЛЮДИ WHERE ФАМИЛИЯ = 'Бусыгин') a FROM DUAL) SELECT 9 * REGEXP_COUNT(a,'9') + 8 * REGEXP_COUNT(a,'8') + 7 * REGEXP_COUNT(a,'7') + 6 * REGEXP_COUNT(a,'6') + 5 * REGEXP_COUNT(a,'5') + 4 * REGEXP_COUNT(a,'4') + 3 * REGEXP_COUNT(a,'3') + 2 * REGEXP_COUNT(a,'2') + 1 * REGEXP_COUNT(a,'1') FROM   t;

SELECT ФАМИЛИЯ, COUNT(ФАМИЛИЯ) OVER (PARTITION BY ФАМИЛИЯ) A, ИМЯ, COUNT(ИМЯ) OVER (PARTITION BY ИМЯ) B, ОТЧЕСТВО, COUNT(ОТЧЕСТВО) OVER (PARTITION BY ОТЧЕСТВО) C FROM Н_ЛЮДИ order by A,B,C;

SELECT MAX(a) FROM (SELECT ФАМИЛИЯ, COUNT(ФАМИЛИЯ) a, ИМЯ, COUNT(ИМЯ), ОТЧЕСТВО, COUNT(ОТЧЕСТВО) FROM Н_ЛЮДИ group by ФАМИЛИЯ, ИМЯ, ОТЧЕСТВО order by COUNT(ФАМИЛИЯ));

WITH T AS (SELECT ФАМИЛИЯ, COUNT(ФАМИЛИЯ) a, ИМЯ, COUNT(ИМЯ), ОТЧЕСТВО, COUNT(ОТЧЕСТВО) FROM Н_ЛЮДИ group by ФАМИЛИЯ, ИМЯ, ОТЧЕСТВО order by COUNT(ФАМИЛИЯ)) SELECT ФАМИЛИЯ, MAX(a) FROM T;



SELECT sum_ball, М_ИД, ФАМИЛИЯ, ИМЯ, ОТЧЕСТВО 
FROM (
	SELECT DISTINCT Н_ВЕДОМОСТИ.ЧЛВК_ИД М_ИД, SUM(ОЦЕНКА) OVER (PARTITION BY ЧЛВК_ИД) sum_ball 
	FROM Н_ВЕДОМОСТИ 
	WHERE ЧЛВК_ИД IN(
	SELECT ИД FROM Н_ЛЮДИ WHERE ФАМИЛИЯ || ИМЯ || ОТЧЕСТВО IN (
		SELECT ФАМИЛИЯ || ИМЯ || ОТЧЕСТВО 
		FROM(
			SELECT ФАМИЛИЯ, ИМЯ, ОТЧЕСТВО, COUNT(*) a 
			FROM Н_ЛЮДИ 
			GROUP BY ФАМИЛИЯ, ИМЯ, ОТЧЕСТВО) 
		WHERE a=(
			SELECT MAX(a) 
			FROM (
				SELECT ФАМИЛИЯ, COUNT(ФАМИЛИЯ) a, ИМЯ, COUNT(ИМЯ), ОТЧЕСТВО, COUNT(ОТЧЕСТВО) 
				FROM Н_ЛЮДИ 
				group by ФАМИЛИЯ, ИМЯ, ОТЧЕСТВО order by COUNT(ФАМИЛИЯ))))) 
	AND REGEXP_LIKE(ОЦЕНКА, '[[:digit:]]') AND ОЦЕНКА NOT IN ('99')) 
JOIN Н_ЛЮДИ ON М_ИД=Н_ЛЮДИ.ИД  
WHERE sum_ball < (
	WITH t AS (SELECT (SELECT MAX(ИД) FROM Н_ЛЮДИ) a FROM DUAL) 
	SELECT 9 * REGEXP_COUNT(a,'9') + 8 * REGEXP_COUNT(a,'8') + 7 * REGEXP_COUNT(a,'7') + 6 * REGEXP_COUNT(a,'6') + 5 * REGEXP_COUNT(a,'5') + 4 * REGEXP_COUNT(a,'4') + 3 * REGEXP_COUNT(a,'3') + 2 * REGEXP_COUNT(a,'2') + 1 * REGEXP_COUNT(a,'1') 
	FROM   t);

14 14 14 14 14 14 14 14 14 14 14 14 14 14 14 14 14 14 14 14 14 14 14 14 
===========================
SELECT 'Оценки 4 и 5 во всем университете', TO_CHAR(ROUND(AVG(ОЦЕНКА),2)) Средняя_оценка, TO_CHAR(COUNT(ОЦЕНКА)) Количество_оценок 
FROM Н_ВЕДОМОСТИ 
WHERE ОЦЕНКА IN('4','5') 
UNION 
SELECT 'Оценки ''зачет'' в произвольном учебном году во всем университете','-' Средняя_оценка, TO_CHAR(COUNT(ОЦЕНКА)) Количество_оценок 
FROM Н_ВЕДОМОСТИ 
WHERE ДАТА BETWEEN TO_DATE('2011/09/01', 'yyyy/mm/dd') AND TO_DATE('2014/07/20', 'yyyy/mm/dd') AND ОЦЕНКА IN ('зачет')
UNION all
SELECT 'Расстояние Левенштейна',TO_CHAR(utl_match.edit_distance('Припадчев', ФАМИЛИЯ)) Средняя_оценка, '-' Количество_оценок
FROM (SELECT ФАМИЛИЯ
FROM Н_ЛЮДИ 
WHERE ИД IN (
	SELECT ЧЛВК_ИД FROM Н_ВЕДОМОСТИ WHERE ОЦЕНКА='3'
	UNION
	SELECT ЧЛВК_ИД FROM Н_ВЕДОМОСТИ WHERE ОЦЕНКА='4'
	UNION
	SELECT ЧЛВК_ИД FROM Н_ВЕДОМОСТИ WHERE ОЦЕНКА='5')
AND ROWNUM <=10);

12 12 12 12 12 12 12 12 12 12 12 12 12 12 12 12 12 12 12 12 12 12 12 12 

 SUM(ОЦЕНКА) OVER (PARTITION BY ЧЛВК_ИД) sum_ball

SELECT  EXTRACT(YEAR FROM (b - a) YEAR TO MONTH )
   || ' years '
   || EXTRACT(MONTH FROM (b - a) YEAR TO MONTH )
   || ' months '
   || EXTRACT(DAY FROM (b - a) DAY TO SECOND ) 
   || ' days '
   || EXTRACT(HOUR FROM (b - a) DAY TO SECOND )
   || ' hours'
    "INTERVAL" 
FROM (
SELECT TO_DATE('01-02-2005','dd-mm-YYYY') a ,  TO_DATE('02-01-2010','dd-mm-YYYY') b FROM dual)
;

http://stackoverflow.com/questions/3006431/how-to-display-table-data-more-clearly-in-oracle-sqlplus
```acle-sqlplus
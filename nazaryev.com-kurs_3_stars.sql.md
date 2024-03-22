```bash

SELECT XMLElement("COUNTRY", 
                   XMLElement("NAME", NAME),
                   XMLElement("ID", ID)) AS "RESULT" 
FROM CITIZENSHIP;


SELECT XMLElement("COUNTRY", 
                  XMLForest(ID, NAME)) AS "RESULT"
FROM CITIZENSHIP;

SELECT XMLElement("BRANCH", 
                  XMLForest(ID, NAME)) AS "RESULT"
FROM BRANCHES;

<COUNTRY><ID>3</ID><NAME>Kazakhstan</NAME></COUNTRY>
<COUNTRY><ID>1</ID><NAME>Russia</NAME></COUNTRY>
<COUNTRY><ID>2</ID><NAME>Ukraine</NAME></COUNTRY>

<BRANCH><ID>1</ID><NAME>Dnevnoe</NAME></BRANCH>
<BRANCH><ID>2</ID><NAME>Vechernee</NAME></BRANCH>
<BRANCH><ID>3</ID><NAME>Zaochnoe</NAME></BRANCH>


SELECT
  XMLConcat
  (
  	(
  		SELECT XMLAgg(XMLElement("CITIZENSHIP",
  			(
  				SELECT XMLAgg(XMLElement("COUNTRY", XMLForest(ID,NAME))) FROM CITIZENSHIP)
  			)
  		)from dual
  	),
  	(
  		SELECT XMLAgg(XMLElement("DUAL1", XMLForest(DUMMY))) FROM dual
  	)
  ) AS "RESULT"
FROM 
  dual;  


SET pagesize 50000;
SET long 50000;

SELECT
  XMLConcat(
    XMLElement("CITIZENSHIP", (SELECT XMLAgg(XMLElement("COUNTRY", XMLForest(ID,NAME))) FROM CITIZENSHIP)),
    XMLElement("BRANCHES", (SELECT XMLAgg(XMLElement("BRANCH", XMLForest(ID,NAME))) FROM CITIZENSHIP)),
    XMLElement("SUBJECTS", (SELECT XMLAgg(XMLElement("SUBJECT", XMLForest(ID,NAME))) FROM SUBJECTS)),
    XMLElement("SPECIALTIES", (SELECT XMLAgg(XMLElement("SPECIALTY", XMLForest(ID,NAME,CODE))) FROM SPECIALTIES)),
    XMLElement("DEPARTMENT_TYPES", (SELECT XMLAgg(XMLElement("DEPARTMENT_TYPE", XMLForest(ID,NAME))) FROM DEPARTMENT_TYPES)),
    XMLElement("PROGRAMSUBJECTS", (SELECT XMLAgg(XMLElement("PROGRAMSUBJECT", XMLForest(ID,PROGRAM_ID,SUBJECT_ID,THRESHOLD_MARK,PS_YEAR))) FROM PROGRAMSUBJECTS)),
    XMLElement("EXAMS", (SELECT XMLAgg(XMLElement("EXAM", XMLForest(ID,ENTRANT_ID,SUBJECT_ID,MARK,CODE))) FROM EXAMS WHERE ROWNUM <= 10)),
    XMLElement("ORDERS_ITEMS", (SELECT XMLAgg(XMLElement("ORDER_ITEM", XMLForest(ID,NAME,ITEM_NUMBER))) FROM ORDERS_ITEMS)),
    XMLElement("DEPARTMENTS", (SELECT XMLAgg(XMLElement("DEPARTMENT", XMLForest(ID,NAME,ABBR,DEPARTMENT_ID,DEPARTMENT_TYPE_ID,CODE))) FROM DEPARTMENTS)),
    XMLElement("PROGRAMS", (SELECT XMLAgg(XMLElement("PROGRAM", XMLForest(ID,SPEC_ID,BRANCH_ID))) FROM PROGRAMS)),
    XMLElement("DEPARTMENTPROGRAM", (SELECT XMLAgg(XMLElement("DEPPROG", XMLForest(ID,PROGRAM_ID,DEPARTMENT_ID))) FROM DEPARTMENTPROGRAM)),
    XMLElement("COMMANDMENTS", (SELECT XMLAgg(XMLElement("COMMANDMENT", XMLForest(ID,ENTRANT_ID,PROGRAM_ID,ORDER_ID,PRE_COMMANDMENT,COMMANDMENT_YEAR,CODE,DEPARTMENT_ID,COMMIT_DATE,CREATE_DATE))) FROM COMMANDMENTS)),
    XMLElement("PRIORITIES", (SELECT XMLAgg(XMLElement("PRIORITY", XMLForest(ID,ENTRANT_ID,PROGRAM_ID,PRIORITY))) FROM PRIORITIES WHERE ROWNUM <= 10)),
    XMLElement("ACCEPTANCE_PLANS", (SELECT XMLAgg(XMLElement("ACCEPTANCE_PLAN", XMLForest(ID,PROGRAM_ID,AMOUNT,PLAN_YEAR,DEPARTMENT_ID))) FROM ACCEPTANCE_PLANS)),
    XMLElement("ENTRANTS", (SELECT XMLAgg(XMLElement("ENTRANT", XMLForest(ID,HUMAN_ID,ORIGINAL,MEDAL,ALLOWANCE,ENTRY_YEAR))) FROM ENTRANTS WHERE ROWNUM <= 10)),
    XMLElement("HUMANS", (SELECT XMLAgg(XMLElement("HUMAN", XMLForest(ID,NAME,SURNAME,SECOND_NAME,BIRTH_DATE,SEX,CITIZENSHIP_ID))) FROM HUMANS WHERE ROWNUM <= 10))
  )
FROM 
  dual;









CREATE OR REPLACE PACKAGE ALLDATA IS
  TYPE rowGetSubjects IS RECORD(
    l_id SUBJECTS.ID%TYPE,
    l_name SUBJECTS.NAME%TYPE
  );

  TYPE rowGetSpecialties IS RECORD(
    l_id SPECIALTIES.ID%TYPE,
    l_name SPECIALTIES.NAME%TYPE,
    l_code SPECIALTIES.CODE%TYPE
  );

  TYPE rowGetDepartmentTypes IS RECORD(
    l_id DEPARTMENT_TYPES.ID%TYPE,
    l_name DEPARTMENT_TYPES.NAME%TYPE
  );

  TYPE rowGetProgramSubjects IS RECORD(
    l_id PROGRAMSUBJECTS.ID%TYPE,
    l_program_id PROGRAMSUBJECTS.PROGRAM_ID%TYPE,
    l_subject_id PROGRAMSUBJECTS.SUBJECT_ID%TYPE,
    l_threshold_mark PROGRAMSUBJECTS.THRESHOLD_MARK%TYPE,
    l_ps_year PROGRAMSUBJECTS.PS_YEAR%TYPE
  );

  TYPE rowGetExams IS RECORD(
    l_id EXAMS.ID%TYPE,
    l_entrant_id EXAMS.ENTRANT_ID%TYPE,
    l_subject_id EXAMS.SUBJECT_ID%TYPE,
    l_mark EXAMS.MARK%TYPE,
    l_code EXAMS.CODE%TYPE
  );

  TYPE rowGetOrderItems IS RECORD(
    l_id ORDERS_ITEMS.ID%TYPE,
    l_name ORDERS_ITEMS.NAME%TYPE,
    l_full_text ORDERS_ITEMS.FULL_TEXT%TYPE,
    l_item_number ORDERS_ITEMS.ITEM_NUMBER%TYPE
  );

  TYPE rowGetDepartments IS RECORD(
    l_id DEPARTMENTS.ID%TYPE,
    l_name DEPARTMENTS.NAME%TYPE,
    l_department_id DEPARTMENTS.DEPARTMENT_ID%TYPE,
    l_department_type_id DEPARTMENTS.DEPARTMENT_TYPE_ID%TYPE,
    l_code DEPARTMENTS.CODE%TYPE,
    l_abbr DEPARTMENTS.ABBR%TYPE
  );

  TYPE rowGetDepartmentProgram IS RECORD(
    l_id DEPARTMENTPROGRAM.ID%TYPE,
    l_program_id DEPARTMENTPROGRAM.PROGRAM_ID%TYPE,
    l_department_id DEPARTMENTPROGRAM.DEPARTMENT_ID%TYPE
  );

  TYPE rowGetBranches IS RECORD(
    l_id BRANCHES.ID%TYPE,
    l_name BRANCHES.NAME%TYPE
  );

  TYPE rowGetPrograms IS RECORD(
    l_id PROGRAMS.ID%TYPE,
    l_spec_id PROGRAMS.SPEC_ID%TYPE,
    l_branch_id PROGRAMS.BRANCH_ID%TYPE
  );

  TYPE rowGetAcceptancePlans IS RECORD(
    l_id ACCEPTANCE_PLANS.ID%TYPE,
    l_program_id ACCEPTANCE_PLANS.PROGRAM_ID%TYPE,
    l_amount ACCEPTANCE_PLANS.AMOUNT%TYPE,
    l_plan_year ACCEPTANCE_PLANS.PLAN_YEAR%TYPE,
    l_department_id ACCEPTANCE_PLANS.DEPARTMENT_ID%TYPE
  );

  TYPE rowGetPriorities IS RECORD(
    l_id PRIORITIES.ID%TYPE,
    l_entrant_id PRIORITIES.ENTRANT_ID%TYPE,
    l_program_id PRIORITIES.PROGRAM_ID%TYPE,
    l_priority PRIORITIES.PRIORITY%TYPE
  );

  TYPE rowGetCommandments IS RECORD(
    l_id COMMANDMENTS.ID%TYPE,
    l_entrant_id COMMANDMENTS.ENTRANT_ID%TYPE,
    l_program_id COMMANDMENTS.PROGRAM_ID%TYPE,
    l_order_id COMMANDMENTS.ORDER_ID%TYPE,
    l_pre_commandment COMMANDMENTS.PRE_COMMANDMENT%TYPE,
    l_commandment_year COMMANDMENTS.COMMANDMENT_YEAR%TYPE,
    l_code COMMANDMENTS.CODE%TYPE,
    l_department_id COMMANDMENTS.DEPARTMENT_ID%TYPE,
    l_commit_date COMMANDMENTS.COMMIT_DATE%TYPE,
    l_create_date COMMANDMENTS.CREATE_DATE%TYPE
  );

  TYPE rowGetEntrants IS RECORD(
    l_id ENTRANTS.ID%TYPE,
    l_human_id ENTRANTS.HUMAN_ID%TYPE,
    l_original ENTRANTS.ORIGINAL%TYPE,
    l_medal ENTRANTS.MEDAL%TYPE,
    l_allowance ENTRANTS.ALLOWANCE%TYPE,
    l_entry_year ENTRANTS.ENTRY_YEAR%TYPE,
    l_scanned_profile ENTRANTS.SCANNED_PROFILE%TYPE
  );

  TYPE rowGetHumans IS RECORD(
    l_id HUMANS.ID%TYPE,
    l_name HUMANS.NAME%TYPE,
    l_surname HUMANS.SURNAME%TYPE,
    l_second_name HUMANS.SECOND_NAME%TYPE,
    l_birth_date HUMANS.BIRTH_DATE%TYPE,
    l_sex HUMANS.SEX%TYPE,
    l_citizenship_id HUMANS.CITIZENSHIP_ID%TYPE
  );

  TYPE tblGetSubjects IS TABLE OF rowGetSubjects;
  TYPE tblGetSpecialties IS TABLE OF rowGetSpecialties;
  TYPE tblGetDepartmentTypes IS TABLE OF rowGetDepartmentTypes;
  TYPE tblGetProgramSubjects IS TABLE OF rowGetProgramSubjects;
  TYPE tblGetExams IS TABLE OF rowGetExams;
  TYPE tblGetOrderItems IS TABLE OF rowGetOrderItems;
  TYPE tblGetDepartments IS TABLE OF rowGetDepartments;
  TYPE tblGetDepartmentProgram IS TABLE OF rowGetDepartmentProgram;
  TYPE tblGetBranches IS TABLE OF rowGetBranches;
  TYPE tblGetPrograms IS TABLE OF rowGetPrograms;
  TYPE tblGetAcceptancePlans IS TABLE OF rowGetAcceptancePlans;
  TYPE tblGetPriorities IS TABLE OF rowGetPriorities;
  TYPE tblGetCommandments IS TABLE OF rowGetCommandments;
  TYPE tblGetEntrants IS TABLE OF rowGetEntrants;
  TYPE tblGetHumans IS TABLE OF rowGetHumans;

  FUNCTION GetSubjects
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetSubjects
  PIPELINED;

  FUNCTION GetSpecialties
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetSpecialties
  PIPELINED;

  FUNCTION GetDepartmentTypes
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetDepartmentTypes
  PIPELINED;

  FUNCTION GetProgramSubjects
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetProgramSubjects
  PIPELINED;  

  FUNCTION GetExams
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetExams
  PIPELINED;

  FUNCTION GetOrderItems
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetOrderItems
  PIPELINED;

  FUNCTION GetDepartments
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetDepartments
  PIPELINED;  

  FUNCTION GetDepartmentProgram
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetDepartmentProgram
  PIPELINED;

  FUNCTION GetBranches
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetBranches
  PIPELINED;

  FUNCTION GetPrograms
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetPrograms
  PIPELINED;

  FUNCTION GetAcceptancePlans
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetAcceptancePlans
  PIPELINED;

  FUNCTION GetPriorities
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetPriorities
  PIPELINED;

  FUNCTION GetCommandments
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetCommandments
  PIPELINED;

  FUNCTION GetEntrants
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetEntrants
  PIPELINED;

  FUNCTION GetHumans
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetHumans
  PIPELINED;

END ALLDATA;
/

CREATE OR REPLACE PACKAGE BODY ALLDATA IS
  FUNCTION GetSubjects
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetSubjects
  PIPELINED
  IS
  BEGIN
    IF pCount IS NULL THEN
      FOR curr IN 
      (SELECT * FROM SUBJECTS) LOOP
      PIPE ROW (curr);
      END LOOP;
    ELSE
      FOR curr IN
      (SELECT * FROM SUBJECTS WHERE ROWNUM<=pCount) LOOP
      PIPE ROW (curr);
      END LOOP;
    END IF;
  END GetSubjects;

  FUNCTION GetSpecialties
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetSpecialties
  PIPELINED
  IS
  BEGIN
    IF pCount IS NULL THEN
      FOR curr IN 
      (SELECT * FROM SPECIALTIES) LOOP
      PIPE ROW (curr);
      END LOOP;
    ELSE
      FOR curr IN
      (SELECT * FROM SPECIALTIES WHERE ROWNUM<=pCount) LOOP
      PIPE ROW (curr);
      END LOOP;
    END IF;
  END GetSpecialties;  

  FUNCTION GetDepartmentTypes
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetDepartmentTypes
  PIPELINED
  IS
  BEGIN
    IF pCount IS NULL THEN
      FOR curr IN 
      (SELECT * FROM DEPARTMENT_TYPES) LOOP
      PIPE ROW (curr);
      END LOOP;
    ELSE
      FOR curr IN
      (SELECT * FROM DEPARTMENT_TYPES WHERE ROWNUM<=pCount) LOOP
      PIPE ROW (curr);
      END LOOP;
    END IF;
  END GetDepartmentTypes; 

  FUNCTION GetProgramSubjects
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetProgramSubjects
  PIPELINED
  IS
  BEGIN
    IF pCount IS NULL THEN
      FOR curr IN 
      (SELECT * FROM PROGRAMSUBJECTS) LOOP
      PIPE ROW (curr);
      END LOOP;
    ELSE
      FOR curr IN
      (SELECT * FROM PROGRAMSUBJECTS WHERE ROWNUM<=pCount) LOOP
      PIPE ROW (curr);
      END LOOP;
    END IF;
  END GetProgramSubjects;

  FUNCTION GetExams
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetExams
  PIPELINED
  IS
  BEGIN
    IF pCount IS NULL THEN
      FOR curr IN 
      (SELECT * FROM EXAMS) LOOP
      PIPE ROW (curr);
      END LOOP;
    ELSE
      FOR curr IN
      (SELECT * FROM EXAMS WHERE ROWNUM<=pCount) LOOP
      PIPE ROW (curr);
      END LOOP;
    END IF;
  END GetExams;

  FUNCTION GetOrderItems
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetOrderItems
  PIPELINED
  IS
  BEGIN
    IF pCount IS NULL THEN
      FOR curr IN 
      (SELECT * FROM ORDERS_ITEMS) LOOP
      PIPE ROW (curr);
      END LOOP;
    ELSE
      FOR curr IN
      (SELECT * FROM ORDERS_ITEMS WHERE ROWNUM<=pCount) LOOP
      PIPE ROW (curr);
      END LOOP;
    END IF;
  END GetOrderItems;

  FUNCTION GetDepartments
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetDepartments
  PIPELINED
  IS
  BEGIN
    IF pCount IS NULL THEN
      FOR curr IN 
      (SELECT * FROM DEPARTMENTS) LOOP
      PIPE ROW (curr);
      END LOOP;
    ELSE
      FOR curr IN
      (SELECT * FROM DEPARTMENTS WHERE ROWNUM<=pCount) LOOP
      PIPE ROW (curr);
      END LOOP;
    END IF;
  END GetDepartments;

  FUNCTION GetDepartmentProgram
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetDepartmentProgram
  PIPELINED
  IS
  BEGIN
    IF pCount IS NULL THEN
      FOR curr IN 
      (SELECT * FROM DEPARTMENTPROGRAM) LOOP
      PIPE ROW (curr);
      END LOOP;
    ELSE
      FOR curr IN
      (SELECT * FROM DEPARTMENTPROGRAM WHERE ROWNUM<=pCount) LOOP
      PIPE ROW (curr);
      END LOOP;
    END IF;
  END GetDepartmentProgram;

  FUNCTION GetBranches
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetBranches
  PIPELINED
  IS
  BEGIN
    IF pCount IS NULL THEN
      FOR curr IN 
      (SELECT * FROM BRANCHES) LOOP
      PIPE ROW (curr);
      END LOOP;
    ELSE
      FOR curr IN
      (SELECT * FROM BRANCHES WHERE ROWNUM<=pCount) LOOP
      PIPE ROW (curr);
      END LOOP;
    END IF;
  END GetBranches;

  FUNCTION GetPrograms
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetPrograms
  PIPELINED
  IS
  BEGIN
    IF pCount IS NULL THEN
      FOR curr IN 
      (SELECT * FROM PROGRAMS) LOOP
      PIPE ROW (curr);
      END LOOP;
    ELSE
      FOR curr IN
      (SELECT * FROM PROGRAMS WHERE ROWNUM<=pCount) LOOP
      PIPE ROW (curr);
      END LOOP;
    END IF;
  END GetPrograms;

  FUNCTION GetAcceptancePlans
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetAcceptancePlans
  PIPELINED
  IS
  BEGIN
    IF pCount IS NULL THEN
      FOR curr IN 
      (SELECT * FROM ACCEPTANCE_PLANS) LOOP
      PIPE ROW (curr);
      END LOOP;
    ELSE
      FOR curr IN
      (SELECT * FROM ACCEPTANCE_PLANS WHERE ROWNUM<=pCount) LOOP
      PIPE ROW (curr);
      END LOOP;
    END IF;
  END GetAcceptancePlans;

  FUNCTION GetPriorities
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetPriorities
  PIPELINED
  IS
  BEGIN
    IF pCount IS NULL THEN
      FOR curr IN 
      (SELECT * FROM PRIORITIES) LOOP
      PIPE ROW (curr);
      END LOOP;
    ELSE
      FOR curr IN
      (SELECT * FROM PRIORITIES WHERE ROWNUM<=pCount) LOOP
      PIPE ROW (curr);
      END LOOP;
    END IF;
  END GetPriorities;

  FUNCTION GetCommandments
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetCommandments
  PIPELINED
  IS
  BEGIN
    IF pCount IS NULL THEN
      FOR curr IN 
      (SELECT * FROM COMMANDMENTS) LOOP
      PIPE ROW (curr);
      END LOOP;
    ELSE
      FOR curr IN
      (SELECT * FROM COMMANDMENTS WHERE ROWNUM<=pCount) LOOP
      PIPE ROW (curr);
      END LOOP;
    END IF;
  END GetCommandments;

  FUNCTION GetEntrants
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetEntrants
  PIPELINED
  IS
  BEGIN
    IF pCount IS NULL THEN
      FOR curr IN 
      (SELECT * FROM ENTRANTS) LOOP
      PIPE ROW (curr);
      END LOOP;
    ELSE
      FOR curr IN
      (SELECT * FROM ENTRANTS WHERE ROWNUM<=pCount) LOOP
      PIPE ROW (curr);
      END LOOP;
    END IF;
  END GetEntrants;

  FUNCTION GetHumans
  (pCount NUMBER DEFAULT NULL)
  RETURN tblGetHumans
  PIPELINED
  IS
  BEGIN
    IF pCount IS NULL THEN
      FOR curr IN 
      (SELECT * FROM HUMANS) LOOP
      PIPE ROW (curr);
      END LOOP;
    ELSE
      FOR curr IN
      (SELECT * FROM HUMANS WHERE ROWNUM<=pCount) LOOP
      PIPE ROW (curr);
      END LOOP;
    END IF;
  END GetHumans;

END ALLDATA;
/

SELECT * FROM TABLE(ALLDATA.GetSpecialties);
SELECT * FROM TABLE(ALLDATA.GetSubjects);
SELECT * FROM TABLE(ALLDATA.GetDepartmentTypes);
SELECT * FROM TABLE(ALLDATA.GetProgramSubjects);
SELECT * FROM TABLE(ALLDATA.GetDepartments(5));
SELECT * FROM TABLE(ALLDATA.GetOrderItems);
SELECT * FROM TABLE(ALLDATA.GetExams(5));
SELECT * FROM TABLE(ALLDATA.GetDepartmentProgram(5));
SELECT * FROM TABLE(ALLDATA.GetPrograms(5));
SELECT * FROM TABLE(ALLDATA.GetBranches);
SELECT * FROM TABLE(ALLDATA.GetAcceptancePlans);
SELECT * FROM TABLE(ALLDATA.GetPriorities(5));
SELECT * FROM TABLE(ALLDATA.GetCommandments(5));
SELECT * FROM TABLE(ALLDATA.GetHumans(5));
SELECT * FROM TABLE(ALLDATA.GetEntrants(5));
/
```


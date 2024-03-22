```bash

SET pagesize 50000;
SET long 50000;

SET SERVEROUTPUT ON SIZE 40000
set serveroutput on size unlimited


CREATE OR REPLACE Function ya_pos (addr IN VARCHAR2)
RETURN VARCHAR2
AS
TEXT CLOB;
POS VARCHAR2(50);
BEGIN
TEXT := load_xml('geocode-maps.yandex.ru/1.x/?geocode='||addr);
SELECT 
extractValue(
  extract(
    extract(
      extract(VALUE(t),'/ymaps/GeoObjectCollection/*','xmlns="http://maps.yandex.ru/ymaps/1.x"'),
    'featureMember/*','xmlns="http://www.opengis.net/gml"'),
  'GeoObject/*','xmlns="http://maps.yandex.ru/ymaps/1.x"'),
'Point/pos','xmlns="http://www.opengis.net/gml"')
INTO POS
FROM TABLE(XMLSequence(XMLType(TEXT))) t;
RETURN POS;
END;
/



CREATE OR REPLACE Function get_pos (addr  IN  VARCHAR2)
RETURN VARCHAR2
AS
  tmp VARCHAR2(500);
  pos VARCHAR2(50);
BEGIN
  tmp := REPLACE(addr,' ','+');
  pos := ya_pos(tmp);
  RETURN pos;
END;
/

BEGIN
DBMS_OUTPUT.ENABLE;
DBMS_OUTPUT.PUT_LINE(get_pos('Санкт-Петербург, Вяземский переулок, 5/7'));
END;
/


exec dbms_network_acl_admin.create_acl(acl => 'resolve.xml',description => 'resolve acl', principal =>'ARTEM', is_grant => true, privilege => 'resolve');
exec dbms_network_acl_admin.assign_acl(acl => 'utl_http.xml', host =>'*');
select utl_inaddr.get_host_name('127.0.0.1') from dual;

begin
  dbms_network_acl_admin.create_acl (
    acl         => 'utl_http.xml',
    description => 'HTTP Access',
    principal   => 'ARTEM',
    is_grant    => TRUE,
    privilege   => 'connect',
    start_date  => null,
    end_date    => null
  );
  dbms_network_acl_admin.add_privilege (
    acl        => 'utl_http.xml',
    principal  => 'ARTEM',
    is_grant   => TRUE,
    privilege  => 'resolve',
    start_date => null,
    end_date   => null
  );
  dbms_network_acl_admin.assign_acl (
    acl        => 'utl_http.xml',
    host       => 'www.geocode-maps.yandex.ru',
    lower_port => 80,
    upper_port => 80
  );
  commit;
end;



load_xml('geocode-maps.yandex.ru/1.x/?geocode=Санкт-Петербург+Новоизмайловский+проспект,16,корпус+8');

CREATE OR REPLACE Function load_xml (p_url  IN  VARCHAR2)
RETURN clob
AS
  l_http_request   UTL_HTTP.req;
  l_http_response  UTL_HTTP.resp;
  l_clob           CLOB;
  l_text           VARCHAR2(32767);
BEGIN
  -- Initialize the CLOB.
  DBMS_LOB.createtemporary(l_clob, FALSE);

  -- Make a HTTP request and get the response.
  l_http_request  := UTL_HTTP.begin_request(p_url);
  l_http_response := UTL_HTTP.get_response(l_http_request);

  -- Copy the response into the CLOB.
  BEGIN
    LOOP
      UTL_HTTP.read_text(l_http_response, l_text, 32766);
      DBMS_LOB.writeappend (l_clob, LENGTH(l_text), l_text);
    END LOOP;
  EXCEPTION
    WHEN UTL_HTTP.end_of_body THEN
      UTL_HTTP.end_response(l_http_response);
  END;
  -- Relase the resources associated with the temporary LOB.
  RETURN l_clob;
  DBMS_LOB.freetemporary(l_clob);
EXCEPTION
  WHEN OTHERS THEN
    UTL_HTTP.end_response(l_http_response);
    DBMS_LOB.freetemporary(l_clob);
    RAISE;
END load_xml;
/

BEGIN
DBMS_OUTPUT.ENABLE;
DBMS_OUTPUT.PUT_LINE(load_xml('geocode-maps.yandex.ru/1.x/?geocode=Санкт-Петербург+Новоизмайловский+проспект,16,корпус+8'));
END;
/
```
<h2> Aqui esta todo el codiguito</h2>

CREATE TABLE CLIENTE (ID_CLIENTE INTEGER,
NOMBRE VARCHAR2(30),
SUELDO_BASE FLOAT, 
EMAIL VARCHAR2(30), 
CONSTRAINT PK_ID_CLIENTE PRIMARY KEY (ID_CLIENTE));

CREATE TABLE DIRECCION (ID_DIRECCION INTEGER,
ID_CLIENTE INTEGER,
CALLE VARCHAR2(30),
NUMERO_BASE INTEGER, 
CP INTEGER, 
MUNICIPIO VARCHAR2(30),


CONSTRAINT PK_ID_DIRECCION PRIMARY KEY (ID_DIRECCION),
CONSTRAINT FK1_ID_CLIENTE FOREIGN KEY (ID_CLIENTE)
REFERENCES CLIENTE(ID_CLIENTE));


create sequence sec_CLIENTE
start with 1
increment by 1
nomaxvalue;



create sequence sec_DIRECCION
start with 1
increment by 1
nomaxvalue;
CREATE OR REPLACE PROCEDURE GUARDAR_CLIENTE(MY_ID_CLIENTE  OUT INTEGER,
MY_NOMBRE IN VARCHAR2, MY_SUELDO_BASE IN FLOAT, MY_EMAIL IN VARCHAR2)
AS
BEGIN
SELECT SEC_CLIENTE.NEXTVAL INTO MY_ID_CLIENTE FROM DUAL;
INSERT INTO CLIENTE VALUES(MY_ID_CLIENTE,MY_NOMBRE,MY_SUELDO_BASE,MY_EMAIL);
END;
/

CREATE OR REPLACE PROCEDURE GUARDAR_CLIENTE_DIRECCION(MY_ID_CLIENTE OUT INTEGER,
MY_ID_DIRECCION OUT INTEGER, MY_NOMBRE IN VARCHAR2, MY_SUELDO_BASE IN FLOAT,
MY_EMAIL IN VARCHAR2, MY_CALLE IN VARCHAR2,MY_NUMERO_BASE IN INTEGER, 
MY_CP IN INTEGER, MY_MUNICIPIO IN VARCHAR2) AS
BEGIN
GUARDAR_CLIENTE(MY_ID_CLIENTE, MY_NOMBRE, MY_SUELDO_BASE,MY_EMAIL);
SELECT SEC_DIRECCION.NEXTVAL INTO MY_ID_DIRECCION FROM DUAL;
INSERT INTO DIRECCION VALUES(MY_ID_DIRECCION, MY_ID_CLIENTE, MY_CALLE,
MY_NUMERO_BASE,MY_CP, MY_MUNICIPIO);
END;
/

´´´

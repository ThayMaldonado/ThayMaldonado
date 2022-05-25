CREATE TABLE inquilino
(
codigo_inquilino VARCHAR2(100) not null,
nif varchar2(100),
nombre_inquilino varchar2(100),
apellido_inquilino varchar2(100),
fecha_na varchar2(100),
tel_cont number(10),
CONSTRAINT pk_codigo_inquilino PRIMARY KEY (codigo_inquilino)
);

CREATE TABLE agencia
(
id_agencia VARCHAR2(100) not null,
cif varchar2(100),
direccion varchar2(100),
telefono varchar2(50),
CONSTRAINT pk_id_agencia PRIMARY KEY (id_agencia)
);

CREATE TABLE alquiler
(
codigo_alquiler VARCHAR2(100) NOT NULL,
tipo_alquiler VARCHAR2(100),
fecha_inicio DATE,
fecha_fin DATE,
importe_mensual VARCHAR2(100),
finanza VARCHAR2(100),
fecha_firma DATE,
id_inquilino VARCHAR2(100),
id_agencia_alquiler VARCHAR2(100),
CONSTRAINT pk_codigo_alquiler PRIMARY KEY (codigo_alquiler),
FOREIGN KEY (id_inquilino) REFERENCES inquilino (codigo_inquilino),
FOREIGN KEY (id_agencia_alquiler) REFERENCES agencia (id_agencia)
);

CREATE TABLE vivienda
(	
id_vivienda VARCHAR2(100) not null,
codigo_agencia VARCHAR2(100),
calle varchar2(100),
numero number(10),
piso number(10),
codigo_postal varchar2(100),
poblacion varchar2(100),
descripcion varchar2(100),
CONSTRAINT  pk_id_vivienda PRIMARY KEY (id_vivienda),
FOREIGN KEY (codigo_agencia) REFERENCES agencia (id_agencia)


);

CREATE TABLE propietario
(
id_propietario VARCHAR2(20) not null,
codigo_vivienda VARCHAR2(100),
nif varchar2(100),
nombre_propietario varchar2(100),
apellido_propietario varchar2(100),
telefono number(10),
direccion varchar2(100),
email varchar2(100),
CONSTRAINT pk_id_propietario PRIMARY KEY (id_propietario),
FOREIGN KEY (codigo_vivienda) REFERENCES vivienda (id_vivienda)

);


INSERT INTO inquilino (codigo_inquilino,nif,nombre_inquilino,apellido_inquilino,fecha_na,tel_cont) VALUES ('001d','11222112','mauricio','antor','01/04/1980','675843214');
INSERT INTO inquilino (codigo_inquilino,nif,nombre_inquilino,apellido_inquilino,fecha_na,tel_cont) VALUES ('002d','22111221','thay','vargas','07/03/1985','123214579');

INSERT INTO agencia (id_agencia,cif,direccion,telefono) VALUES ('001a','14534267','nueva providencia 1978','454678945');
INSERT INTO agencia (id_agencia,cif,direccion,telefono) VALUES ('002a','45674345','los leones 3444','123456345');

INSERT INTO alquiler (codigo_alquiler,tipo_alquiler,fecha_inicio,fecha_fin,importe_mensual,finanza,fecha_firma,id_inquilino,id_agencia_alquiler) VALUES ('001c','renovada','20/05/2020','20/05/2022','120000','130000','18/05/2020','001d','001a');
INSERT INTO alquiler (codigo_alquiler,tipo_alquiler,fecha_inicio,fecha_fin,importe_mensual,finanza,fecha_firma,id_inquilino,id_agencia_alquiler) VALUES ('001f','no renovada','17/05/2020','17/05/2022','110000','140000','10/05/2020','002d','002a');

INSERT INTO vivienda (id_vivienda,codigo_agencia,calle,numero,piso,codigo_postal,poblacion,descripcion) VALUES ('004e','001a','avenida siempre viva','2470','2','9090888','7','casa prefabricada');
INSERT INTO vivienda (id_vivienda,codigo_agencia,calle,numero,piso,codigo_postal,poblacion,descripcion) VALUES ('005e','002a','fransico bilbao','6780','3','67867676','9','casa tres pisos');

INSERT INTO propietario (id_propietario,codigo_vivienda,nif,nombre_propietario,apellido_propietario,telefono,direccion,email) VALUES ('20718876-4','004e','3456447','juan','peña','567849780','avenida siempre viva','juanpena@gmail.com');
INSERT INTO propietario (id_propietario,codigo_vivienda,nif,nombre_propietario,apellido_propietario,telefono,direccion,email) VALUES ('17867960-7','005e','5667347','osvaldo','cansino','563455890','fransico bilbao','osvaldocansino@gmail.com');

SELECT v.numero , p.apellido_propietario
FROM vivienda v
INNER JOIN propietario p
on p.codigo_vivienda = v.id_vivienda;

SELECT v.piso , p.nif
FROM vivienda v
INNER JOIN propietario p
ON p.codigo_vivienda = v.id_vivienda;

SELECT v.codigo_postal , p.telefono
FROM vivienda v
INNER JOIN propietario p
ON p.codigo_vivienda = v.id_vivienda;

SELECT a.tipo_alquiler , g.cif
FROM alquiler a
INNER JOIN agencia g
ON g.id_agencia = a.id_agencia_alquiler;

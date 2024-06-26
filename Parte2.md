Parte 2:
Crear una vista donde se muestre la lista de miembros registrados a las conferencias.
           Base de datos: event
           nombre_conferencia | codigo_registro | nombre_miembro 

1)Crear Tabla Conference
CREATE TABLE conference (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(255)
);
2)Crear Tabla Miembros
CREATE TABLE miembros (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(255) NOT NULL,
    apellido VARCHAR(255),
    email VARCHAR(255),
    telefono VARCHAR(20),
    direccion VARCHAR(255)
);
3)Crear Tabla Registration
CREATE TABLE registration (
    id SERIAL PRIMARY KEY,
    conference_id INT,
    member_id INT,
    nombre VARCHAR(255),
    FOREIGN KEY (conference_id) REFERENCES conference(id),
    FOREIGN KEY (member_id) REFERENCES miembros(id)
);
4)Crear Vista de Miembros Registrados
CREATE VIEW vista_registros_conferencias AS
SELECT 
    c.nombre AS nombre_conferencia,
    r.id AS codigo_registro,
    m.nombre AS nombre_miembro
FROM 
    conference c
JOIN 
    registration r ON c.id = r.conference_id
JOIN 
    miembros m ON r.member_id = m.id;
5)Mostrar Lista
SELECT * FROM vista_registros_conferencias;
<img src="/Capturas/Parte 2.png">

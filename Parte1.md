Parte 1:
Crear una vista que muestre la lista de productos comprados por los clientes con las siguientes columnas: 
           Base de datos: invoice
           nombre_cliente | fecha_compra | nombre_producto | cantidad

1)Tabla Client
CREATE TABLE client (
    id INT PRIMARY KEY,
    nui VARCHAR(50),
    fullname VARCHAR(255),
    address VARCHAR(255)
);
2)Tabla Invoice
CREATE TABLE invoice (
    id INT PRIMARY KEY,
    code VARCHAR(50),
    create_at DATE,
    total DECIMAL(10, 2),
    client_id INT,
    FOREIGN KEY (client_id) REFERENCES client(id)
);
3)Tabla Product
CREATE TABLE product (
    id INT PRIMARY KEY,
    description VARCHAR(255),
    brand VARCHAR(255),
    price DECIMAL(10, 2),
    stock INT
);
4)Tabla Invoice Details
CREATE TABLE invoice_details (
    id INT PRIMARY KEY,
    invoice_id INT,
    product_id INT,
    quantity INT,
    FOREIGN KEY (invoice_id) REFERENCES invoice(id),
    FOREIGN KEY (product_id) REFERENCES product(id)
);
5)Vista de Productos
CREATE VIEW productos_comprados AS
SELECT 
    c.fullname AS nombre_cliente, 
    i.create_at AS fecha_compra, 
    p.description AS nombre_producto, 
    d.quantity AS cantidad
FROM 
    client c
JOIN 
    invoice i ON c.id = i.client_id
JOIN 
    invoice_details d ON i.id = d.invoice_id
JOIN 
    product p ON d.product_id = p.id;
6) Mostrar lista
SELECT * FROM productos_comprados;
<img src="/Capturas/Parte 1.png">


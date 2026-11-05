# Práctica: Gestión de Inventario y Pedidos con JDBC, Maven y Lombok

Aplicación de consola en Java que gestiona las operaciones de inventario y pedidos conectándose a una base de datos relacional MySQL / MariaDB mediante JDBC, aplicando el patrón DAO y asegurando la integridad transaccional.

---

## 🛠️ Tecnologías y Herramientas Utilizadas

- **Lenguaje:** Java 21 (JDK 21)
- **Gestor de dependencias:** Maven
- **Librerías:** 
  - `mysql-connector-j` (Driver oficial JDBC Tipo 4)
  - `Project Lombok` (Reducción de boilerplate en POJOs)
- **Base de Datos:** MySQL / MariaDB (XAMPP)
- **Gestor visual de BD:** DBeaver Community
- **IDE:** IntelliJ IDEA

---

## 🗄️ Modelo de Base de Datos (`tiendaDB`)

La base de datos se compone de dos tablas con relación de clave foránea (1:N):

1. **`productos`**: Almacena el catálogo y stock actual.
   - `id_producto` (INT, PK, Auto-increment)
   - `nombre` (VARCHAR 150)
   - `precio` (DECIMAL 10,2)
   - `stock` (INT)

2. **`pedidos`**: Registra los pedidos realizados vinculados a un producto.
   - `id_pedido` (INT, PK, Auto-increment)
   - `fecha_pedido` (DATE)
   - `cantidad` (INT)
   - `id_producto` (INT, FK -> `productos.id_producto`)

---

## 📂 Arquitectura del Proyecto

El código fuente sigue el patrón de diseño DAO (Data Access Object) y se organiza en los siguientes paquetes:

```text
src/main/java/com/tienda/
├── app/
│   └── Main.java              # Interfaz de consola y menú interactivo
├── conexion/
│   └── ConexionDB.java        # Centralización de la conexión segura JDBC
├── dao/
│   ├── ProductoDAO.java       # Operaciones sobre productos (Insertar, Consultar ID, Modificar Stock)
│   └── PedidoDAO.java         # Operaciones sobre pedidos (Transacción ACID y Consulta con JOIN)
└── model/
    ├── Producto.java          # POJO para Producto anotado con Lombok
    └── Pedido.java            # POJO para Pedido anotado con Lombok

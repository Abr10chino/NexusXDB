# 📦 NexusX — Capa de Base de Datos e Infraestructura

Este directorio contiene la configuración de la infraestructura de datos y la documentación del modelo relacional para la plataforma **NexusX**. Aquí se centraliza la definición de tablas, los scripts de inicialización de MySQL 8.0 y la orquestación en contenedores mediante Docker.

---

## 🛠️ Tecnologías Utilizadas

* **Gestor de Base de Datos:** MySQL 8.0
* **Orquestación y Contenedores:** Docker & Docker Compose
* **Gestor SQL Recomendado:** DBeaver / MySQL Workbench

---

## 📂 Archivos del Directorio

En esta carpeta encontrarás los siguientes componentes clave:

| Archivo | Descripción |
| :--- | :--- |
| `docker-compose.yml` | Archivo de orquestación para levantar el contenedor MySQL (`dbNexusX`) en el puerto `3307`. |
| `db.sql` | Script SQL de creación del esquema `nexusXDB`, tablas, claves primarias/foráneas y datos semilla. |
| `NexusX ERD.png` | Diagrama Entidad-Relación (MER) en formato de alta resolución (fondo transparente). |
| `Nexus ERD.jpeg` | Vista rápida en formato imagen del Diagrama Entidad-Relación. |
| `LICENSE` | Licencia MIT de uso y distribución del software. |

---

## 📐 Esquema de la Base de Datos (`nexusXDB`)

El modelo está compuesto por 4 tablas principales organizadas en dos dominios:

### 1. Dominio de Catálogo de Productos
* **`categories`**: Almacena las categorías de los productos.
* **`products`**: Registra los artículos del catálogo con su código único, precio, stock y relación.

### 2. Dominio de Carga e Importaciones CSV
* **`imports`**: Guarda el historial y estado de cada archivo CSV procesado (`processed_at`, `total_rows`, `accepted_rows`, `rejected_rows`, `status`).
* **`import_errors`**: Registra las filas rechazadas en una importación, capturando el número de fila (`` `row_number` ``), la trama cruda (`raw_data`) y el motivo del fallo.

> ⚠️ **Nota técnica:** La columna `` `row_number` `` en `import_errors` utiliza comillas invertidas (*backticks*) para evitar conflictos con la palabra reservada de MySQL 8.0 (`ROW_NUMBER()`).

---

## 🚀 Cómo Desplegar y Levantar la Base de Datos

### Requisitos Previos
* Tener instalado **Docker** y **Docker Desktop / Engine**.
* Clonar o descompilar este proyecto en tu máquina local.

### Pasos de Ejecución

1. **Abrir la terminal** en este directorio (`db/`).
2. **Levantar el contenedor con Docker Compose:**
   ```bash
   docker compose up -d
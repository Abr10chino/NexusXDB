# NexusX - Database Module

## 🛠️ Tecnologías

- MySQL 8.0
- Docker
- Docker Compose
- DBeaver (opcional)

## 📁 Estructura del directorio

| Archivo | Descripción |
|---|---|
| `docker-compose.yml` | Configuración del contenedor MySQL. |
| `db.sql` | Script de creación e inicialización de `nexusXDB`. |
| `NexusX ERD.png` | Diagrama Entidad-Relación. |
| `Nexus ERD.jpeg` | Diagrama alternativo del modelo de datos. |
| `LICENSE` | Licencia MIT. |

## 🗄️ Modelo de datos

La base de datos `nexusXDB` está organizada en dos dominios:

### 1. Catálogo

Gestiona las categorías y los productos.

- `categories`: almacena las categorías.
- `products`: almacena los productos asociados a una categoría.

**Relación 1:N**

```text
categories (1) ───── (N) products
```

Una categoría puede contener múltiples productos.

### 2. Importaciones CSV

Gestiona las importaciones y sus respectivos errores.

- `imports`: registra los procesos de importación.
- `import_errors`: almacena los errores detectados durante cada importación.

**Relación 1:N**

```text
imports (1) ───── (N) import_errors
```

Una importación puede registrar múltiples errores.

> **Nota técnica:** La columna `row_number` de `import_errors` debe escribirse entre comillas invertidas (`` `row_number` ``) en las consultas SQL para evitar conflictos con el nombre de la función de ventana `ROW_NUMBER` de MySQL 8.0.

## 🐳 Despliegue con Docker

**Requisito:** Tener Docker y Docker Compose instalados.

### 1. Iniciar la base de datos

Desde el directorio `db/`, ejecutar:

```bash
docker compose up -d
```

### 2. Verificar el contenedor

```bash
docker compose ps
```

### 3. Consultar los registros

```bash
docker compose logs -f
```

### 4. Detener la base de datos

```bash
docker compose down
```

## 🔌 Conexión desde DBeaver / Cliente SQL

Puedes utilizar DBeaver o cualquier otro cliente compatible con MySQL. Configura la conexión manteniendo los siguientes parámetros:

- **Host:** `localhost`
- **Puerto:** `3307`
- **Base de Datos:** `nexusXDB`
- **Usuario:** `root`
- **Contraseña:** `root`

Una vez establecida la conexión, puedes consultar las tablas y ejecutar consultas SQL.

Para ejecutar el script `db.sql` desde DBeaver:

1. Abrir el archivo en el editor SQL.
2. Seleccionar la conexión correspondiente.
3. Ejecutar el script con `Alt + X`.

## ⚠️ Consideraciones

- El script `db.sql` se ejecuta automáticamente durante la inicialización inicial de MySQL si está montado correctamente en `/docker-entrypoint-initdb.d/`.
- Si el volumen de datos ya fue inicializado, los cambios en `db.sql` no se ejecutan automáticamente.
- Las credenciales indicadas son para desarrollo y no deben utilizarse en producción.

## 📄 Licencia

Distribuido bajo la licencia MIT. Consultar el archivo `LICENSE` para más información.

---

**NexusX | Database Module**
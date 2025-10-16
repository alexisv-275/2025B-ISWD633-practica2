### Crear contenedor de Postgres sin que exponga los puertos. Usar la imagen: postgres:15-alpine3.21
# COMPLETAR

```
docker run -d --name postgres-server -e POSTGRES_DB=postgres -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=admin123 postgres:15 alpine3.21
```

### Crear un cliente de postgres. Usar la imagen: dpage/pgadmin4
```
docker run -d --name pgadmin-client -p 8080:80 -e PGADMIN_DEFAULT_EMAIL=admin@admin.com -e PGADMIN_DEFAULT_PASSWORD=admin123 dpage/pgadmin4
```

# COMPLETAR

La figura presenta el esquema creado en donde los puertos son:
- a: 5432 (postgres)
- b: 80 (puerto interno pgAdmin)
- c: 8080 (puerto externo pgAdmin)

![Imagen](esquema-2-ejercicio.PNG)

## Desde el cliente
### Acceder desde el cliente al servidor postgres creado.
```
docker exec -it postgres-server psql -U postgres -d postgres
```

# COMPLETAR CON UNA CAPTURA DEL LOGIN
### Crear la base de datos info, y dentro de esa base la tabla personas, con id (serial) y nombre (varchar), agregar un par de registros en la tabla, obligatorio incluir su nombre.

```
-- Crear base de datos
CREATE DATABASE info;

-- Conectarse a la base de datos info
\c info

-- Crear tabla personas
CREATE TABLE personas (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL
);

-- Insertar registros (incluir tu nombre)
INSERT INTO personas (nombre) VALUES (Alexis');
INSERT INTO personas (nombre) VALUES (Daniel');
```

## Desde el servidor postgresl
### Acceder al servidor
### Conectarse a la base de datos info

```
docker exec -it postgres-server psql -U postgres -d postgres
\c info
```
# COMPLETAR
### Realizar un select *from personas
```
-- Consultar registros
SELECT * FROM personas;

-- Salir
\q
```

# AGREGAR UNA CAPTURA DE PANTALLA DEL RESULTADO

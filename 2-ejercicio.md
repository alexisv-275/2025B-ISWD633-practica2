### Crear contenedor de Postgres sin que exponga los puertos. Usar la imagen: postgres:15-alpine3.21
# COMPLETAR
Previo a este paso fue necesario crear una red ya que se producía el error:

[Error -2] Name does not resolve.

Que significa que el contenedor de pgAdmin (pgadmin-client) no puede encontrar una dirección IP para el nombre del servidor que le diste (postgres-server). Docker no está permitiendo la resolución de nombres entre tus dos contenedores.


```
docker network create prac_network
```

```
docker run -d \
  --name postgres-server \
  -e POSTGRES_DB=postgres \
  -e POSTGRES_USER=postgres \
  -e POSTGRES_PASSWORD=admin123 \
  --network prac_network \
  postgres:15-alpine3.21
```

### Crear un cliente de postgres. Usar la imagen: dpage/pgadmin4
```
docker run -d \
  --name pgadmin-client \
  -p 8080:80 \
  -e PGADMIN_DEFAULT_EMAIL=admin@admin.com \
  -e PGADMIN_DEFAULT_PASSWORD=admin123 \
  --network prac_network \
  dpage/pgadmin4
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
<img width="1917" height="1128" alt="image" src="https://github.com/user-attachments/assets/680ddfb0-54ac-4989-8ba2-fed39fd48893" />
<img width="1907" height="1125" alt="image" src="https://github.com/user-attachments/assets/ad814c2b-4f52-4c10-a77c-39b9b76533e0" />


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
<img width="1919" height="1129" alt="image" src="https://github.com/user-attachments/assets/df0f84d3-e290-4d07-8494-85c13cf0b8c4" />


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

<img width="950" height="345" alt="image" src="https://github.com/user-attachments/assets/d5b265b8-6182-4515-aaf1-81f8ea36c6c2" />


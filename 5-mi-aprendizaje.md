# Mi Aprendizaje - Práctica 2

## 🚀 Principales Aprendizajes Logrados

### **Variables de Entorno**
Aprendí a configurar contenedores dinámicamente usando el parámetro `-e`, especialmente para servicios como MySQL y PostgreSQL. Esto permite separar la configuración del código, haciendo las aplicaciones más portables y seguras.

### **Redes de Docker**
Aprendí de la creación de redes personalizadas con `docker network create` y la comunicación entre contenedores. Los contenedores en la misma red pueden comunicarse usando sus nombres como hostnames, lo que es fundamental para arquitecturas multi-contenedor.

### **Arquitecturas Multi-Contenedor**
Implementé sistemas donde cada contenedor tiene una responsabilidad específica (base de datos vs aplicación), aprendiendo sobre separación de responsabilidades y persistencia de datos.

---
## 📋 Comandos Docker 

| **Comando** | **Explicación** | **Ejemplo Aplicado** |
|-------------|-----------------|---------------------|
| `docker run -e <var>=<valor>` | Crear contenedor con variables de entorno | `docker run -e POSTGRES_PASSWORD=admin123 postgres:15-alpine3.21` |
| `docker run -p <externo>:<interno>` | Mapear puertos específicos | `docker run -p 8080:80 dpage/pgadmin4` |
| `docker network create <nombre> -d bridge` | Crear red personalizada tipo bridge | `docker network create net-wp -d bridge` |
| `docker run --network <red>` | Conectar contenedor a red específica | `docker run --network net-curso01 nginx:alpine` |
| `docker network connect <red> <contenedor>` | Conectar contenedor existente a red | `docker network connect net-curso02 contenedor3` |
| `docker network disconnect <red> <contenedor>` | Desconectar contenedor de red | `docker network disconnect net-curso01 contenedor1` |
| `docker network ls` | Listar todas las redes disponibles | `docker network ls` |
| `docker network inspect <red>` | Inspeccionar configuración de red | `docker network inspect net-wp` |
| `docker network rm <red>` | Eliminar red personalizada | `docker network rm net-curso01` |
| `docker exec -it <contenedor> psql -U <usuario>` | Acceder a PostgreSQL interactivamente | `docker exec -it postgres-server psql -U postgres` |
| `docker run -e MYSQL_ROOT_PASSWORD=<pass>` | Crear MySQL con contraseña root | `docker run -e MYSQL_ROOT_PASSWORD=rootpass mysql:8` |
| `docker run -e WORDPRESS_DB_HOST=<host>` | Configurar WordPress para conectar a BD | `docker run -e WORDPRESS_DB_HOST=mysql_container wordpress` |

### 🔍 Comandos Especiales 

- **Variables múltiples**: `docker run -e VAR1=value1 -e VAR2=value2 image`
- **Configuración PostgreSQL completa**: `docker run -e POSTGRES_DB=info -e POSTGRES_USER=user -e POSTGRES_PASSWORD=pass postgres:15-alpine3.21`
- **Configuración WordPress completa**: `docker run -e WORDPRESS_DB_NAME=wordpress -e WORDPRESS_DB_USER=wpuser -e WORDPRESS_DB_PASSWORD=wppass wordpress`
- **Contenedor sin puertos expuestos**: `docker run -d --name servidor postgres:15-alpine3.21` (sin -p)

---

## 📈 Impacto en mi Formación Profesional

Estos conocimientos me preparan para:
- **Microservicios**: Diseñar sistemas distribuidos modernos
- **DevOps**: Crear entornos reproducibles y escalables  
- **Seguridad**: Manejar configuraciones sensibles correctamente
- **Industria**: Trabajar con el stack tecnológico demandado actualmente

La experiencia práctica con WordPress, MySQL y PostgreSQL me familiarizó con tecnologías ampliamente usadas en la industria.

---

## 🔐 Docker Secrets para Datos Confidenciales

### **¿Qué son?**
Los Docker Secrets gestionan información sensible (contraseñas, certificados) de forma segura en Docker Swarm.

### **Características:**
- **Encriptación**: Almacenados cifrados en el clúster
- **Acceso controlado**: Solo servicios autorizados pueden usarlos
- **Montaje seguro**: Se montan en `/run/secrets/` en memoria

### **Ejemplo:**
```bash
# Crear secreto
echo "password123" | docker secret create db_pass -

# Usar en servicio
docker service create --name mysql \
  --secret db_pass \
  -e MYSQL_ROOT_PASSWORD_FILE=/run/secrets/db_pass \
  mysql:8
```

### **Ventajas sobre variables de entorno:**
- No aparecen en `docker inspect`
- No se guardan en logs del sistema
- Mayor control de acceso y rotación automática

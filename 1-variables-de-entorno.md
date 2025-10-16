# Variables de Entorno
### ¿Qué son las variables de entorno?
Variable dinámica del sistema operativo que permite gestionar configuraciones de aplicaciones. 
# COMPLETAR

### Para crear un contenedor con variables de entorno

```
docker run -d --name <nombre contenedor> -e <nombre variable1>=<valor1> -e <nombre variable2>=<valor2>
```

### Crear un contenedor a partir de la imagen de nginx:alpine con las siguientes variables de entorno: username y role. Para la variable de entorno rol asignar el valor admin.


```
docker run -d --name srv-web -e username=alexis -e role=admin nginx:alpine
```

# COMPLETAR

# CAPTURA CON LA COMPROBACIÓN DE LA CREACIÓN DE LAS VARIABLES DE ENTORNO DEL CONTENEDOR ANTERIOR
<img width="1226" height="370" alt="image" src="https://github.com/user-attachments/assets/90deb578-7d31-494e-9993-09025c0f8fe4" />

```
docker run -d --name srv-web -e username=alexis -e role=admin nginx:alpine
```

<img width="895" height="281" alt="image" src="https://github.com/user-attachments/assets/806842ef-acfd-4c44-b21d-d152d8557ccf" />

### Crear un contenedor con la imagen de mysql, mapear todos los puertos
# COMPLETAR
```
docker run -d --name mysql_db -p 3306:3306 mysql:latest
```

### ¿El contenedor se está ejecutando?
# COMPLETAR
No, no aparece al ejecutar el comando docker ps. 
<img width="1540" height="199" alt="image" src="https://github.com/user-attachments/assets/ef82e758-9d99-411d-85c4-2267053bda09" />


### Identificar el problema
# COMPLETAR
Durante la creación del contenedor con mysql era necesario proveer una de las siguientes variables de entorno: 
- MYSQL_ROOT_PASSWORD
- MYSQL_ALLOW_EMPTY_PASSWORD
- MYSQL_RANDOM_ROOT_PASSWORD
  
<img width="1456" height="243" alt="image" src="https://github.com/user-attachments/assets/f7751184-e91e-48e4-817c-d032bd4ee8ea" />


### Para crear un contenedor con variables de entorno especificadas
- Portabilidad: Las aplicaciones se vuelven más portátiles y pueden ser desplegadas en diferentes entornos (desarrollo, pruebas, producción) simplemente cambiando el archivo de variables de entorno.
- Centralización: Todas las configuraciones importantes se centralizan en un solo lugar, lo que facilita la gestión y auditoría de las configuraciones.
- Consistencia: Asegura que todos los miembros del equipo de desarrollo o los entornos de despliegue utilicen las mismas configuraciones.
- Evitar Exposición en el Código: Mantener variables sensibles como contraseñas, claves API, y tokens fuera del código fuente reduce el riesgo de exposición accidental a través del control de versiones.
- Control de Acceso: Los archivos de variables de entorno pueden ser gestionados con permisos específicos, limitando quién puede ver o modificar la configuración sensible.

### ¿Qué bases de datos existen en el contenedor creado?
# COMPLETAR

En primer lugar fue necesario crear el contenedor proveyendo una de las variables de entorno.
```
docker run -d --name mysql_db -p 3306:3306 -e MYSQL_ROOT_PASSWORD=dbalexis123* mysql:latest
```
```
docker exec mysql_db mysql -u root -pdbalexis123* -e "SHOW DATABASES;"
```
Las bases de datos existentes son: 
- Database
- information_schema
- mysql
- performance_schema
- sys

<img width="1155" height="179" alt="image" src="https://github.com/user-attachments/assets/81b859e7-e53e-409a-8a76-4b1606e94db8" />

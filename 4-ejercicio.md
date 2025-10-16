## Esquema para el ejercicio
![Imagen](esquema-4-ejercicio.PNG)

### Crear la red
# COMPLETAR
```
docker network create net-wp -d bridge
```
### Crear el contenedor mysql a partir de la imagen mysql:8, configurar las variables de entorno necesarias
# COMPLETAR
```
docker run -d --name contenedor_mysql --network net-wp -e MYSQL_ROOT_PASSWORD=rootpassword -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wpuser -e MYSQL_PASSWORD=wppassword mysql:8
```

### Crear el contenedor wordpress a partir de la imagen: wordpress, configurar las variables de entorno necesarias
# COMPLETAR
```
docker run -d --name contenedor_wordpress --network net-wp -p 9300:80 -e WORDPRESS_DB_HOST=contenedor_mysql -e WORDPRESS_DB_NAME=wordpress -e WORDPRESS_DB_USER=wpuser -e WORDPRESS_DB_PASSWORD=wppassword wordpress
```

De acuerdo con el trabajo realizado, en el esquema del ejercicio el puerto a es **9300**

Ingresar desde el navegador al wordpress y finalizar la configuración de instalación.
# COLOCAR UNA CAPTURA DE LA CONFIGURACIÓN
<img width="1848" height="1119" alt="image" src="https://github.com/user-attachments/assets/c168e9dd-6438-4668-a205-4efc88509177" />


Desde el panel de admin: cambiar el tema y crear una nueva publicación.
Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress
# COLOCAR UNA CAPTURA DEL SITO EN DONDE SEA VISIBLE LA PUBLICACIÓN.
<img width="1829" height="1124" alt="image" src="https://github.com/user-attachments/assets/f9df2410-0947-4f9b-b43c-2f68447ea533" />
<img width="1844" height="1115" alt="image" src="https://github.com/user-attachments/assets/46e026fa-511c-40b6-857d-7ef439a14713" />


### Eliminar el contenedor wordpress
# COMPLETAR
```
docker stop contenedor_wordpress
docker rm contenedor_wordpress
```

### Crear nuevamente el contenedor wordpress
Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress
```
docker run -d --name contenedor_wordpress --network net-wp -p 9300:80 -e WORDPRESS_DB_HOST=contenedor_mysql -e WORDPRESS_DB_NAME=wordpress -e WORDPRESS_DB_USER=wpuser -e WORDPRESS_DB_PASSWORD=wppassword wordpress
```

<img width="1462" height="227" alt="image" src="https://github.com/user-attachments/assets/c2335c14-551e-43dc-9c65-4b39b6312db1" />


### ¿Qué ha sucedido, qué puede observar?
# COMPLETAR
Lo que observo es que el sitio que publiqué antes de borrar el contenedor de wp permanece intacto. Según investigo es porque los datos se almacenaron en mysql y dado que este contenedor no fue eliminado, wp al volver a ser creado pudo reconectarse a la bd y recuperar la información. 

<img width="1831" height="1111" alt="image" src="https://github.com/user-attachments/assets/3820cd23-0c70-4825-8f74-cc9fd2a1fb0b" />


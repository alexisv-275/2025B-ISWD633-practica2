# Redes
Las redes son un componente fundamental que permite la comunicación entre contenedores, así como la comunicación de los contenedores con el mundo exterior. 
![Imagen](redes.PNG)
- Bridge: Esta es la red por defecto en Docker. Permite la comunicación entre contenedores en el mismo host. Cada contenedor conectado a la red bridge tiene una IP propia en la subred de la red bridge.
    -  Brige por default: Cuando se ejecuta un contenedor, Docker crea automáticamente una red de tipo bridge por default. Esta red se utiliza para permitir la comunicación entre contenedores en el mismo host. Cada contenedor conectado a esta red obtiene su propia dirección IP en la subred de la red bridge.
    - Bridge creada por nosotros: Un usuario también puede crear sus propias redes de tipo bridge en Docker. Esto puede ser útil para organizar y segmentar los contenedores de una aplicación de manera más controlada. Al crear una red bridge personalizada, se puede especificar un rango de direcciones IP y otras configuraciones de red específicas. Los contenedores conectados a esta red utilizarán las direcciones IP de la subred definida por el usuario.
- Host: Con esta red, los contenedores comparten la red del host en lugar de tener su propia interfaz de red. Esto puede mejorar el rendimiento de red, pero los contenedores pueden entrar en conflicto con los puertos del host si intentan utilizar los mismos puertos.
- None: Con esta red, se deshabilita la configuración de red. Los contenedores que usan esta red tienen su propia red de loopback y no pueden comunicarse con otros contenedores a menos que se conecten explícitamente a una red.

### Crear una red de tipo bridge

```
docker network create <nombre red> -d bridge
```

### Crear un contenedor vinculado a una red

```
docker run -d --name <nombre contenedor> --network <nombre red> <nombre imagen>
```

### Para saber a qué red está conectado un contenedor

```
docker inspect <nombre contenedor>
```
ó
```
docker network inspect <nombre red> 
```

### Vincular contenedor a una red
```
docker network connect <nombre red> <nombre contenedor>
```

### Para desvincular un contenedor de una red
```
docker network disconnect <nombre red> <nombre contenedor>
```

### Para listar las redes existentes
```
docker network ls
```

### Crear los contenedores y las redes que se presentan en el esquema. Usar para todos los contenedores la imagen de nginx:alpine

![Imagen](esquema-ejercicio-redes.PNG)

### Crear redes
```
docker network create net-curso01 -d bridge
docker network create net-curso02 -d bridge
```

### Crear contenedores 
```
docker run -d --name contenedor1 --network net-curso01 nginx:alpine
docker run -d --name contenedor2 --network net-curso01 nginx:alpine
docker run -d --name contenedor3 --network net-curso01 nginx:alpine
docker network connect net-curso02 contenedor3
docker run -d --name contenedor4 --network net-curso02 nginx:alpine
```

# COLOCAR UNA CAPTURA DE LAS REDES EXISTENTES CREADAS
```
docker network ls
```
<img width="599" height="201" alt="image" src="https://github.com/user-attachments/assets/fdeeed09-a52e-4dd6-81bb-3f858b98d94d" />


# COLOCAR UNA(S) CAPTURAS(S) DE LOS CONTENEDORES CREADOS EN DONDE SE EVIDENCIE A QUÉ RED ESTÁN VINCULADOS
```
docker network inspect net-curso01
```
<img width="1158" height="534" alt="image" src="https://github.com/user-attachments/assets/ec9e724f-c593-41ec-bd42-6d3658b27334" />

```
docker network inspect net-curso02
```
<img width="1179" height="374" alt="image" src="https://github.com/user-attachments/assets/9f6e98f9-f1e9-4842-b240-f2d9ec7a8d98" />



### Para eliminar las redes creadas
```
docker network rm <nombre de la red>
```
```
docker network rm net-curso01
docker network rm net-curso02
```
<img width="589" height="301" alt="image" src="https://github.com/user-attachments/assets/c5f851b0-3683-4264-b8f0-e2c36947d416" />


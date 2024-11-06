# Proyecto Car Sightings - Guía de Pruebas con Imágenes Locales :whale2:

Este proyecto consiste en una serie de servicios contenedorizados utilizando Docker, que incluyen Python, Java, Node.js, Nginx, MongoDB y PostgreSQL. A continuación, se detallan los pasos para ejecutar y probar el proyecto en tu entorno local usando imágenes locales para los servicios principales.

## Requisitos

- Docker y Docker Compose instalados en tu sistema.

## Instrucciones para Probar el Proyecto

### 1. Clona el Repositorio

Si aún no lo has hecho, clona el repositorio y navega al directorio del proyecto:

```bash
git clone https://github.com/briann-duran/Car-Sightings.git
cd Car-Sightings
```
### 2. Construye las Imágenes Locales

Para probar el proyecto usando imágenes locales, asegúrate de construir las imágenes de Python, Java, Node.js y Nginx desde sus respectivos Dockerfiles. Ejecuta los siguientes comandos desde cada subdirectorio del proyecto:

```bash
# En el directorio raíz, navega a cada carpeta y construye las imágenes

cd python_images
docker build -t local_python_images:v1 -f Dockerfile_python_images .
cd ../java_sighting
docker build -t local_java_sighting:v1 -f Dockerfile_java_sighting .
cd ../node_cars
docker build -t local_node_cars:v1 -f Dockerfile_node_cars .
cd ../nginx
docker build -t local_nginx:v1 -f Dockerfile_nginx .
cd ..
```

### 3. Ejecuta Docker Compose
Con las imágenes locales construidas, inicia el proyecto usando Docker Compose desde el directorio raíz del proyecto:

`docker-compose up --build`

### 4. Accede a los Servicios
Una vez que Docker Compose termine de iniciar los contenedores, puedes acceder a los servicios en los siguientes puertos:

- Nginx: `http://localhost:8081/seed`
- Python (Images): `http://localhost:5000/health`
- Java (Sightings): `http://localhost:8082/health`
- Node (Cars): `http://localhost:3000/health`. Si MongoDB está vacío, puedes usar HTTP GET en /seed para llenarlo `mongodb://localhost:3000/seed`
- MongoDB: `mongodb://localhost:27017`
- PostgreSQL: `postgres://localhost:5432`

### 5. Detener el Proyecto
Para detener y eliminar todos los contenedores en ejecución, ejecuta el siguiente comando:

`docker-compose down`

## Notas Adicionales
Este proyecto utiliza volúmenes para la persistencia de datos de MongoDB y PostgreSQL, lo que permite que los datos almacenados persistan aunque los contenedores sean detenidos o eliminados.

Para ajustes adicionales, puedes modificar las configuraciones en el archivo docker-compose.yml o actualizar los servicios individualmente en sus respectivos subdirectorios.

# Prueba la aplicación con el plugin Docker para Intellij IDEA

Instala el siguiente plugin
<img width="490" alt="image" src="https://github.com/user-attachments/assets/5c38a955-f464-4f5b-990e-c5a78d17de1f">

Luego dirigete al archivo `docker-compose.yml` y ejecuta compose presionar el boton :fast_forward:

<img width="959" alt="image" src="https://github.com/user-attachments/assets/6d37ee0a-6414-46c6-9397-824ea83084de">

luego, verifica que los contenedores se han ejecutado correctamente como se muestra en la siguiente imagen:
<img width="959" alt="image" src="https://github.com/user-attachments/assets/7a094918-bfb2-4fd8-9f97-536cfc99559a">

y presiona el siguiente enlace (resaltado en rojo) para visualizar la aplicación:
<img width="959" alt="image" src="https://github.com/user-attachments/assets/525713a3-dcea-4dc1-b3fc-e0220a99db71">

<img width="938" alt="image" src="https://github.com/user-attachments/assets/81ebc83a-ebe4-4df2-a63c-897065dfa7fa">

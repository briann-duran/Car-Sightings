# Proyecto Car Sightings

Este proyecto consiste en una serie de servicios contenedorizados utilizando Docker, que incluyen Python, Java, Nginx, MongoDB, PostgreSQL y más. A continuación, encontrarás instrucciones para ejecutar el proyecto en tu entorno local utilizando Docker Compose y detalles sobre las imágenes de Docker que se han subido a Docker Hub.

## Requisitos

- Docker y Docker Compose instalados en tu máquina.
- Acceso a un terminal/ventana de comandos.

## Cómo ejecutar el proyecto

Para ejecutar este proyecto, puedes usar Docker Compose, que se encarga de levantar todos los servicios definidos en el archivo `docker-compose.yml`. Sigue estos pasos:

### 1. Clona el repositorio

Si aún no has clonado el repositorio, puedes hacerlo con:

```bash
git clone https://github.com/briann-duran/Car-Sightings.git
cd Car-Sightings

Car-Sightings/
  ├── docker-compose.yml
  ├── nginx/
      ├── default.conf
      ├── html/
          ├── index.html
          ├── main.js
          ├── bootstrapxxxx.min.css
          ├── bootstrapxxxx.min.js
          ├── style.css

### 2. Una vez tengas todo configurado, navega a la carpeta donde se encuentra el archivo docker-compose.yml y ejecuta:

`docker-compose up --build`

### 3. Este comando descargará las imágenes necesarias (si no están ya en tu máquina) y luego levantará los servicios definidos en el archivo. Los servicios estarán disponibles en los siguientes puertos:

Nginx: `http://localhost:8081`
Python (Images): `http://localhost:5000`
Java (Sightings): `http://localhost:8082`
Node (Cars): `http://localhost:3000`
MongoDB: `mongodb://localhost:27017`
PostgreSQL: `postgres://localhost:5432`

### 4. Detener los servicios

Para detener los contenedores en ejecución, puedes usar:
`docker-compose down`

Este comando detiene y elimina los contenedores creados por Docker Compose.

## Imágenes en Docker Hub

He subido las imágenes utilizadas en este proyecto a mi cuenta de Docker Hub. Puedes obtener las siguientes imágenes públicas y utilizarlas de la siguiente manera:

### 1. Python Images

Imagen de Python para gestionar las imágenes subidas:

`docker pull brianduran/python_images:v1`

### 2. Java Sighting

Imagen de la aplicación Java (Spring Boot) para manejar los avistamientos:

`docker pull brianduran/java_sighting:v1`

### 3. Node Cars

Imagen de la aplicación Node.js para gestionar los autos:

`docker pull brianduran/node_cars:v1`

### 4. Nginx

Imagen del servidor Nginx para servir la aplicación web:

`docker pull brianduran/nginx:v2`

Puedes visitar mi perfil en Docker Hub para obtener más detalles sobre las imágenes disponibles.

#### Estructura del archivo `docker-compose.yml`

Este es el contenido del archivo docker-compose.yml que define los servicios y su configuración:

`version: "3.8"

services:

  # 1. Python_Images
  images:
    image: brianduran/python_images:v1
    ports:
      - "5000:5000"
    environment:
      - UPLOAD_FOLDER=/app/uploads
    volumes:
      - ./python_images/uploads:/app/uploads

  # 2. Java_Sighting
  sightings:
    image: brianduran/java_sighting:v1
    ports:
      - "8082:8080"
    environment:
      - SPRING_DATASOURCE_URL=jdbc:postgresql://db:5432/databaseName
      - SPRING_DATASOURCE_USERNAME=the_username
      - SPRING_DATASOURCE_PASSWORD=the_password
    depends_on:
      - db

  # 3. Postgres
  db:
    image: postgres:14.1-alpine
    environment:
      POSTGRES_DB: databaseName
      POSTGRES_USER: the_username
      POSTGRES_PASSWORD: the_password
    ports:
      - "5432:5432"
    volumes:
      - db_data:/var/lib/postgresql/data

  # 4. Node_Cars
  cars:
    image: brianduran/node_cars:v1
    ports:
      - "3000:3000"
    environment:
      - MONGO_URI=mongodb://mongo:27017/mydatabase
    depends_on:
      - mongo

  # 5. Mongo
  mongo:
    image: mongo:latest
    ports:
      - "27017:27017"
    volumes:
      - mongo_data:/data/db

  # 6. Nginx
  nginx:
    image: brianduran/nginx:v2
    ports:
      - "8081:80"
    volumes:
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf
      - ./nginx/html:/usr/share/nginx/html
    depends_on:
      - images
      - sightings
      - cars

# Se persistirán los datos de Posgres y Mongo
volumes:
  db_data:
  mongo_data:
`

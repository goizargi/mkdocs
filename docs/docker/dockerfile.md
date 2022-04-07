### Dockerfile

#### Para que sirve?

Archivo sin extension que crea imagenes de docker acorde a los comandos/instrucciones previamente establecidos

#### Como se crea?

    FROM Nombre_imagen
    ENV [variables de entorno]
    USER [Nombre de usuario desde el que se quieran ejecutar las instrucciones]
    RUN [comandos a ejecutar]

##### Ejemplos

###### Dockerfile Ubuntu
    FROM ubuntu:latest
    RUN apt-get update && apt-get upgrade
    RUN useradd -m nombre_usuario -p contrasena
    RUN mkdir /home/directorio_usuario/carpeta

* * *

###### Dockerfile Jenkins
    FROM jenkins/jenkins:lts
    ENV contrasena=abcd
    USER root
    RUN echo "hola"
    RUN apt-get update


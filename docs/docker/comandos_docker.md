### Comandos DOCKER

- Descargar una imagen

        docker pull Nombre_imagen

- Ver las imagenes descargadas

        docker images

- Ejecutar una imagen para crear un contenedor

        docker run [opciones] nombre_imagen [comando] . . .        
        docker run jenkins/jenkins:lts

- Crear una imagen a partir de un dockerfile

        docker build [opciones] ruta nombre

- Ver lista de contenedores iniciados

        docker container ls

- Hacer una exportacion de imagen
 
        docker export ID_CONTENEDOR > nombre_archivo.tar
        docker export 55e4472ac30d > prueba.tar

- Hacer una importacion de imagen desde el archivo .tar

        docker import nombre_archivo.tar nombre_imagen_importada
        docker import prueba.tar imagen_prueba

- Crear un contenedor a partir de la imagen importada

        docker run --name nombre_contenedor -ti [-p puerto] nombre_imagen_importada comando
        docker run --name prueba1 -ti imagen_prueba sh

![importarExportar](https://user-images.githubusercontent.com/92585491/156369882-326ee1b6-9937-4ef5-b25c-c1e37f3dfea4.PNG)

![iniciar_mkdocs_puerto](https://user-images.githubusercontent.com/92585491/156369897-38466ae5-aef3-4138-9cf6-d5dce7435865.PNG)

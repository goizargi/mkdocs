Para consultar y administrar un cluster de Kubernetes, se usa la herramienta **kubectl**

- Ver la configuracion actual de kubectl

        kubectl config view

- Cambiar el contexto en uso
  
        kubectl

- Autorizar el agregar un nuevo usuario en **kubeconf**

        kubectl config set-credentials NAME [--client-certificate=ruta_certificado] [--client-key=ruta_keyfile] [--token=bearer_token] [--username=nombre_usuario] [--password=contrasena]

- Configurar la autenticacion basica para "cluster-admin"

        kubectl config set-credentials cluster-admin --username=[nombre_usuario]  --password=[contrasena_usuario]

- Lanzar el dashboard 

        kubectl proxy

- Visualizar el token para iniciar sesion en el dashboard

        kubectl -n kubernetes-dashboard describe secret

#### Creacion de objetos

- Crear recursos definidos a traves de archivos **.yaml** ,**.yml** y **.json**

        kubectl apply -f [archivo.extension]

- Para varios archivos

        kubectl apply -f [archivo1.extension] [archivo2.extension]

- Crear un recurso en todos los archivos del directorio

        kubectl apply -f ./dir

- Crear recursos desde una URL
 
        kubectl apply -f [URL]

- Crear un recurso desde el nombre de la imagen del repositorio

        kubectl create deployment [deployment-name] --image=[image-name]

       - Ejemplo:
        
            kubectl create deployment nginx --image=nginx

- Borrar recursos

        kubectl delete -f ./archivo.extension

- Borrar un pod

        kubectl delete pod nombre_pod


#### Interactuar con pods en ejecucion

- Ejecutar un pod

        kubectl run -i --tty nombre --image=[nombre_imagen] -- sh

- Verificar que un contenedor del pod se esta ejecutando, y ademas, visualizar los cambios en dicho pod

        kubectl get pod nombre_pod --watch

- Abrir una sesion interactiva dentro del contenedor en ejecucion

        kubectl exec -it nombre_contenedor -- /bin/bash

- Adjuntar un pod a un contenedor

        kubectl attach [nombre_pod] -i

- Reenvio de puertos para un pod

        kubectl port-forward [nombre_pod] [puerto_maquina_local]:[puerto_pod]

- Ver IP de un pod

        kubectl get -o template pod nombre_pod --template={{.status.podIP}}

- Instalar el dashboard

        kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.5.1/aio/deploy/recommended.yaml

- Crear un objeto a partir de un fichero YAML

        kubectl create -f nombre_fichero.yaml
 
- Crear una cuenta de servicio para el dashboard

        kubectl create serviceaccount nombre_cuenta

- Enlazar cluster

        kubectl create clusterrolebinding nombre_cuenta --clusterrole=cluster-admin --serviceaccount=default:nombre_cuenta

- Listar los secretos

        kubectl get secrets

- Visualizar el secreto de un usuario

        kubectl describe secret nombre_secreto

- Copiar el secreto, iniciar el dashboard, ir al [enlace para acceder](http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/) y pegar el token para iniciar sesion con el usuario creado

       - Comando para iniciar el dashboard
       
            kubectl proxy

![InkedCaptura_LI](https://user-images.githubusercontent.com/92585491/157859718-5623d43f-427a-478e-be2c-5062ada41bfb.jpg)

####Crear un job

- Comando para crear un job:

        kubectl create job nombre_job --image=nombre_imagen

Ver el job creado en el dashboard:

![Captura2-1](https://user-images.githubusercontent.com/92585491/157858776-2d385db2-43c2-4d2b-8ea0-2deb059b5ecf.png)

####Crear un deployment

    kubectl apply -f /ruta_fichero.yaml

- Fichero YAML:

        apiVersion: apps/v1
        kind: Deployment
        metadata:
        name: nginx-deployment
        labels:
          app: nginx
        spec:
         replicas: 3
         selector:
          matchLabels:
            app: nginx
         template:
          metadata:
            labels:
              app: nginx
          spec:
            containers:
            - name: nginx
              image: nginx:1.14.2
              ports:
              - containerPort: 80

- Visualizar los deployments para comprobar que se ha creado

        kubectl get deployments

- Ver el set de replicas creado por el deployment

        kubectl get rs

- Ver las etiquetas de cada replica

        kubectl get pods --show-labels

![prueba-deployment11](https://user-images.githubusercontent.com/92585491/158187872-d306cab7-8a9d-4f89-92ae-057f58abdc8b.png)

####Actualizar un deployment

    kubectl set image deployment/nginx-deployment nginx=nginx:1.16.1

   *Alternativa*
       
    kubectl edit deployment/nginx-deployment

   Cambiar en la seccion *.spec.template.spec.containers[0].image* la version **nginx:1.14.2** por **nginx:1.16.1** 

- Ver que se ha creado otro set de replicas al actualizar el deployment

        kubectl get rs

- Ver los detalles del deployment

        kubectl describe deployments

![prueba-deployment2](https://user-images.githubusercontent.com/92585491/158186733-5a6d2be0-06f1-44dd-a74b-76551f87c4b9.PNG)

###Volver un deployment a la version anterior

1. Crear una actualizacion del deployment con errata

        kubectl set image deployment/nginx-deployment nginx=nginx:1.161

2. Ver los pods

        kubectl get pods

    *Aparece uno con un error de imagen*

3. Ver el historial de versiones del deployment

        kubectl rollout history deployment/nginx-deployment

     Para ver mas info de cada revision:

        kubectl rollout history deployment/nginx-deployment --revision=numero_revision

4. Volver a la version anterior

        kubectl rollout undo deployment/nginx-deployment

      4.1. Volver a una version especifica

        kubectl rollout undo deployment/nginx-deployment --to-revision=numero_revision

![prueba-deployment3](https://user-images.githubusercontent.com/92585491/158186735-d7df96c7-0c0b-4a68-a254-644aa7e452a2.PNG)

![prueba-deployment4](https://user-images.githubusercontent.com/92585491/158186736-5cba1d89-f874-4576-bf6b-573be650e965.PNG)

![prueba-deployment5](https://user-images.githubusercontent.com/92585491/158186739-ec1d47bf-c3dd-4b4b-b637-c5ebc30abd2a.PNG)

####Escalar un deployment

     kubectl scale deployment/nginx-deployment --replicas=10

1. Comprobar que las replicas estan funcionando

        kubectl get deploy

2. Actualizar a una imagen no existente

        kubectl set image deployment/nginx-deployment nginx=nginx:nombre_falso

3. Ver el nuevo set de replicas

        kubectl get rs

![prueba-deployment6](https://user-images.githubusercontent.com/92585491/158186741-8dea7374-ade0-4c69-9c0f-dc04eeae3a09.PNG)


######Escalado automatico de un deployment

1. Crear un Dockerfile de php + apache

        FROM php:5-apache
        COPY index.php /var/www/html/index.php
        RUN chmod a+rx index.php

2. Crear un deployment 

        kubectl apply -f /ruta_fichero.yaml

     - Fichero YAML

            apiVersion: apps/v1
            kind: Deployment
            metadata:
              name: php-apache
            spec:
              selector:
                matchLabels:
                  run: php-apache
              replicas: 1
              template:
                metadata:
                  labels:
                    run: php-apache
                spec:
                  containers:
                  - name: php-apache
                    image: k8s.gcr.io/hpa-example
                    ports:
                    - containerPort: 80
                    resources:
                      limits:
                        cpu: 500m
                      requests:
                        cpu: 200m
            ---
            apiVersion: v1
            kind: Service
            metadata:
              name: php-apache
              labels:
                run: php-apache
            spec:
              ports:
              - port: 80
              selector:
                run: php-apache


3. Crear el escalado horizontal automatico

        kubectl autoscale deployment php-apache --cpu-percent=50 --min=1 --max=10

4. Agregar **metrics-server**

        kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.4.1/components.yaml

    - Editar el fichero de metrics-server

            kubectl edit deployments.apps -n kube-system metrics-server 
* * *           
            spec:
              containers:
              - args:
                - --cert-dir=/tmp
                - --secure-port=4443
                - --kubelet-insecure-tls=true
                - --kubelet-preferred-address-types=InternalIP

5. Ver el estado del HPA (HorizontalPodAutoscaler)
  
        kubectl get hpa

6. Aumentar la carga

    - En otra ventana de PowerShell

            kubectl run -i --tty load-generator --rm --image=busybox --restart=Never -- /bin/sh  -c "while sleep 0.01; do wget -q -O- http://php-apache; done"

    - Ver los cambios en la carga de CPU (Actualiza cada 1 minuto)

            kubectl get hpa php-apache --watch

![prueba-deployment7](https://user-images.githubusercontent.com/92585491/158186742-a4e2bb1f-efa9-460e-876d-73af2ad507c4.PNG)

![prueba-deployment8](https://user-images.githubusercontent.com/92585491/158186744-22a66256-eaf3-4cd2-83a7-d45cf090ac78.PNG)

![prueba-deployment9-1](https://user-images.githubusercontent.com/92585491/158329192-245c11ce-90dd-435b-ad86-b9a6d8e35bf1.PNG)

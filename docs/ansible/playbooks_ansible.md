###PLAYBOOKs
Ejecutar un playbook:

    ansible-playbook NombrePlaybook.yml
    
  ***En caso de dar fallo:** Comprobar que SSH esta instalado y funcionando. Para instalarlo e iniciarlo:*
  
    yum install openssh-server openssh-client
    service ssh start
        
  - Comprobar que tenemos privilegios. En caso de no tenerlos, ejecutar en la terminal del equipo real:
  
        docker run -d --name nommbreContenedor -it --privileged {ID de la imagen} /usr/sbin/init
	

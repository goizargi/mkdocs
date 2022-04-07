###Ansible

Plataforma de RedHat para orquestar, automatizando y administrando equipos (sin agentes)

Para instalar Ansible manualmente, usar ***yum install ansible***

Archivos a editar:

  - **ansible.cfg**
  
    - Que es?
    
       ***Archivo de configuracion de distintos parametros de Ansible***
            
    - Descomentar los siguientes valores [defaults]
    
          - inventory
       
          - library
      
          - sudo_user
      
          - remote_port
      
    - Descomentar la linea ***"roles_path = /etc/ansible/roles"***
    
    - Descomentar la linea ***"remote_user = root"***
    
    - Descomentar la linea ***"log_path = /var/log/ansible.log"***
    
    - Descomentar la linea ***"display_skipped_hosts = True"*** 
      
	    **Solo si queremos que aparezca el mensaje 'Skipping [host]'**

  - hosts
    - Que es?
    
           Archivo donde se almacenan las conexiones para los PLAYBOOKS
           
    
    - Para añadir un HOST: 
      
       *Direccion IP de la maquina*

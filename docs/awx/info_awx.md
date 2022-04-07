**AWX** es un proyecto comunitario de codigo abierto con el que se proporciona software para administrar proy
ectos de Ansible. AWX se aloja en **GitHub** y en el se proporciona una interfaz de usuario basada en la Web, API 
REST y un motor de tareas para Ansible.

En el panel visual de AWX se permite programar e implementar cuadernos de trabajos de Ansible y se 
proporciona registro, auditoria y seguimiento del sistema centralizados. Mediante AWX se proporciona el 
codigo fuente para **Ansible Tower**, la version comercial de AWX.

*AWX es la version gratuita de Ansible Tower.*

#### **Implementacion en Ubuntu 20.04**

1. Actualizar el sistema e instalar Ansible

        sudo apt update
        sudo apt upgrade
        sudo apt install ansible

2. Instalar Docker y Docker Compose

    - Docker:

            sudo apt install apt-transport-https ca-certificates curl software-properties-common gnupg-agent
            curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
            sudo apt update
            sudo apt install docker-ce
            sudo /etc/init.d/docker start

    - Docker Compose:
            
            sudo apt install docker-compose

3. Instalar Node y NPM

    - Node:
   
            sudo apt install nodejs npm

    - NPM:

            sudo npm install npm --global

4. Instalar AWX

     - Instalar  el modulo **docker-py python**

            sudo apt install python3-pip git pwgen vim
     
     - Descargar el fichero AWX desde **GitHub** y descomprimirlo
 
            wget https://github.com/ansible/awx/archive/17.1.0.zip
            unzip 17.1.0.zip

     - Ir a la carpeta *awx/installer* y generar una key secreta

            cd awx-17.1.0/installer/
            pwgen -N 1 -s 30
     
     - Editar el fichero *inventory* con lo siguiente:      
            
            sudo nano inventory
                 
                  dockerhub_base=ansible 
                  awx_task_hostname=awx 
                  awx_web_hostname=awxweb 
                  postgres_data_dir=/tmp/pgdocker 
                  host_port=80 
                  host_port_ssl=443 
                  docker_compose_dir=/tmp/awxcompose 
                  pg_username=awx 
                  pg_password=awxpass 
                  pg_database=awx 
                  pg_port=5432 
                  admin_user=admin 
                  admin_password=password 
                  create_preload_data=True 
                  secret_key=<clave_secreta>
     
     - Ejecutar el playbook *install.yml*
 
            ansible-playbook -i inventory install.yml

5. Comprobar los contenedores

        docker ps

6. Acceder a la web: ***http://IP_MAQUINA***

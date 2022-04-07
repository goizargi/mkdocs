###Agentes/nodos

- Generar la clave SSH en el maestro *(Contenedor Jenkins)*

![image](https://user-images.githubusercontent.com/92585491/140940804-3930608a-f2b0-48aa-a0ea-f5e2f9a22598.png)

- Instalar Java en el nodo esclavo *(Ubuntu)*

    - Añadir el repositorio:

        apt install software-properties-common apt-transport-https -y
        add-apt-repository ppa:openjdk-r/ppa -y
      
    - Instalar **Java OpenJDK**
      
        apt install openjdk-8-jdk -y

- Crear un usuario en el contenedor del nodo *(Ubuntu)*

     ![image](https://user-images.githubusercontent.com/92585491/140941524-099fcd45-a830-449f-b5ff-7e3ecbef767c.png)

- Añadir nuevas credenciales en Jenkins desde el administrador:

    - **Tipo:** Usuario SSH con clave privada
    - **Usuario:** --> El que se haya creado en el paso anterior
    - Introducir clave privada directamente *(Copiar la clave conseguida a traves del paso **1**)*
 
   
- Habilitar puertos SSH
![image](https://user-images.githubusercontent.com/92585491/140940564-84aad497-020f-4047-aea6-ecc71e589834.png)
*Contenedor nodo (ubuntu)*

![image](https://user-images.githubusercontent.com/92585491/140940446-a4af073b-aadc-4727-bc18-94c099b9f5f2.png)
*Contenedor Jenkins*
    
- Añadir la clave ssh al nodo esclavo (Ubuntu)
![image](https://user-images.githubusercontent.com/92585491/140940274-ca5d1aab-1d01-4150-82c3-c2dd24f26900.png)

- Agregar un nodo desde el administrador de Jenkins

    - **Nombre:** Nombre del nodo
    - **Directorio raiz remoto:** Carpeta */home* del usuario que se haya creado en el paso **3** 
    - **Metodo de ejecucion:** Arrancar agentes remotos en maquinas Unix via **SSH**
    - **Nombre de maquina: Direccion IP del nodo esclavo *(Ubuntu)*
    - **Credenciales:** Las credenciales que se hayan añadido en el paso 4
    - **Estrategia de verificacion:** Manually trusted key Verification Strategy
    
- Verificar que se establece la conexion
![image](https://user-images.githubusercontent.com/92585491/140944128-ca913474-43a8-46cc-8920-d85427b98a02.png)
![image](https://user-images.githubusercontent.com/92585491/140944175-b132bfb4-0fbe-416a-977d-86523dd6e4b6.png)

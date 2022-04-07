####Como agregar los servidores al inventario en Ansible

1. Conexion SSH usando PuTTY

   - IP: 172.21.10.49 (GES1RANSIBLE)

   - Usuario: root
   
   1.1. Anadir la clave privada para autenticar la conexion
  
   - ***Menu izquierdo** > Connection > SSH > Auth*
      
     - *"Private key file for authentication"* --> Agregar el fichero de la key previamente proporcionado  
   
   1.2. Volver a **"Session"** dentro del menu izquierdo, poner nombre a la sesion y guardarla con todas las configuraciones.

   1.5. Iniciar conexion (Open)
 
   1.6. Ir a "/ansible" y editar el fichero **inventory_R2**
      
   - Agregar los servidores siguiendo el formato

   1.7. Lanzar el fichero haciendo un *ping* a los servidores especificados 
   
    ansible -i inventory_R2 -m ping nombre_servidor1, nombre_servidor2, nombre_servidor3...

   

- Nueva tarea --> Pipeline
- Opciones a configurar:
    - "Esta opcion debe parametrizarse":
      - Se pueden añadir distintos parametros dentro del Build
  - Puede ser ***cadena, contraseña, ejecucion, boolean***.
  
**EJEMPLO:**
  
        pipeline {
          agent any 
          stages {
              stage('Build') { 
                steps {
                  echo "Hola ${params.text}"
                }
              }
          }
        }

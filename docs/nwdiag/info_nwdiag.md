### Que es?

nwdiag permite dibujar diagramas de red. 


###Ejemplos basicos

####1. Diagrama simple

1. Definir una red

        @startuml
        nwdiag {
           network dmz {
               address = "210.x.x.x/24"
           }
        }
        @enduml

2. Definir elementos/servidores en una red

        @startuml
        nwdiag {
          network dmz {
              address = "210.x.x.x/24"

              web01 [address = "210.x.x.1"];
              web02 [address = "210.x.x.2"];
          }
        }
        @enduml

    ![1](https://drive.google.com/uc?export=view&id=1iYd3dLEl362d9FJOZxRrwkn4g_M2z_ff)

3. Ejemplo completo

        @startuml
        nwdiag {
          network dmz {
              address = "210.x.x.x/24"

              web01 [address = "210.x.x.1"];
              web02 [address = "210.x.x.2"];
          }
          network internal {
              address = "172.x.x.x/24";

              web01 [address = "172.x.x.1"];
              web02 [address = "172.x.x.2"];
              db01;
              db02;
          }
        }
        @enduml

    ![2](https://drive.google.com/uc?export=view&id=1V84Q1385h1vfqUltpZ9iRN4OUdijiey5)

####2. Definir multiples direcciones

     @startuml
     nwdiag {
       network dmz {
           address = "210.x.x.x/24"
           // Definir varias direcciones (usando coma)
           web01 [address = "210.x.x.1, 210.x.x.20"];
           web02 [address = "210.x.x.2"];
       }
       network internal {
           address = "172.x.x.x/24";
           web01 [address = "172.x.x.1"];
           web02 [address = "172.x.x.2"];
           db01;
           db02;
       }
     }
     @enduml

   ![3](https://drive.google.com/uc?export=view&id=1-2V-OvZXraCJclNGCM2E5qlO8J6QUtyF)

####3. Agrupar nodos

1. Definir un grupo dentro de las definiciones de red

        @startuml
        nwdiag {
          network Sample_front {
             address = "192.168.10.0/24";

             // definir grupo
             group web {
             web01 [address = ".1"];
             web02 [address = ".2"];
             }
          }
          network Sample_back {
             address = "192.168.20.0/24";
             web01 [address = ".1"];
             web02 [address = ".2"];
             db01 [address = ".101"];
             db02 [address = ".102"];

             // definir una red usando nodos previamente definidos
             group db {
               db01;
               db02;
             }
          }
        }
        @enduml

     ![4](https://drive.google.com/uc?export=view&id=1-3rMTElxN2xGahhFxqAEsFvSImm6LWmc)

2. Definir un grupo fuera de las definiciones de red

        @startuml
        nwdiag {
          // definir el grupo fuera de las definiones de red
          group {
            color = "#FFAAAA";
          
            web01;
            web02;
            db01;
          }

          network dmz {
            web01;
            web02;
          }
          network internal {
            web01;
            web02;
            db01;
            db02;
          }
        }
        @enduml

    ![5](https://drive.google.com/uc?export=view&id=1-9jT-ah1MBJs2ktmXMnwLggHgEgB66hG)

3. Definir varios grupos en la misma red

     3.1. Ejemplo con 2 grupos

        @startuml
        nwdiag {
          group {
            color = "#FFaaaa";
            web01;
            db01;
          }
          group {
            color = "#aaaaFF";
            web02;
            db02;
          }
          network dmz {
              address = "210.x.x.x/24"

              web01 [address = "210.x.x.1"];
              web02 [address = "210.x.x.2"];
          }
          network internal {
              address = "172.x.x.x/24";

              web01 [address = "172.x.x.1"];
              web02 [address = "172.x.x.2"];
              db01 ;
              db02 ;
          }
         }
        @enduml

      ![6](https://drive.google.com/uc?export=view&id=1-ACA3e8XcFLGb9PT-b1aJE-aaGXR0xRq)

     3.2. Ejemplo con 3 grupos

        @startuml
        nwdiag {
          group {
             color = "#FFaaaa";
             web01;
             db01;
          }
          group {
             color = "#aaFFaa";
             web02;
             db02;
          }
          group {
             color = "#aaaaFF";
             web03;
             db03;
          }

          network dmz {
              web01;
              web02;
              web03;
          }
          network internal {
              web01;
              db01 ;
              web02;
              db02 ;
              web03;
              db03;
          }
        }
        @enduml

     ![7](https://drive.google.com/uc?export=view&id=1-E_Yiu618BzogEr5O_RAN1XQNVImnLXY)

####4. Sintaxis extendida (Para redes/grupos)

1. Redes - Se pueden agregar varias direcciones, color, descripcion, forma

        @startuml
        nwdiag {
          network Sample_front {
            address = "192.168.10.0/24"
            color = "red"

            // definir grupo
            group web {
              web01 [address = ".1, .2", shape = "node"]
              web02 [address = ".2, .3"]
            }
          }
          network Sample_back {
             address = "192.168.20.0/24"
             color = "palegreen"
             web01 [address = ".1"]
             web02 [address = ".2"]
             db01 [address = ".101", shape = database ]
             db02 [address = ".102"]

             // definir la red usando nodos definidos
             group db {
               db01;
               db02;
             }
          }
        }
        @enduml

     ![8](https://drive.google.com/uc?export=view&id=1-PIfoGapOLImaQE5AsRk9f7Q_wAomkcT)

2. Grupo - Se puede agregar/cambiar color y descripcion

        @startuml
        nwdiag {
          group {
            color = "#CCFFCC";
            description = "Descripcion del grupo";

            web01;
            web02;
            db01;
          }

          network dmz {
              web01;
              web02;
          }
          network internal {
              web01;
              web02;
              db01 [address = ".101", shape = database];
          }
        }
        @enduml

     ![9](https://drive.google.com/uc?export=view&id=1-YnCldRTIhPBlahxcoHK8Ui3g-5tdJwL)

####5. Sprites

*Se pueden usar todos los sprites de la **[Libreria Estandar](https://plantuml.com/es/stdlib)** o cualquier otra libreria*

Usa *"<$sprite>"* para usar un sprite y *\n* para una nueva linea

    @startuml
    !include <office/Servers/application_server>
    !include <office/Servers/database_server>

    nwdiag {
      network dmz {
         address = "210.x.x.x/24"

         // Establecer varias direcciones (usando coma)
         web01 [address = "210.x.x.1, 210.x.x.20",  description = "<$application_server>\n web01"]
         web02 [address = "210.x.x.2",  description = "<$application_server>\n web02"];
      }
      network internal {
         address = "172.x.x.x/24";

         web01 [address = "172.x.x.1"];
         web02 [address = "172.x.x.2"];
         db01 [address = "172.x.x.100",  description = "<$database_server>\n db01"];
         db02 [address = "172.x.x.101",  description = "<$database_server>\n db02"];
      }
    }
    @enduml

   ![10](https://drive.google.com/uc?export=view&id=1-d-rzaQuZ_pd4_5B62r-qV-7pNJDoMgQ)

####6. Iconos

Tambien se pueden usar iconos de [OpenIconic](https://plantuml.com/es/openiconic) en la descripcion de un red o grupo.

Usa *"<$icon>"* para crear un icono, *"<$icon * n>"* para multiplicar el tamano por el factor "n" y *"<\n>"* para una nueva linea.

    @startuml
 
    nwdiag {
      group nightly {
        color = "#FFAAAA";
        description = "<&clock> Restarted nightly <&clock>";
        web02;
        db01;
      }
      network dmz {
         address = "210.x.x.x/24"

         user [description = "<&person*4.5>\n user1"];
         web01 [address = "210.x.x.1, 210.x.x.20",  description = "<&cog*4>\nweb01"]
         web02 [address = "210.x.x.2",  description = "<&cog*4>\nweb02"];

         }
         network internal {
            address = "172.x.x.x/24";

            web01 [address = "172.x.x.1"];
            web02 [address = "172.x.x.2"];
            db01 [address = "172.x.x.100",  description = "<&spreadsheet*4>\n db01"];
            db02 [address = "172.x.x.101",  description = "<&spreadsheet*4>\n db02"];
            ptr  [address = "172.x.x.110",  description = "<&print*4>\n ptr01"];
         }
    }
    @enduml

   ![11](https://drive.google.com/uc?export=view&id=1-d220GWfBLN3f8y1qzTcI7L5wQPp0cMD)

####7. Mismos nodos en mas de dos redes

    @startuml
    nwdiag {
      // definir el grupo fuera de la definicion de la red
      group {
        color = "#7777FF";

        web01;
        web02;
        db01;
      }

      network dmz {
         color = "pink"

         web01;
         web02;
      }

      network internal {
         web01;
         web02;
         db01 [shape = database ];
      }

      network internal2 {
         color = "LightBlue";

         web01;
         web02;
         db01;
      }

    }
    @enduml

   ![12](https://drive.google.com/uc?export=view&id=1-gcjKMtqMEAUc-V319592R7qrZXTUdVJ)

####8. Redes pares (Peer Networks)

Las redes pares son simples conexiones entre dos nodos, en las que no se usa la red "busbar" horizontal.

    @startuml
    nwdiag {
      inet [shape = cloud];
      inet -- router;

      network {
         router;
         web01;
         web02;
      }
    }
    @enduml

   ![13](https://drive.google.com/uc?export=view&id=1-hGhQ0Q-jWOR_1wAJH234NQDZkiig7Hz)

####9. Redes pares y grupos

1. Sin grupo

        @startuml
        nwdiag {
            internet [ shape = cloud];
            internet -- router;

            network proxy {
                router;
                app;
            }
            network default {
                app;
                db;
            }
        }
        @enduml

       ![14](https://drive.google.com/uc?export=view&id=1-mNsmLWasavI-8NUzR4PIPJdU1hAiSTs)

2. Con un grupo primero

        @startuml
        nwdiag {
            internet [ shape = cloud];
            internet -- router;

            group {
              color = "pink";
              app;
              db;
            }

            network proxy {
                router;
                app;
            }

            network default {
                app;
                db;
            }
        }
        @enduml

       ![15](https://drive.google.com/uc?export=view&id=1-sGJki6yFkmQn_LHHZdaTHv76dzIl_gz)

3. Con un grupo segundo

        @startuml
        nwdiag {
            internet [ shape = cloud];
            internet -- router;

            network proxy {
                router;
                app;
            }

            group {
              color = "pink";
              app;
              db;
            }

            network default {
              app;
              db;
            }
        }
        @enduml

       ![16](https://drive.google.com/uc?export=view&id=1-samF3AdSSBuELYcydNxTuOB06MmIa_w)

3. Con un grupo tercero

        @startuml
        nwdiag {
            internet [ shape = cloud];
            internet -- router;

            network proxy {
                router;
                app;
            }
            network default {
                app;
                db;
            }
            group {
              color = "pink";
              app;
              db;
            }
        }
        @enduml

       ![17](https://drive.google.com/uc?export=view&id=1057yzKTDoB6hdXGKwuuAB7GhmFKORmv-)

####10. Anadir titulo, texto, cabecera, pie o leyenda en el diagrama

    @startuml

    header CABECERA

    footer PIE DE PAGINA

    title TITULO

    nwdiag {
       network inet {
           web01 [shape = cloud]
       }
    } 

    legend
      Leyenda
    end legend

    caption Esto es el texto
    @enduml
 
   ![18](https://drive.google.com/uc?export=view&id=106JkKzXOYiIaLbMDfb-qHGipzZlEYY4_)

####11. Otras redes internas

1. Sin direccion o tipo

        @startuml
        nwdiag {
           network LAN1 {
               a [address = "a1"];
           }
           network LAN2 {
               a [address = "a2"];
               switch;
           }
           switch -- equip;
           equip -- printer;
        }
        @enduml

       ![19](https://drive.google.com/uc?export=view&id=10DqAeMS_3GUVpAaAiaESRH7TpCretilX)

2. Con direccion o tipo

        @startuml
        nwdiag {
           network LAN1 {
               a [address = "a1"];
           }
           network LAN2 {
               a [address = "a2"];
               switch [address = "s2"];
           }
           switch -- equip;
           equip [address = "e3"];
           equip -- printer;
           printer [address = "USB"];
        }
        @enduml 

       ![20](https://drive.google.com/uc?export=view&id=10EvN9LxKPNe9Fcd1vco9b-9UUYIPTETP)

####12. Apendice: Todas las formas en *nwdiag*

    @startuml
    nwdiag {
       network Network1 {
           Actor       [shape = actor]       
           Agent       [shape = agent]       
           Artifact    [shape = artifact]    
           Boundary    [shape = boundary]
       }
       network Network2 {
           Card        [shape = card]        
           Cloud       [shape = cloud]       
           Collections [shape = collections]
           Component   [shape = component]   
       }
       network Network3{
           Control     [shape = control]     
           Database    [shape = database]    
           Entity      [shape = entity]      
           File        [shape = file]        
       } 
       network Network4{
           Folder      [shape = folder]      
           Frame       [shape = frame]       
           Hexagon     [shape = hexagon]     
           Interface   [shape = interface]
       }
       network Network5{
           Label       [shape = label]       
           Node        [shape = node]        
           Package     [shape = package]     
           Person      [shape = person] 
       }
       network Network6{
           Queue       [shape = queue]       
           Stack       [shape = stack]       
           Rectangle   [shape = rectangle]   
           Storage     [shape = storage]     
           Usecase     [shape = usecase]
       }
    }
    @enduml

   ![21](https://drive.google.com/uc?export=view&id=10PqYifds43V9jEa2DoI69VBsiiS1bGi1)

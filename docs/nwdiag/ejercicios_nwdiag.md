####Ejercicio 1

    @startuml
    nwdiag {
       network red1{
           address = "192.168.1.0/24";
           BBDD [address = "192.168.1.10"];
           WEB [address = "192.168.1.15, 192.168.1.16"];
       }
       network red2{
           address = "192.168.2.0/24";
           administracion [address = "192.168.2.10"];
           taller [address = "192.168.2.15"];
           WEB [address = "192.168.2.3, 192.168.2.4"];
           BBDD1;
           BBDD2;

           //GRUPO CON NODOS DEFINIDOS
           group BD{
              BBDD1;
              BBDD2;
           }
       }
    }
    @enduml

   ![22](https://drive.google.com/uc?export=view&id=10dlonQuC4gwS49pxcMCzx3qqyx95JmHX)

####Ejercicio 2

    @startuml
    nwdiag {
       //GRUPO FUERA DE LAS DEFINICIONES DE RED
       group{
          color = "#FFAAAA";
          WEB;
          administracion;
          taller;
       }
       network red1{
           address = "192.168.1.0/24";
           BBDD [address = "192.168.1.10"];
           WEB [address = "192.168.1.15, 192.168.1.16"];
       }
       network red2{
           address = "192.168.2.0/24";
           administracion [address = "192.168.2.10"];
           taller [address = "192.168.2.15"];
           WEB [address = "192.168.2.3, 192.168.2.4"];
           BBDD1;
           BBDD2;
    
           //GRUPO CON NODOS DEFINIDOS
           group BD{
              BBDD1;
              BBDD2;
           }
       }
    }
    @enduml

   ![23](https://drive.google.com/uc?export=view&id=10lHUP0DXDPjS4p0Pch2lo2mRd3EFepDy)

####Ejercicio 3

    @startuml
    nwdiag {
        group{
           color = "#FFAAAA";
           WEB;
           administracion;
        }
        group{
           color = "#AAAAFF";
           BBDD;
           taller;
        }
        //ANADIR COLOR Y FORMAS
        network red1{
            address = "192.168.1.0/24";
            color = "blue";
            BBDD [address = "192.168.1.10", shape = database];
            WEB [address = "192.168.1.15, 192.168.1.16"];
        }
        network red2{
            address = "192.168.2.0/24";
            administracion [address = "192.168.2.10"];
            taller [address = "192.168.2.15"];
            WEB [address = "192.168.2.3, 192.168.2.4"];
            BBDD1 [shape = database];
            BBDD2 [shape = database];
            
            group BD{
               BBDD1;
               BBDD2;
            }
        }
    }
    @enduml

   ![24](https://drive.google.com/uc?export=view&id=10mY4M-ydhQNR5Lb3wmUelsKvSlRSFhk8)

####Ejercicio 4

    @startuml
    !include <office/Servers/application_server>
    nwdiag {
        group{
          color = "#FFAAAA";
          WEB;
          administracion;
        }
        group{
          color = "#AAAAFF";
          BBDD;
          taller;
        }
	
        //ANADIR SPRITES
        network red1{
            address = "192.168.1.0/24";
            color = "blue";
            BBDD [address = "192.168.1.10", shape = database];
            WEB [address = "192.168.1.15, 192.168.1.16", description = "<$application_server>\n WEB"];
        }
        network red2{
            address = "192.168.2.0/24";
            administracion [address = "192.168.2.10"];
            taller [address = "192.168.2.15"];
            WEB [address = "192.168.2.3, 192.168.2.4"];
            BBDD1 [shape = database];
            BBDD2 [shape = database];
            
            group BD{
               BBDD1;
               BBDD2;
            }
        }
    }
    @enduml

   ![25](https://drive.google.com/uc?export=view&id=10psXT852rXiiMRiWrkskY8vnxldXnIe0)

####Ejercicio 5

    @startuml
    nwdiag {
        group{
	  color = "#FFAAAA";
          WEB;
          administracion;
        }

        group{
          color = "#AAAAFF";
          BBDD;
          taller;
        }
	
        //ANADIR ICONOS
        network red1{
            address = "192.168.1.0/24";
            color = "blue";
            BBDD [address = "192.168.1.10", shape = database];
            WEB [address = "192.168.1.15, 192.168.1.16"];
        }
        network red2{
            address = "192.168.2.0/24";
            administracion [address = "192.168.2.10"];
            taller [address = "192.168.2.15", description = "<&person*4>\n taller"];
            WEB [address = "192.168.2.3, 192.168.2.4"];
            BBDD1 [shape = database];
            BBDD2 [shape = database];
            
            group BD{
               BBDD1;
               BBDD2;
            }
        }
    }
    @enduml

   ![26](https://drive.google.com/uc?export=view&id=10rmcdd4wTZPjCdb8l7Smn_vAiqNtO8Sm)

####Ejercicio 6

    @startuml
    nwdiag {
       group{
          color = "#FFAAAA";
          WEB;
          administracion;
       }
       group{
          color = "#AAAAFF";
          BBDD;
          taller;
       }
	
       network red1{
          address = "192.168.1.0/24";
          color = "blue";
          BBDD [address = "192.168.1.10", shape = database];
          WEB [address = "192.168.1.15, 192.168.1.16"];
       }
       network red2{
          address = "192.168.2.0/24";
          administracion [address = "192.168.2.10"];
          taller [address = "192.168.2.15", description = "<&person*4>\n taller"];
          WEB [address = "192.168.2.3, 192.168.2.4"];
          BBDD1 [shape = database];
          BBDD2 [shape = database];
         
          group BD{
             BBDD1;
             BBDD2;
          }
       }

       //MISMOS NODOS EN MAS DE DOS REDES
       network red3{
          address = "192.168.3.0/24";
          color = "green";
          BBDD;
          WEB;
       }
    }
    @enduml

   ![27](https://drive.google.com/uc?export=view&id=10wKCpuvsnpzOk-tzzmYbquc3-SmvEJ3X)

####Ejercicio 7

    @startuml
    nwdiag {
       //RED VERTICAL
       internet [shape = cloud];
       internet -- router;
	
       network{
           router;
           WEB;
           BBDD;
       }
    }
    @enduml

   ![28](https://drive.google.com/uc?export=view&id=10wwhRuCNFnymla-Wt1mvLmcPWB-BeRq_)

####Ejercicio 8

    @startuml
    nwdiag {
       //RED VERTICAL SIN GRUPO
       internet [shape = cloud];
       internet -- router;
	
       network red1{
           router;
           WEB;
       }
       network red2{
           WEB;
           BBDD;
       }
    }
    @enduml

   ![29](https://drive.google.com/uc?export=view&id=10zmgadZ777-oAP2CDSb2uJcbat5JOxsy)

####Ejercicio 9

    @startuml
    nwdiag {
       //GRUPO PRIMERO
       internet [shape = cloud];
       internet -- router;
	
       group{
         color = "tomato";
         WEB;
         BBDD;
       }
       network red1{
           router;
           WEB;
       }
       network red2{
           WEB;
           BBDD;
       }
    }
    @enduml

   ![30](https://drive.google.com/uc?export=view&id=116qtdM8G2VU0ZINHGsWkQ-BEA4bjQy9M)

####Ejercicio 10

    @startuml
    nwdiag {
       //GRUPO SEGUNDO
       internet [shape = cloud];
       internet -- router;
	
       network red1{
           router;
           WEB;
       }
       group{
           color = "greenyellow";
           WEB;
           BBDD;
       }
       network red2{
           WEB;
           BBDD;
       }
    }
    @enduml

   ![31](https://drive.google.com/uc?export=view&id=11Ac9hQs44hEq6CJbyVBRJDGCVqmEK4v0)

####Ejercicio 11

    @startuml
    nwdiag {
       //GRUPO TERCERO
       internet [shape = cloud];
       internet -- router;	
	
       network red1{
           router;
           WEB;
       }
       network red2{
           WEB;
           BBDD;
       }

       group{
          color = "royalblue";
          WEB;
          BBDD;
       }
    }
    @enduml

   ![32](https://drive.google.com/uc?export=view&id=11EUFd0uta6LCRAq6RQu8QO8ZoU6TrZ43)

####Ejercicio 12
 
    //ANADIR TITULO, CABECERA, LEYENDA...
    @startuml
    title GRUPOS - 3
    nwdiag {
       //GRUPO TERCERO
       internet [shape = cloud];
       internet -- router;	
	
       network red1{
           router;
           WEB;
       }
       network red2{
           WEB;
           BBDD;
       }

       group{
          color = "royalblue";
          WEB;
          BBDD;
       }
    }
    @enduml

  ![33](https://drive.google.com/uc?export=view&id=11PJ4_3-g1xYUs7oDKrlJ6V0IuwMkRqZL)

####Ejercicio completo

    @startuml
    nwdiag{
       internet [shape = cloud];
       internet -- router;
          network firewall{
              width = full;
              router;
              equipo01;
          }
          network dmz{
              width = full;
              address = "192.168.30.0/24";
              web [address = "192.168.30.3", description = "<&cog*3>\n web", shape = "node"];
          }
          network administracion{
              width = full;
              address = "192.168.10.0/24";
              equipo01;
              impresora [address = "192.168.10.55", description = "<&print*3>\n impresora"];
              bbdd [shape = database];
              empleado01 [address = "192.168.10.10", description = "<&person*3>\n empleado01"];
          }
          network taller{
              width = full;
              address = "192.168.20.0/24";
              empleado02 [address = "192.168.20.10", description = "<&person*3>\n empleado02"];	
              web;
          }
	
          group empleados{
             color = "red";
             empleado01;
             empleado02;
          }
	
          group{
            color = "green";
            web;
            bbdd;
          }

    }
    @enduml

   ![34](https://drive.google.com/uc?export=view&id=10SYFcDaUphbSEBcrfDKgjr4Igfv2qnH8)

# BookStore

 👾👾👾
 <details>
  <summary>Tabla de contenidos</summary>
  <ol>
    <li><a href="#Objetivo">Objetivo</a></li>
    <li><a href="#Setup">Flow</a></li>
            <ol>
            <li><a href="#ec2">EC2</a></li>
            <li><a href="#install-docker">Instalar Docker</a></li>
            <li><a href="#install-docker-compose">Instalar Docker compose</a></li>
            <li><a href="#nginx">Nginx</a></li>
        </ol>
    <li><a href="#testing">Testing</a></li>
  </ol>
</details>


## Objetivo 👌
El proyecto a desplegar en este laboratorio es una aplicación web. La aplicación permite visualizar una colección de recursos, para efectos de este caso, libros. Igualmente, cuando el usuario selecciona alguno de los recursos, se ofrece una vista con información detallada sobre el recurso seleccionado. La información de los recursos (libros) se encuentra almacenada en base de datos. La aplicación tiene tres (vistas): raíz (“/”, home), descripción detallada de los recursos libros y acerca de.

## Setup
### Diagrama de despliegue
![Diagram_desploy_Aws_react-Page-4 drawio](https://user-images.githubusercontent.com/53051443/168497527-fa9b3084-05fe-4fb9-b84d-9fd52d7021d3.svg)

## EC2
Para objetivos con respecto al proyecto dos se tuvo en consideraciones la creación de:

1) EC2(BASTION HOST A)
-- Esta instancia es la encargada de hacer de puente entre las instancias en la zona A y la unica con ip publica 
2) EC2(Frontend A)
-- Esta instancia es la encargada de mostrar con respecto al cliente y se pone lo más cerca en la configuración VPC
-- Actua como la creación base de la AMI,para las plantillas y la respectiva replicación cuando se da la escalabilidad 
3) EC2(Backend)
-- Esta instancia es la encargada de la parte logica  y la conexión con la BD(mongodb)
-- Actua como la creación base de la AMI,para las plantillas y la respectiva replicación cuando se da la escalabilidad de otro backend 
4) EC2(MONGO_NGINX)
-- Esta instancia es la encargada de la parte de tener el mongodb y el nginx para actuar como proxy entre las peticiones entre frontend y backend 
-- Esta instancia de mongo actua como la principal en el modelo de conexiones a BD

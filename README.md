# BookStore


🥤🥤🥤
# Integrantes

## David Felipe Garcia Contreras (dfgarciac1@eafit.edu.co)
## Camilo Cañas Jaramillo (ccanasj@eafit.edu.co)
## Ximena Guerrero Villa (xguerrerov@eafit.edu.co)

 👾👾👾
 <details>
  <summary>Tabla de contenidos</summary>
  <ol>
    <li><a href="#objetivo">Objetivo</a></li>
    <li><a href="#setup">Flow</a></li>
            <ol>
            <li><a href="#ec2">EC2</a></li>
            <li><a href="#docker">Docker</a></li>
            <li><a href="#docker-compose">Instalar Docker compose</a></li>
            <li><a href="#nginx">Nginx</a></li>
            <li><a href="#balancing-change"</a></li>
            <li><a href="#VPC"</a></li>
        </ol>
    <li><a href="#testing">Testing</a></li>
  </ol>
</details>


## Objetivo 👌
El proyecto a desplegar en este laboratorio es una aplicación web. La aplicación permite visualizar una colección de recursos, para efectos de este caso, libros. Igualmente, cuando el usuario selecciona alguno de los recursos, se ofrece una vista con información detallada sobre el recurso seleccionado. La información de los recursos (libros) se encuentra almacenada en base de datos. La aplicación tiene tres (vistas): raíz (“/”, home), descripción detallada de los recursos libros y acerca de.

## Setup
### Diagrama de despliegue
![Diagram_desploy_Aws_react-Page-4 drawio (2)](https://user-images.githubusercontent.com/53051443/168498725-27b5a67b-fec6-40a5-ab63-c1fa3582c80c.svg)
### Diagrama de UPTIME ROBOT 
![image](https://user-images.githubusercontent.com/53051443/168499871-9d2218c8-ad4b-4d05-a2db-85651d453d7b.png)


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

## Docker
```
#'update repo'
sudo apt-get update

#'get neccesay'
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release```
    
#'Docker’s official GPG key:'
 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
 
#'stable repository'
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
#'Install DockerEngine'
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin

#'Docker  installed correctly'
sudo docker run hello-world

```
## Docker-compose
```
 #Install docker compose '
 sudo apt-get update
 sudo apt-get install docker-compose-plugin

```
## Nginx
```
 #Install nginx '
sudo apt update
sudo apt install nginx

```
Luego de tener el nginx instalado se debera modificar de manera que redirija a las privadas del frontend y el backend 

## Balancing-Change
En la sección de balanceadores de carga, creamos un  balanceador de carga, uno para el Front para administrar el enrutamiento público  front-end en diferentes zonas de disponibilidad.

El proceso para crear el balanceador de carga fue el siguiente. Teniendo en cuenta que para el tema del frontend es necesario modificar el nginx la configuración para que no de problemas y se direccione con el balanceador de carga.


### 1 Crear una AMI para la instancia del frontend 
### 2 Crear un targer group 
### 3 Crear el balanceador de carga 
### 4 Crear una plantilla de lanzamiento
### 5 Crear el auto scaling group

## VPC

Para los temas de la VPC se configuraron:

```
DOS ZONAS LA A Y LA B 
DONDE SE HAYAN 1 PUBLICA Y 2 PRIVADAS PARA CADA ZONA DE DISPONIBILIDAD 
```
## DNS 
```
Para los temas del DNS se pidio por medio de la pagina de freenom, donde se resuelve apuntando al balanceador de carga por lo cual el dominio es:
https://pepegan.ga/
```
## Calcula el precio 
https://calculator.aws/#/

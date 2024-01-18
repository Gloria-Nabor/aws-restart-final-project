# aws-restart-final-project

## 📋Descripción General

Este proyecto tiene como objetivo proporcionar información clave para implementar y automatizar servicios en la nube de AWS, específicamente para lanzar un Servidor Web desde la consola de administración de Amazon Web Services (AWS). 

 **Proyecto basado en los laboratorios**:
 
    • 190- [JAWS] - Lab - Automatización de implementaciones con **AWS CloudFormation** (Tareas 1 y 3).
    • 267- [NF]- Lab - Creación de su VPC y lanzamiento de un servidor web

## 📌Abordar los desafíos de la transformación digital:

Esta proyecto aprovecha los beneficios de la nube pública brindando una solución accesible ante las crecientes dificultades que enfrentan los emprendedores y pequeños comercios como son costos elevados o impredecibles, servicios de administración y de escalamiento complejos.  

## Introducción

AWS CloudFormation es un servicio que ofrece una manera sencilla de crear una colección de recursos de AWS.

En la [guía de automatización con Cloud Formation]([aws-cloudformation-user-guide.md](https://github.com/Gloria-Nabor/aws-restart-final-project/blob/ca1795436d1b1cc3822408d63c3a46546ed8c371/aws-cloudformation-user-guide.md) se datalla paso a paso el proceso de configuración de una **VPC** para lanzar un sitio web en una instancia **EC2**. 

## Antes de comenzar, se sugiere tener lo siguiente:

- Una cuenta de AWS (si no cuenta con ella, puede registrarse [aquí](https://aws.amazon.com)). Tambien puede usar la cuenta del entrenamiento AWS re/start que le permita acceder al sandbox correspondiente.

  AWS ofrece un nivel gratuito durante los primeros 12 meses, lo que la convierte en una solución rentable.

- Conocimientos básicos de la consola de administración y servicios de AWS. 
 
## Objetivos:

    • Obtener experiencia práctica en los servicios de AWS.
    • Lanzar un servidor web utilizando múltiples recursos de AWS.
    • Realizar dos implementaciones: manual y automatizada.

# Implementación 1: 
    • Configuración de una VPC e instancia EC2 para alojar un sitio web simple.
    • Un Bucket de S3.

*Habilidades Clave:* 
Mejores prácticas en la arquitectura en AWS, aprendiendo cómo encajan los componentes para brindar una solución integral. 

## Entregables: 
    • Una serie de guías para ayudar a configurar cada recurso.
    • Un video tutorial.

# Implementación 2: 
    • Infraestructura como código (IaC)

*Habilidades Clave:* 
Automatización para creación de un conjunto Recursos.

## Entregables:
    • Crear una pila para implementar los servicios anteriormente mencionados usando CloudFormation.
    • Video demo de la experiencia de automatización.        

# Relevancia del caso empresarial

Café solicita un sitio web básico para promocionarse. Le gustaría comenzar con un sitio web estático que muestre imágenes de productos y detalles de la cafetería, como la ubicación, los horarios de atención y el número de teléfono. 

En el futuro cercano, se podrán implementar funciones como pedidos en línea, seguimiento del historial de pedidos, generación y entrega de informes de ventas, campañas de marketing, y gestión de cortes del servidor con alta disponibilidad y conmutación por error. 

## Infraestructura Empresarial:
El proyecto presenta una infraestructura de nivel empresarial, lo que significa que, a futuro, podrá expandirse aprovechandovpc


otros servicios de AWS. A futuro, es posible incorporar funcionalidades como el escalado automático, copias de seguridad diarias, restauraciones sencillas, actualizaciones administradas, entre otras implementaciones posibles. Esto garantiza que la infraestructura sea flexible y pueda adaptarse a las cambiantes necesidades del negocio, considerando que “Café” tiene planes de expansión.

# Desarrollo del Proyecto

  - **Implementación manual de los servicios siguientes:**
    - Virtual Private Cloud (VPC) 
    - Instancia de Amazon Elastic Compute Cloud (Amazon EC2)
    - Bucket de Amazon Simple Storage Service (Amazon S3)*
      
  - **Automatización con AWS CloudFormation para demostrar la eficiencia de esta tecnología.**

# Propuesta técnica

El cliente ha solicitado crear un sitio web. Comenzar el proyecto con un sitio web estático. 

*Sitio web básico: requisitos técnicos*

**La implementación técnica inicial debe incluir:**
1. Servidor web que almacenará la información del Café (archivos HTML e imágenes*)
2. Una VPC y una instancia EC2 configuradas para alojar un sitio web simple.

## Entrega al Cliente:

    • Una Solución económica, resiliente y segura, basada en la nube con la posibilidad de escalar según la demanda.
    • Una dirección IP pública/URL para acceder al sitio web de Café.
Este enfoque integral busca proporcionar soluciones técnicas efectivas y enfrentar desafíos empresariales con las mejores prácticas de AWS.

# Arquitectura del Proyecto:

## Virtual Private Cloud (VPC)

La infraestructura del proyecto se basa en una VPC, proporcionando un entorno aislado y controlado para los recursos de la aplicación. 

*Componentes clave asociados:*

    - Tabla de ruteo: Controla el tráfico entre la subred e internet.
    - Internet Gateway (IGW): Permite la comunicación entre instancias en la VPC e internet.

## Instancia EC2

El sitio web está alojado en una instancia EC2, proporcionando un entorno de alojamiento flexible y personalizable.

*Componentes clave asociados:*

    - Grupos de Seguridad: Gestiona las reglas de tráfico entrante y saliente a la instancia, proporcionando un control detallado sobre la seguridad y accesibilidad.

     Estos recursos fundamentales de AWS trabajan juntos para crear un entorno de alojamiento del sitio web en AWS. 

## Anexo del Diagrama de Arquitectura [aquí](https://github.com/Gloria-Nabor/aws-restart-final-project/assets/114413852/2deefd25-cc27-40a6-8a18-e9e91d7319db).

# 🚀 AWS CloudFormation: Automatización de Infraestructura

Implementar infraestructura puede ser desafiante, pero con AWS CloudFormation, puede definirse en una plantilla para que los recursos se implementen automáticamente. 

- Este proyecto incluye la implementación de una pila de AWS CloudFormation con una Nube Privada Virtual (VPC) y un grupo de seguridad, junto con una instancia de Amazon Elastic Compute Cloud (EC2). 

# template1.yaml


La plantilla [template1.yaml](https://github.com/Gloria-Nabor/aws-restart-final-project/blob/ca1795436d1b1cc3822408d63c3a46546ed8c371/template1.yaml) está escrita en un formato llamado YAML, que se utiliza habitualmente para los archivos de configuración. El formato del archivo es importante, incluidas las sangrías y los guiones. Las plantillas de CloudFormation también se pueden escribir en JSON.

## Se configuran los recursos siguientes:
## Parámetros

    • VPC Rango CIDR 
    • Opción de Zona de Disponibilidad
    • Opciones Subnet CIDR
    • Nombre de Instancia
    • Tipo de Instancia- Forzado a t3.micro
    • Nombre clave/KeyName (default del laboratorio)

## Recursos

    • VPC
    • Internet Gateway
    • Rutas y tabla de enrutamiento para el tráfico de Internet.
    • Subnet [Publica]
    • Grupo de seguridad para permitir el tráfico de Internet.

## 🌐Acceder al WebServer

- Abra la URL pública de la instancia ec2 en una navegador para acceder al sitio de prueba.

# Listado de Archivos:
- Plantilla CloudFormation [template1.yaml](https://github.com/Gloria-Nabor/aws-restart-final-project/blob/ca1795436d1b1cc3822408d63c3a46546ed8c371/template1.yaml)
   
- Diseño de Pila CloudFormation [template1-designer.png](https://github.com/Gloria-Nabor/aws-restart-final-project/blob/ca1795436d1b1cc3822408d63c3a46546ed8c371/template1-designer.png)
   
- Diagrama de Arquitectura [aws-architecture-diagram](https://github.com/Gloria-Nabor/aws-restart-final-project/assets/114413852/2deefd25-cc27-40a6-8a18-e9e91d7319db)

- Guía de automatización con Cloud Formation [aws-cloudformation-user-guide.md](https://github.com/Gloria-Nabor/aws-restart-final-project/blob/ca1795436d1b1cc3822408d63c3a46546ed8c371/aws-cloudformation-user-guide.md)

## Información adicional:

En la lista de recursos del template se incluye un Bucket S3 (Simple Storage Service). 
CloudFormation asignará un nombre aleatorio para evitar conflictos con buckets existentes.

**Algunos usos de Amazon S3:**

- En el desarrollo de nuevas funciones y siguiendo un enfoque de "infraestructura como código", es una buena práctica almacenar las plantillas en un Bucket S3 para facilitar el versionamiento de la pila en CloudFormation y controlar el acceso.

- En el caso de optar por mantener el sitio web estático, un Bucket S3 puede alojar el archivo index.html y demás contenido, permitiendo el acceso mediante la URL asignada por Amazon S3.

*Consulte dentro del contenido del curso de AWS re/star:*

**Laboratorios:**

    • 191- Actividad de Café: Resolución de problemas en las implementaciones de AWS CloudFormation. (Duración: 75 minutos) 
    • 192- [JAWS] - Lab - [Reto] CloudFormation: Desafío usando AWS CloudFormation para crear una AWS VPC y una instancia de Amazon EC2.
    • Actividad: Crear un sitio web en S3. (Duración: 45 minutos)
 
*Utilice las páginas de documentación a modo de ayuda: [Fragmentos de plantillas de Amazon S3](https://docs.aws.amazon.com/es_es/AWSCloudFormation/latest/UserGuide/quickref-s3.html) y [AWS::EC2::Instance](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-ec2-instance.html)*.

*Amplie sus conocimientos y aprenda más de los beneficios de AWS en [Training and Certification](https://aws.amazon.com/training/).* 

<hr>

## Equipo 👨‍💻👩‍💻: 

| <img src="https://i.imgur.com/Cbmeoax.png" width=50> | <img src="https://i.imgur.com/7c1XLaf.jpg" width=50> | <img src="https://imgur.com/K5oBokB.png" width=50> |<img src="https://i.imgur.com/.jpg" width=50> | <img src="https://i.imgur.com/HK9Axa5.png" width=50> 
|:-:|:-:|:-:|:-:|:-:|
| **Brenda Díaz** | **Gloria Nabor** | **Miriam Almanza** | **Moisés Solorio** | **Nancy Contreras** | 
| <a href="https://github.com/brendadiaz2410"><img src="https://img.shields.io/badge/github-%23121011.svg?&style=for-the-badge&logo=github&logoColor=white"/></a> <a href="https://www.linkedin.com/in/brenda-yareli-d%C3%ADaz-ruiz-038895246/"><img src="https://img.shields.io/badge/linkedin%20-%230077B5.svg?&style=for-the-badge&logo=linkedin&logoColor=white"/></a> | <a href="https://github.com/Gloria-Nabor"><img src="https://img.shields.io/badge/github-%23121011.svg?&style=for-the-badge&logo=github&logoColor=white"/></a> <a href="https://www.linkedin.com/in/gloria-nabor/"><img src="https://img.shields.io/badge/linkedin%20-%230077B5.svg?&style=for-the-badge&logo=linkedin&logoColor=white"/></a> | <a href="https://github.com/miriamalmanza"><img src="https://img.shields.io/badge/github-%23121011.svg?&style=for-the-badge&logo=github&logoColor=white"/></a> <a href="https://www.linkedin.com/in/miriam-almanza-de-la-fuente/"><img src="https://img.shields.io/badge/linkedin%20-%230077B5.svg?&style=for-the-badge&logo=linkedin&logoColor=white"/></a> | <a href="https://github.com/"><img src="https://img.shields.io/badge/github-%23121011.svg?&style=for-the-badge&logo=github&logoColor=white"/></a> <a href="https://www.linkedin.com/in//"><img src="https://img.shields.io/badge/linkedin%20-%230077B5.svg?&style=for-the-badge&logo=linkedin&logoColor=white"/></a> |<a href="https://github.com/nancydata"><img src="https://img.shields.io/badge/github-%23121011.svg?&style=for-the-badge&logo=github&logoColor=white"/></a>  <a href="https://www.linkedin.com/in/nancybellmx/"><img src="https://img.shields.io/badge/linkedin%20-%230077B5.svg?&style=for-the-badge&logo=linkedin&logoColor=white"/></a>

<hr>

# Guía: automatización con CloudFormation

Esta guia le ayudará a implementar un pila de CloudFormation al definir los recursos dentro de una plantilla.

## Objetivo
  • Implementar una pila de AWS CloudFormation con una nube privada virtual (VPC), un grupo de seguridad y una Amazon Elastic Compute Cloud (EC2) definidos, como se muestra en este diagrama:
      
## Duración
  • El tiempo estimado para completar esta práctica es de 30 minutos.

## Acceder a la AWS Management Console

**• Opción 1**: Usuarios de AWS

Inicie sesión con su cuenta de AWS [aquí](https://signin.aws.amazon.com), debe elegir su tipo de usuario, si es [usuario raíz](https://docs.aws.amazon.com/es_es/signin/latest/userguide/introduction-to-root-user-sign-in-tutorial.html), capture el correo electrónico y la contraseña, o si es un [usuario de IAM](https://docs.aws.amazon.com/es_es/signin/latest/userguide/introduction-to-iam-user-sign-in-tutorial.html), ingrese ID o alias, nombre de usuario de IAM y contraseña.

Haga clic [aquí](#tarea-implementar-una-pila-de-aws-cloudformation) para pasar a la siguiente tarea.

**• Opción 2:** Estudiantes de  AWS re/start

Ingrese a la cuenta de entrenamiento del curso de AWS re/start y localice el laboratorio siguiente:

            • 190- [JAWS] - Lab - Automatización de implementaciones con AWS CloudFormation.

1. En la parte superior de las instrucciones, haga clic en `Start Lab` (Iniciar laboratorio) para lanzar el laboratorio.
   
    Se abrirá el panel Start Lab (Iniciar laboratorio), donde se muestra el estado del laboratorio.

2. Espere hasta que aparezca el mensaje **“Lab status: ready”** (Estado del laboratorio: listo) y, a continuación, haga clic en la **X** para cerrar el panel Start Lab (Iniciar laboratorio).

3. En la parte superior de estas instrucciones, haga clic en `AWS`.
   
    La **AWS Management Console** se abrirá en una pestaña nueva del navegador. El sistema iniciará sesión de forma automática.

    **Sugerencia**: Si no se abre una pestaña nueva del navegador, debería aparecer un anuncio o un ícono en la parte superior de éste en el que se indique que el navegador no permite que se abran ventanas emergentes en el sitio. Haga clic en el anuncio o en el ícono y seleccione “Allow pop ups” (Permitir ventanas emergentes).

4. Acomode la pestaña de la AWS Management Console para que aparezca al lado de estas instrucciones. Idealmente, debería poder ver ambas pestañas del navegador a la vez para que sea más sencillo seguir los pasos de esta guía.

    *No cambie de región durante este laboratorio.*

## Tarea: Implementar una pila de AWS CloudFormation

Se implementará una pila de CloudFormation que creará una VPC, un grupo de seguridad, y una instancia EC2.

5. Haga clic derecho en este enlace y descargue la plantilla de CloudFormation: template1.yaml

6. A  modo informativo, puede abrir este archivo en un editor de texto (no en un procesador de textos).
    La plantilla está escrita en un formato llamado [YAML](https://en.wikipedia.org/wiki/YAML), que se utiliza habitualmente para los archivos de configuración. El formato del archivo es importante, incluidos los guiones y las sangrías (dos espacios para cada sangría).

    Al revisar el archivo, observará las secciones siguientes:
   
   - La sección **[Parameters](https://docs.aws.amazon.com/es_es/AWSCloudFormation/latest/UserGuide/parameters-section-structure.html)** (Parámetros) se utiliza para solicitar entradas que puedan emplearse en otras partes de la plantilla. La plantilla pide dos rangos de direcciones IP (CIDR) para definir la VPC. 
           
   - La sección **[Resources](https://docs.aws.amazon.com/es_es/AWSCloudFormation/latest/UserGuide/resources-section-structure.html)** (Recursos) se utiliza para definir la infraestructura que se va a implementar. La plantilla está definiendo la VPC y un grupo de seguridad.
       
   Cuando se crean plantillas de CloudFormation, se puede hacer referencia a otros recursos en la plantilla utilizando la palabra clave *!Ref*. Por ejemplo, en  la plantilla **template1.yaml**, hay una parte que define una VPC y luego *!Ref VPC* se utiliza para referirse al recurso VPC dentro de la definición de la tabla de enrutamiento:

    
          VPC:    
            Type: AWS::EC2::VPC
            Properties: 
              CidrBlock: 10.0.0.0/16
        
          PublicRouteTable:
            Type: AWS::EC2::RouteTable        
            Properties:
              VpcId: !Ref VPC
    
   La definición de una instancia de **Amazon EC2** es compleja porque requiere utilizar recursos asociados, como una AMI, un grupo de seguridad y una subred. A continuación se detallan sus **propiedades**:
   
   ▪ **ImageId:**

           AmazonLinuxAMIID:
             Type: AWS::SSM::Parameter::Value<AWS::EC2::Image::Id>
             Default: /aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2
                
   ▪ I**nstanceType:** t3.micro
        
   ▪ **SecurityGroupIds:**
   
           SecurityGroupIds:
             - !Ref WebSecurityGroup
            
   ▪ **SubnetId:**  PublicSubnet
            
   ▪ **Etiquetas:** utilice el siguiente bloque YAML

            Tags:
 			       - Key: Name
 			         Value: App Server
             
   - La sección **[Outputs](https://docs.aws.amazon.com/es_es/AWSCloudFormation/latest/UserGuide/outputs-section-structure.html)** (Resultados) se utiliza para proporcionar información selectiva sobre los recursos de la pila. La plantilla proporciona el grupo de seguridad predeterminado para la VPC que se crea.
      
       Ahora utilizará esta **plantilla** para lanzar una **pila de CloudFormation**.

       
7. En AWS Management Console, en el menú **Services** (Servicios), haga clic en **CloudFormation**.
  
8. Haga clic en `Create stack` (Crear pila) y a continuación haga lo siguiente:
   
   - Haga clic en **Upload a template file** (Cargar un archivo de plantilla).
   
   - Haga clic en **Browse** (Examinar) o **Choose file** (Elegir archivo) y cargue el archivo de la plantilla que descargó anteriormente.
   
   - Haga clic en `Next` (Siguiente).
   
9. En la página Specify **Details** (Especificar detalles), realice las siguientes configuraciones:
   - En **Stack name** (Nombre de la pila), ingrese `Lab`.
     
     En la sección **Parameters** (Parámetros), verá que CloudFormation le solicita el rango de direcciones IP (CIDR) de la VPC y la subred. La plantilla ha especificado un valor predeterminado, por lo que no es necesario modificar estos valores.
   
10. Haga clic en `Next` (Siguiente).
    
       La página **Options** (Opciones) puede utilizarse para especificar parámetros adicionales. Puede examinar la página, pero asegúrese de dejar las configuraciones en sus valores predeterminados.
    
11. Haga clic en `Next` (Siguiente).
    
       La página **Review** (Revisar) muestra un resumen de todos las configuraciones. Algunos de los recursos se definen con nombres personalizados, lo que puede dar lugar a conflictos de denominación. Por lo tanto, CloudFormation solicita un reconocimiento de que se están utilizando nombres personalizados.
    
12. Haga clic en `Create stack` (Crear pila).
    
       La pila entrará ahora en el estado ***CREATE_IN_PROGRESS***.
        
14. Haga clic en la pestaña **Events** (Eventos) y desplácese por el listado.
    
       El listado muestra (en orden inverso) las actividades realizadas por CloudFormation, como la de comenzar a crear un recurso y la de completar su creación. Cualquier error encontrado durante la creación de la pila se listará en esta pestaña.
    
15. Haga clic en la pestaña **Resources** (Recursos).
    
       El listado muestra los recursos que se están creando. CloudFormation determina el orden óptimo de creación de los recursos, como crear la VPC antes que la subred.
    
16. Espere hasta que el estado cambie a ***CREATE_COMPLETE***. Puede hacer clic en **⟳ Refresh** (Actualizar) de vez en cuando para actualizar la pantalla.

## Implementación terminada

¡Felicitaciones! Ha completado la implementación de recursos a través de CloudFormation.

# Tareas opcionales:

## Verificar los recursos creados
           
  - Diríjase a la consola de la **VPC** para ver el recurso *Lab VPC* que se creó.
       
  - Ingrese a la consola de **EC2** para examinar la instancia *App Server*.
       
  - Verifique el bucket creado en **S3**.

## Eliminar la pila

Cuando se elimina una pila de CloudFormation, este eliminará automáticamente los recursos que creó.
       
  - A continuación, vuelva a la consola de CloudFormation. Ahora procederá a eliminar la pila.
    
    - En la consola de CloudFormation, seleccione ☑*Lab* (Laboratorio).
   
    - Haga clic en **Delete** (Eliminar) y luego, cuando se le solicite, haga clic en `Delete stack` (Eliminar pila).
   
      La pila mostrará ***DELETE_IN_PROGRESS***. Luego de unos minutos, la pila desaparecerá.
       
## Verificar recursos eliminados

  - Compruebe que el S3 bucket de Amazon, la instancia de Amazon EC2 y la VPC se hayan eliminado.

# ¿Qué es Amazon S3?

Amazon Simple Storage Service (Amazon S3) es un servicio de almacenamiento de objetos que ofrece escalabilidad, disponibilidad de datos, seguridad y rendimiento líderes del sector. 
Los clientes de todos los tamaños y sectores pueden utilizar Amazon S3 para almacenar y proteger cualquier cantidad de datos para diversos casos de uso, tales como lagos de datos, sitios web, 
aplicaciones móviles, copia de seguridad y restauración, archivado, aplicaciones empresariales, dispositivos IoT y análisis de big data. Amazon S3 proporciona funciones de gestión para que pueda optimizar, 
organizar y configurar el acceso a sus datos para satisfacer sus requisitos empresariales, organizativos y de conformidad específicos.

# Actividad: Crear un sitio web en S3
Información general sobre la actividad del café: crear un sitio web en S3

En esta actividad, practicará el uso de la AWS Command Line Interface (AWS CLI) para:

  Crear un bucket de Amazon Simple Storage Service (Amazon S3).
  Crear un nuevo usuario de AWS Identity and Access Management (IAM) que tenga acceso total a Amazon S3.
  Cargar archivos a Amazon S3 a fin de alojar un sitio web simple para la cafetería y panadería.
  Crear un archivo por lotes que se pueda utilizar para actualizar el sitio web estático cuando cambie cualquier archivo del sitio web de manera local.

Una vez que haya completado la actividad, los clientes podrán acceder al sitio web que ha implementado en Amazon S3, como se muestra en este diagrama.

![image3](https://github.com/Gloria-Nabor/aws-restart-final-project/assets/114413852/63f3c248-c4b8-48af-aedf-2ed1228a8b9f)


Con el objetivo de asegurar que todos los estudiantes tengan la misma configuración, practicarán cómo utilizar la AWS CLI desde una instancia de Amazon Elastic Compute Cloud (Amazon EC2). En esta actividad, recibirá una instancia de Amazon Linux que tiene la AWS CLI preinstalada. Debe establecer una conexión Secure Shell (SSH) para la instancia.

 
Objetivos de la actividad

Después de completar esta actividad, podrá realizar lo siguiente:

    Ejecutar comandos de la AWS CLI que utilizan los servicios de IAM y Amazon S3.
    Implementar un sitio web estático en un bucket de S3.
    Crear un script que utilice la AWS CLI para copiar archivos de un directorio local en Amazon S3.

 
Relevancia del caso empresarial

Una solicitud empresarial de la cafetería: lanzar un sitio web

![image001](https://github.com/Gloria-Nabor/aws-restart-final-project/assets/114413852/ef05f717-8241-4705-a15c-df630a34ad2b)

Sofia le mencionó a Nikhil que le gustaría que la cafetería tenga un sitio web para mostrar la cafetería de manera virtual mediante imágenes y que proporcione a los clientes detalles del negocio, como la ubicación de la tienda, los horarios de atención y el número de teléfono.

A Nikhil le complace estar a cargo de crear el primer sitio web para la cafetería.

Durante esta actividad, tomará el rol de Nikhil y trabajará para producir los resultados que todos en la cafetería esperan. Incluso quizá pueda superar las expectativas.

 
Pasos de la actividad

Duración: el tiempo estimado para completar esta actividad es de 45 minutos.

 
Acceso a AWS Management Console

    En la parte superior de estas instrucciones, haga clic en Start Lab (Comenzar laboratorio) para comenzar el laboratorio.

    Se abrirá el panel Start Lab (Comenzar laboratorio), donde se muestra el estado del laboratorio.

    Espere hasta que aparezca el mensaje “Lab status: ready” (Estado del laboratorio: listo) y, a continuación, haga clic en la X para cerrar el panel Start Lab (Comenzar laboratorio).

    En la parte superior de estas instrucciones, haga clic en AWS.

    AWS Management Console se abrirá en una pestaña nueva del navegador. El sistema iniciará sesión de forma automática.

    Sugerencia: Si no se abre una pestaña nueva del navegador, debería aparecer un anuncio o un ícono en la parte superior de este en el que se indica que el navegador no permite que el sitio abra ventanas emergentes. Haga clic en el anuncio o en el ícono y elija “Allow pop ups” (Permitir ventanas emergentes).

    Ordene la pestaña de AWS Management Console para que aparezca al lado de estas instrucciones. Idealmente, debería poder ver ambas pestañas del navegador a la vez para que sea más sencillo seguir los pasos del laboratorio.

 
Tarea 1: Conectarse a una instancia EC2 de Amazon Linux mediante la utilización de SSH.

En esta tarea se conectará con una instancia EC2 de Amazon Linux existente que ya tenga instalada la AWS CLI.

Los usuarios de Windows deberán seguir los pasos de la tarea 1.1. Los usuarios de macOS y Linux deberán seguir la tarea 1.2.

Para usuarios de macOS o Linux: haga clic aquí a fin de obtener las instrucciones de inicio de sesión

 
Tarea 1.1: SSH de Windows
Usuarios de Windows: uso de SSH para conectarse

 Estas instrucciones están dirigidas únicamente a los usuarios de Windows.

Si utiliza macOS o Linux, pase a la siguiente sección.

    Lea los tres puntos de este paso antes de comenzar, ya que no podrá consultar estas instrucciones cuando el panel Details (Detalles) se encuentre abierto.
    Haga clic en el menú desplegable Details (Detalles) encima de estas instrucciones y luego haga clic en Show (Mostrar). Se abrirá la ventana Credentials (Credenciales).
    Haga clic en Download PPK (Descargar PPK) y guarde el archivo labsuser.ppk. Por lo general, el navegador lo guarda en el directorio Downloads (Descargas).
    A continuación, haga clic en la X para salir del panel Details (Detalles).

    Descargue el software necesario.
        Utilizará PuTTY para conectarse mediante SSH a las instancias de Amazon EC2. Si no tiene PuTTY instalado en su computadora, descárguelo [aquí](https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe).

    Abra putty.exe.

    Configure PuTTY sin tiempo de espera de la siguiente manera:
        Haga clic en Connection (Conexión).
        Establezca Seconds between keepalives (Segundos entre keepalives) en 30.

    Esto le permite mantener la sesión de PuTTY abierta durante un periodo más prolongado.

    Configure la sesión de PuTTY de la siguiente manera:
        Haga clic en Session (Sesión).
        Host Name (or IP address) (Nombre del host [o dirección IP]): Copie y pegue el valor de IPv4 Public IP address (Dirección IP pública IPv4) para la instancia. Para obtenerla, vuelva a la consola de EC2 y haga clic en Instances (Instancias). Marque la casilla junto a la instancia a la que desea conectarse y en la pestaña Description (Descripción) copie el valor de IPv4 Public IP (Dirección IP pública IPv4).
        Nuevamente en PuTTY, en la lista de Connection (Conexión), expanda  SSH.
        Haga clic en Auth (Autenticación) (no lo expanda).
        Haga clic en Browse (Explorar).
        Busque y seleccione el archivo lab#.ppk que descargó.
        Haga clic en Open (Abrir) para seleccionarlo.
        Haga clic en Open (Abrir).

    Haga clic en Yes (Sí) para validar el host y conectarse a él.

    Cuando aparezca login as (iniciar sesión como), ingrese: ec2-user.

Esto lo conectará a la instancia EC2.

    Usuarios de Windows: haga clic aquí para pasar a la siguiente tarea.

 

Tarea 1.2: SSH de macOS o Linux

Estas instrucciones están dirigidas únicamente a los usuarios de Mac o Linux. Si es usuario de Windows, pase a la siguiente tarea.

    Lea los tres puntos de este paso antes de comenzar, ya que no podrá consultar estas instrucciones cuando el panel Details (Detalles) se encuentre abierto.

    Haga clic en el menú desplegable Details (Detalles) encima de estas instrucciones y luego haga clic en Show (Mostrar). Se abrirá la ventana Credentials (Credenciales).
    Haga clic en el botón Download PEM (Descargar PEM) y guarde el archivo labsuser.pem.
    A continuación, haga clic en la X para salir del panel Details (Detalles).

    Abra una ventana de terminal y cambie el directorio cd para ir al directorio donde se descargó el archivo labsuser.pem.

Por ejemplo, ejecute este comando si el archivo se guardó en el directorio Downloads (Descargas):

```plain

cd ~/Downloads

```

    Ejecute este comando para cambiar los permisos de la clave a fin de que sean de solo lectura:

    chmod 400 labsuser.pem

    Vuelva a la AWS Management Console y, en el servicio EC2, haga clic en Instances (Instancias). Marque la casilla situada junto a la instancia a la que desea conectarse.

    En la pestaña Description (Descripción), copie el valor de IPv4 Public IP (IP pública IPv4).

    Vuelva a la ventana de terminal y ejecute este comando (sustituya <public-ip> por la dirección IP pública real que haya copiado):

    ssh -i labsuser.pem ec2-user@<public-ip>

    Escriba yes cuando se le pregunte si desea permitir una primera conexión a este servidor remoto SSH.

Como utiliza un par de claves para la autenticación, no se le pedirá una contraseña.

 
Tarea 2: Configurar la AWS CLI

NOTA: A diferencia de otras distribuciones de Linux que se encuentran disponibles a través de Amazon Web Services (AWS), las instancias de Amazon Linux ya vienen con la AWS CLI preinstalada.

    Actualice el software de la AWS CLI con las credenciales.

    aws configure

    Cuando se le solicite, ingrese la siguiente información:
        AWS Access Key ID (ID de clave de acceso de AWS): haga clic en el menú desplegable Details (Detalles), que se encuentra encima de estas instrucciones, y luego haga clic en Show (Mostrar). Copie el valor AccessKey (Clave de acceso) y péguelo en la ventana de terminal.
        AWS Secret Access Key (Clave de acceso secreta de AWS): copie y pegue el valor de SecretKey (Clave secreta) de la misma pantalla de Credentials (Credenciales).
        Default region name (Nombre predeterminado de la región): us-west-2
        Default output format (Formato de salida predeterminado): json

 
Tarea 3: Crear un bucket de S3 mediante la utilización de la AWS CLI

    Abra [la documentación de la AWS CLI para S3api](https://docs.aws.amazon.com/cli/latest/reference/s3api/).

    Sugerencia: En esta actividad, utilizará en ocasiones el comando s3api y en otras el comando s3. Los comandos s3 se crean  partir de operaciones que se encuentran en los comandos s3api.

    Utilice el comando aws s3api create-bucket para crear un bucket en Amazon S3. El bucket debe tener un nombre único, como la combinación de su primera inicial, apellido y tres números aleatorios. Por ejemplo, jsmith256 sería un buen nombre de bucket si su nombre es Jane Smith.

    Especifique --region us-west-2 porque quiere alojar el sitio web en la región de AWS que se encuentra más cerca de las personas más propensas a acceder a él (en el área de Londres).
    Debe agregar --create-bucket-configuration LocationConstraint=us-west-2 al final del comando.

Si el comando es exitoso, recibirá una respuesta con formato JavaScript Object Notation (JSON) con un par de nombre-valor Location, donde el valor refleja el nombre del bucket.

 
Tarea 4: Crear un usuario de IAM nuevo que tenga acceso completo al servicio Amazon S3

    Con la AWS CLI, cree un usuario de IAM nuevo con el nombre: awsS3user

    Sugerencia: Utilice la documentación de AWS CLI, según sea necesario, para descifrar qué comando debe ejecutar. Al igual que el comando anterior que ejecutó, recibirá una respuesta con formato JSON si el comando es exitoso.

    Cree un perfil de inicio de sesión para el usuario nuevo mediante el siguiente comando:

          aws iam create-login-profile --user-name awsS3user --password Training123!

    Copie a AWS el número de cuenta. Para ello:
        En la AWS Management Console que abrió antes en esta actividad, haga clic en el menú desplegable voclabs/user… en la esquina superior derecha de la pantalla.
        Copie el número de cuenta que aparece. Será un número de 12 dígitos con guiones.
        Todavía en el menú desplegable, seleccione Sign Out (Cerrar sesión).

    Inicie sesión en la AWS Management Console como el nuevo usuario awsS3user. Para ello:
        En la pestaña del navegador donde acaba de cerrar sesión de la AWS Management Console, haga clic en el botón Sign in to the Console (Iniciar sesión en la consola). Nota: Debido a cambios en la consola, podría ver Log back in (Volver a iniciar sesión) como una opción.
        Se le redirigirá a una pantalla de inicio de sesión.
        Seleccione IAM user (Usuario de IAM).
        En el campo de texto, ingrese awsS3user.
        Haga clic en Next (Siguiente).
        Debería ver una nueva pantalla de inicio de sesión con un campo Account ID or alias (ID de cuenta o alias). El campo ya debería mostrar el número de cuenta. Si no muestra el número de cuenta, pegue el número de cuenta que copió hace unos instantes (pero elimine los guiones luego de pegarlo).
        Haga clic en Next (Siguiente).
        Para IAM user name (Nombre de usuario de IAM), ingrese awsS3user.
        En Password (Contraseña), ingrese Training123!.
        Haga clic en Sign In (Iniciar sesión).

    En la consola, diríjase al menú Services (Servicios) y elija S3.

La página de servicio de Amazon S3 mostrará un mensaje de error que dice Access denied (Acceso denegado). Esta conducta es esperable debido a que el usuario nuevo no ha recibido ningún derecho. Deje esta página abierta porque volverá a ella pronto.

    De vuelta en la ventana de terminal, busque la política administrada por AWS que otorga acceso completo a Amazon S3. Ejecute este comando para encontrarla:

    aws iam list-policies --query "Policies[?contains(PolicyName,'S3')]"

El conjunto de resultados muestra políticas que tienen un atributo PolicyName que contienen el término S3 en algún momento. Busque la que otorga acceso completo a Amazon S3. La utilizará en el paso siguiente.

    Otórguele acceso completo a awsS3user al bucket de S3 mediante el siguiente comando:

    aws iam attach-user-policy --policy-arn     arn:aws:iam::aws:policy/<policyYouFound> --user-name awsS3user

Reemplace <policyYouFound> en el comando anterior con el valor PolicyName de la política apropiada que encontró al utilizar el comando del paso anterior.

    Regrese a AWS Management Console y actualice la pestaña del navegador.

    El error Access denied (Acceso denegado) debería desaparecer y debería ver el bucket que creó al utilizar la AWS CLI antes en esta actividad.

 
Tarea 5: Extraer los archivos que necesita para esta actividad

    De vuelta en la terminal de SSH, extraiga los archivos que necesita para esta actividad ejecutando los siguientes comandos:

    cd ~/sysops-activity-files

    tar xvzf static-website-v2.tar.gz

    cd static-website

    Ejecute el comando ls para confirmar que los archivos se extrajeron correctamente. Debería ver un archivo index.html y los directorios con los nombres css e images.

    Elimine el archivo tar.gz. Utilice el comando rm de Linux pero deje los archivos extraídos.

 
Tarea 6: Cargar los archivos a Amazon S3 mediante la AWS CLI

    Ejecute el siguiente comando para preparar el bucket que creó antes a fin de que funcione como un sitio web. El proceso asegurará que index.html se comprenda como el documento de índice.

    NOTA: Asegúrese de reemplazar <my-bucket> en el comando debajo con el nombre de su bucket.

    aws s3 website s3://<my-bucket>/ --index-document index.html

    Cargue los archivos en el bucket. Reemplace <my-bucket> con el nombre de su bucket real.

    aws s3 cp /home/ec2-user/sysops-activity-files/static-website/ s3://<my-    bucket>/ --recursive --acl public-read

    Note que el comando de carga incluye un parámetro de lista de control de acceso (ACL) que especifica que el archivo cargado se debe encontrar disponible para que el público lo lea. También incluye el parámetro recursive, que indica que se deben cargar todos los archivos en el directorio actual de su máquina.

    Verifique que se hayan cargado (de nuevo, reemplace <my-bucket> con el nombre de su bucket):

    aws s3 ls <my-bucket>

    De nuevo en la ventana del navegador de AWS Management Console, en el área de servicio de S3, haga clic en el nombre de su bucket.

    Haga clic en la pestaña Properties (Propiedades). En el área Static website hosting (Alojamiento de sitios web estáticos), note que se habilitó Bucket hosting (Alojamiento de buckets) como consecuencia de ejecutar el comando de AWS CLI aws s3 website.

    Haga clic en el enlace Bucket hosting (Alojamiento de buckets) y luego haga clic en la URL de Endpoint (Punto de enlace) que se muestra.

¡Felicitaciones, ha creado un sitio web estático que se encuentra disponible para que el público pueda visitarlo!

 
Una solicitud empresarial de la cafetería: lanzar un sitio web

![Coffee-Shop](https://github.com/Gloria-Nabor/aws-restart-final-project/assets/114413852/e0877f7d-d099-4e79-9d22-e744923ab67f)

Nikhil le mostró a Sofia el nuevo sitio web estático y ella quedó impresionada. Siéntase orgulloso, ¡buen trabajo!

Martha y Frank también estaban impresionados. Sin embargo, no pasó mucho tiempo para que empezaran a pedir cambios. Martha solicitó un cambio en el color del fondo que aparece detrás de las galletas, el café y las tartas en la segunda fila de fotos. Sofía, al darse cuenta de que podría ser solo el primero de muchos cambios, decide usar sus habilidades de programación para transformar la actualización del sitio web en un proceso por lotes. En esta última parte de la actividad, usted asume el rol de Sofía y trabaja en introducir la automatización en el proceso de actualización del sitio web.

 
Tarea 7: Crear un archivo por lotes para actualizar el sitio web de manera sencilla

    En la ventana de terminal, busque el historial de comandos recientes mediante el siguiente comando:

    history

    Ubique la línea donde ejecutó el comando aws s3 cp. Pronto colocará esta línea en su nuevo archivo por lotes.

    Para cambiar los directorios y crear un archivo vacío, ejecute los siguientes comandos en la sesión de terminal de SSH:

    cd ~

    touch update-website.sh

    Abra el archivo vacío en el editor VI.

    vi update-website.sh

    Para ingresar el modo de edición en VI, presione A.

    Agregue la primera línea estándar y luego agregue la línea s3 cp de su historial (reemplace <my-bucket> con el nombre real de su bucket):

    #!/bin/bash

    aws s3 cp /home/ec2-user/sysops-activity-files/static-website/ s3://<my-    bucket>/ --recursive --acl public-read

    Escriba los cambios y salga del archivo presionando ESC; luego escriba :wq y presione ENTER (Intro).

    Conviértalo en un archivo por lotes ejecutable.

    chmod +x update-website.sh

    Abra la copia local del archivo index.html en un editor de textos.

    vi sysops-activity-files/static-website/index.html

    Modifique el archivo como se describe:
        Ubique la primera línea que tiene el código HTML bgcolor="aquamarine" y cámbielo a bgcolor="gainsboro".
        Ubique la línea que tiene el código HTML bgcolor="orange" y cámbielo a bgcolor="cornsilk".
        Ubique la segunda línea que tiene el código HTML bgcolor="aquamarine" y cámbielo a bgcolor="gainsboro".
        Guarde los cambios.

    Ejecute su archivo por lotes para actualizar el sitio web.

    ./update-website.sh

NOTA: El resultado de la línea de comandos debe mostrar que los archivos se copiaron a Amazon S3.

    Vuelva al navegador y actualice la página de la cafetería para ver los cambios en el sitio web.

Felicitaciones, acaba de realizar su primera corrección del sitio web.

Ahora también tiene una herramienta (el script que creó) que le facilita ingresar los cambios de los archivos fuente de su sitio web en Amazon S3.

 
Desafío opcional

¿Notó que su archivo por lotes carga cada archivo a Amazon S3 cada vez que lo ejecuta, incluso cuando la mayoría de los archivos no tienen cambios?

- Consulte la <a href="https://docs.aws.amazon.com/cli/latest/reference/s3/sync.html" target="_blank">documentación de referencia de la AWS CLI sobre sincronización</a> y vea si puede reemplazar la línea `aws s3 cp` en su archivo con una línea `aws s3 sync`.


- Para ponerlo a prueba, realice un cambio pequeño en el archivo index.html. Por ejemplo, modifique uno de los colores de nuevo y guarde el cambio. Luego, ejecute su archivo por lotes actualizado. ¿El script se volvió más eficiente?

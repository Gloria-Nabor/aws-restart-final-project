## PASOS PARA CREAR UN GRUPO DE SEGURIDAD: 

1.-En la AWS Management Console, seleccione el menú **Services** (Servicios) y, luego, seleccione **VPC**.

2.-En el panel de navegación, elija **Security Groups**(Grupos de seguridad).

3.-Elija **Create Security Group**(Crear grupo de seguridad).

4.-Configure el grupo de seguridad con las siguientes opciones:

Security group name (Nombre del grupo de seguridad)

Description (Descripción)

VPC: elija la VPC


# Para añadir una regla de entrada a un grupo de seguridad.
5.-Elija **Edit inbound rules** (Editar reglas de entrada).

6.-Para cada regla, elija **Add Rule** (Agregar regla) y realice lo siguiente.

En **Type** (Tipo), elija el tipo de protocolo que desea permitir.
Para TCP o UDP personalizados, debe ingresar el rango de puertos que va a permitir.

7.-Para **Source** (Fuente), realice una de las siguientes acciones para permitir el tráfico.

Elija **Custom** (Personalizado) y, a continuación, ingrese una dirección IP en notación CIDR, un bloque de CIDR, otro grupo de seguridad o una lista de prefijos.

Elija **Anywhere** (En cualquier lugar) para permitir que todo el tráfico del protocolo especificado llegue a su instancia. 





8.-Elija **create security group**

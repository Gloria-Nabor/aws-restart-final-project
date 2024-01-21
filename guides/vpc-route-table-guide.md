## PASOS PARA CREAR UNA TABLA DE ENRUTAMIENTO:

Una tabla de enrutamiento contiene una serie de reglas, llamadas rutas, que se usan para determinar hacia dónde se dirige el tráfico de red. Cada subred de una VPC debe estar asociada a una tabla de enrutamiento, que es la que controla el enrutamiento de la subred.

1.-En la *AWS Management Console*, seleccione el menú **Services** (Servicios) y, luego, seleccione **VPC**.

2.-En el panel de navegación izquierdo, haga clic en **Route Tables** (Tablas de enrutamiento).

3.-Elija **Create Route Table** (Crear tabla de enrutamiento).




4.-En **Name** (Etiqueta), escriba el nombre de la tabla de enrutamiento.

5.-En **VPC**, elija su VPC.

6.-(Opcional) Para agregar una etiqueta, elija **Add new tag** (Agregar etiqueta nueva) e ingrese la clave y el valor de la etiqueta.

7.-Elija **Create Route Table** (Crear tabla de enrutamiento).




# Para actualizar las rutas de una tabla de enrutamiento mediante la consola

Abra la consola de Amazon VPC

1.-En el panel de navegación, elija **Route tables** (Tablas de enrutamiento) y, a continuación, seleccione la tabla de enrutamiento.

2.-Elija **Actions** (Acciones), **Edit routes** (Editar rutas).

3.-Para agregar una ruta, elija **Add route** (Añadir ruta). En **Destination** (Destino) introduzca el bloque de CIDR de destino, una única dirección IP o el ID de una lista de prefijos.

4.-Para modificar una ruta, para **Destination** (Destino), sustituya el bloque de CIDR de destino o la dirección IP única. En **Target** (Objetivo), elija un objetivo.

5.-Para eliminar una ruta, elija **Remove** (Eliminar).

6.-Elija **Guardar** cambios.








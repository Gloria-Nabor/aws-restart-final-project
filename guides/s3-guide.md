# ¿Qué es Amazon S3?

Amazon Simple Storage Service (Amazon S3) es un servicio de almacenamiento de objetos que ofrece escalabilidad, disponibilidad de datos, seguridad y rendimiento líderes del sector. 
Los clientes de todos los tamaños y sectores pueden utilizar Amazon S3 para almacenar y proteger cualquier cantidad de datos para diversos casos de uso, tales como lagos de datos, sitios web, 
aplicaciones móviles, copia de seguridad y restauración, archivado, aplicaciones empresariales, dispositivos IoT y análisis de big data. Amazon S3 proporciona funciones de gestión para que pueda optimizar, 
organizar y configurar el acceso a sus datos para satisfacer sus requisitos empresariales, organizativos y de conformidad específicos.

# Clases de almacenamiento
Amazon S3 ofrece varios tipos de almacenamiento diseñados para distintos casos de uso. Por ejemplo, puede almacenar datos de producción críticos en S3 Standard o S3 Express One Zone para obtener acceso frecuente, 
ahorrar costes al almacenar datos a los que se accede con poca frecuencia en S3 Standard-IA o S3 One Zone-IA, y archivar datos con los costos más bajos en S3 Glacier Instant Retrieval, S3 Glacier Flexible Retrieval
y S3 Glacier Deep Archive.

## Administrar el almacenamiento

Amazon S3 cuenta con funciones de gestión del almacenamiento que puede utilizar para gestionar los costes, cumplir los requisitos normativos, reducir la latencia y guardar varias copias distintas de sus datos 
para cumplir los requisitos de cumplimiento.

Ciclo de vida de S3: defina la configuración de ciclo de vida para administrar los objetos y almacenarlos de manera económica durante todo su ciclo de vida. Puede realizar la transición de objetos a otras clases
de almacenamiento de S3 o caducar objetos que alcancen el final de su vida útil.

S3 Object Lock: Evita que se eliminen o se sobreescriban objetos de Amazon S3 durante un período de tiempo determinado o de manera indefinida. Object Lock se puede utilizar para cumplir con los requisitos
normativos que requieren almacenamiento de escritura única y lectura múltiple (WORM) o simplemente para agregar otra capa de protección para evitar cambios y eliminaciones de objetos.

Replicación de S3— Replique objetos y sus respectivos metadatos y etiquetas de objeto en uno o más buckets de destino en el mismo o en diferentesRegiones de AWSpara reducir la latencia, el cumplimiento normativo,
la seguridad y otros casos de uso.

Operaciones por lotes de S3: gestione miles de millones de objetos a escala con una sola solicitud de API de S3 o con unos pocos clics en la consola de Amazon S3. Puede utilizar Operaciones Batch para realizar
operaciones comoCopy (Copiar),InvocaciónAWSFunción de Lambda, yRestauraren millones o miles de millones de objetos.

Ejemplo 1: operación de bucket solicitada por el propietario del bucket

En este ejemplo, el propietario del bucket envía una solicitud para una operación de bucket mediante el uso de credenciales raíz de la Cuenta de AWS.

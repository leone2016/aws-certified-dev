## Resumen del tema

- Uso de almacenes de datos en microservicios
- Estrategia de datos para decisiones rápidas
- API como puerta de entrada a lógica y servicios AWS

## Índices secundarios globales (GSI) en DynamoDB

- Clave de partición y de ordenación distintas a la tabla base
- Consultas pueden abarcar todas las particiones
- Se crean con CreateTable → parámetro GlobalSecondaryIndexes
- Consumen capacidad de lectura/escritura del índice, no de la tabla
- Solo soportan consistencia eventual

## Consistencia de datos en servicios AWS

- S3: consistencia fuerte de lectura después de escritura
- DynamoDB: eventual y fuerte (según tipo de lectura)
- Aurora: (revisar modelo de consistencia)

## Cálculo de capacidad de lectura en DynamoDB

- 1 RCU = 4 KB/s lectura eventual; 2 RCU = 1 lectura fuerte de 4 KB
- 10 RCU → 40 KB/s total
- Lecturas fuertes: 40 KB ÷ 4 KB = 10 solicitudes/s
- Lecturas eventuales: 40 KB ÷ 2 KB = 20 solicitudes/s

## Patrones de almacenamiento en AWS

- **Efímero:** Lambda, S2 (S3) – ETL, ML, procesamiento de datos, gráficos
- **Persistente:** EFS, FSx, RDS, DynamoDB – web serving, contenido, microservicios con estado, ML

## Gestión del ciclo de vida de datos

- Políticas de retención y acceso en S3, EFS
- AWS Data Lifecycle Manager para snapshots de EBS
- Seguimiento de creación, procesamiento, análisis, conservación, reutilización

## Objetivos de administración de datos

- Integridad, confidencialidad, disponibilidad
- Cumplimiento y seguridad ante desastres
- Mejora del rendimiento de recuperación (caché, RAM, motores en memoria)

## Estrategias de caché y rendimiento

- CDN, DNS, capas de caché dedicadas
- Validación de datos, TTL, RTO/RPO adecuados
- Diferentes tipos de caché: carga diferenciada, escritura indirecta

## Unificación y carga de datos para análisis

- Consolidar datos en almacenes persistentes para analytics
- Herramientas ETL en AWS: Glue (catálogo), Lambda, Kinesis Data Pipeline, más

## CRUD en DynamoDB con arquitectura serverless

- API Gateway → Lambda → DynamoDB (CRUD)
- Respuesta devuelta por API Gateway

## Diseño de claves en DynamoDB

- Clave primaria = partición (hash) + opcionalmente ordenación (range)
- Elegir clave de partición con alta cardinalidad
- Atributos compuestos para unicidad

## Buenas prácticas de claves y DAX

- Atributos de alta cardinalidad y compuestos
- Copia de elementos populares con DynamoDB Accelerator (DAX)
- Añadir números aleatorios para escrituras intensivas
- Estrategia de aleatorización + partición para rendimiento óptimo

## Consultas vs. escaneos en DynamoDB

- Consultas: usan clave primaria o índices, más eficientes
- Escaneos: recorren toda la tabla, uso intensivo de capacidad



Empecemos con el tercer tema. Utilizar almacenes de datos en el desarrollo de aplicaciones. En las últimas dos lecciones hemos hablado sobre el diseño de aplicaciones con microservicios. Parte de ese diseño y desarrollo es una estrategia de datos para ayudar a gestionar, actuar y reaccionar a sus datos para asegurarse de tomar mejores decisiones, responder más rápidamente y así sucesivamente para transformar sus datos en conocimientos. Para este examen, asegúrese de saber cómo utilizar, administrar y mantener almacenes de datos. Hemos hablado de que las API son la puerta de entrada para nuestros microservicios y el punto de entrada a la lógica de la aplicación. También lo son para los servicios de AWS que puede integrar para soportar el desarrollo de microservicios como Lambda y ECS Fargate, EKS y PrivateLink para conectarse a su VPC y servicios. Y luego, por supuesto, están nuestros almacenes de datos, que se utilizan para persistir los datos que necesitan los microservicios. Profundice en los almacenes de datos disponibles en AWS como RDS, Aurora, DynamoDB, S3, EFS y EBS, entre otros. Asegúrese de saber que almacenamiento de AWS utilizar para datos específicos. Por ejemplo, si necesita un servidor de archivos y almacenamiento de bloques o almacenamiento de objetos. Y comprenda qué modelo de consistencia de base de datos necesita para su aplicación o diferentes escenarios y casos prácticos. Digamos que estás planeando añadir un índice secundario global a tu tabla de DynamoDB para permitir que la aplicación consulte un índice específico en todos los datos de la tabla base y también todas las particiones. ¿Cuáles son tus primeras ideas para desarrollar este tipo de índice? Bueno, un índice global es un índice con una clave de partición y una clave ordenación que pueden ser diferentes de las de la tabla base. Un índice secundario global se considera “global” porque las consultas sobre él pueden abarcar todos los datos de la tabla base en todas las particiones. Para crear una tabla con uno o más índices secundarios globales, ¿qué utilizaría? Utilizaría la operación CreateTable con el parámetro GlobalSecundaryIndexes. Deberá conocer detalles específicos como estos. Los índices secundarios globales heredan el modo de capacidad de lectura y escritura de la tabla base. Así que, como desarrollador, cuando utilice un índice secundario global, deberá tener en cuenta que las consultas o escaneos sobre el índice consumirán unidades de capacidad del índice, no de la tabla base. Y también que las consultas sobre el índice únicamente soportarán consistencia eventual. ¿Qué consistencia soporta S3? S3 proporciona una sólida consistencia de lectura tras escritura. DynamoDB admite consistencia eventual y consistencia fuerte. ¿Qué ocurre con Aurora y RDS? Asegúrese de profundizar en esto. Aquí hay otra cuestión a considerar. Estás actualizando una aplicación para utilizar Lambda y una tabla de DynamoDB que se aprovisionará para tener 10 unidades de capacidad de lectura, y cada elemento de la tabla tendrá un tamaño de 4 KB. ¿Cuántas solicitudes de lectura consistentes, eventuales y fuertes podrá gestionar su tabla por segundo? Asegúrese de saber hacer los cálculos de lectura y escritura. Para obtener el número de solicitudes de lectura consistentes, fuertes y eventuales que su tabla puede acomodar por segundo., simplemente tiene que hacer estos pasos. Recuerde que: 1 WCU (Unidad de Capacidad de Escritura) es igual 1 KB por segundo; o sea, puedes escribir un kilobyte de datos por segundo en esa tabla. 1 RCU (Unidad de Capacidad de Lectura) equivale a 4 KB por segundo; o sea, puedes leer hasta 4 kilobytes de datos por segundo de esa tabla Paso 1: Multiplicar el valor de la RCU aprovisionada por 4 KB Entonces, 10 RCUs veces 4 KB, es igual a Cuarenta Paso 2: Para obtener el número de solicitudes de consistencia fuerte, basta con dividir el resultado del paso uno por 4 KB. Entonces, 40 dividido por 4KB es igual a diez solicitudes de lectura de consistencia fuerte. Paso 3: Para obtener el número de solicitudes de consistencia eventual, basta con dividir el resultado del paso 1 por 2KB. Entonces 40 dividido por dos es igual a 20 solicitudes de lectura de consistencia eventual. Asegúrese también de comprender los diferentes patrones de almacenamiento necesarios para sus datos. ¿Por ejemplo, cuál es un servicio de AWS que utiliza almacenamiento efímero? Bueno, uno es Lambda y también está EC2. ¿Cuáles son los patrones de diseño con los que funciona bien el almacenamiento efímero? Trabajos ETL, Machine Learning, Procesamiento de datos cuando descarga un objeto S3 en respuesta a un evento S3 procesamiento gráfico, entre otros casos de uso. ¿Qué ocurre con los patrones de diseño de almacenamiento persistente y qué servicios de AWS proporcionan almacenamiento persistente? EFS, EBS, FSx, RDS, DynamoDB, entre otros servicios. Y el almacenamiento persistente es necesario para webserving, administración de contenido, microservicios con estado, machine learning, entre otros casos de uso. La solución de almacenamiento óptima para una aplicación varía en función del tipo de método de acceso (bloque, archivo u objeto). Los patrones de acceso, el rendimiento requerido, la frecuencia de acceso, la frecuencia de actualización, la disponibilidad y las restricciones de durabilidad. Los sistemas Well-Architected utilizan múltiples soluciones de almacenamiento y habilitan diferentes funciones para mejorar el rendimiento y utilizar los recursos de forma eficiente. En un diseño de microservicios, cada componente debe tener su propia capa de persistencia de datos. ¿Qué servicios de AWS pueden ayudar a administrar el ciclo de vida de los datos? También debe realizar un seguimiento de sus patrones de creación, procesamiento, análisis, conservación, acceso y reutilización de datos. La administración del ciclo de vida puede utilizar políticas para saber dónde almacenar tus datos, durante cuánto tiempo, quién tiene acceso, entre otros aspectos. S3 y EFS disponen de políticas de ciclo de vida, al igual que otras opciones de almacenamiento. También existe AWS Data LifeCycle Manager para ayudar a automatizar la retención, creación y eliminación de instantáneas de EBS. Como desarrollador, ¿cuáles son sus objetivos para la administración de datos? Para mí, la integridad, la confidencialidad y la disponibilidad son los principales objetivos, así como garantizar la conformidad o la seguridad de los datos en caso de desastre. ¿Es uno de sus objetivos garantizar un mayor rendimiento en la recuperación de datos? En caso afirmativo, ¿qué utilizaría? ¿RAM y motores en memoria? ¿CDN? ¿DNS? Bueno, en diseños distribuidos, puedes desarrollar una capa de caché dedicada para que funcione independientemente de la caché del almacén de datos y los ciclos de vida. Si este es su diseño, asegúrese de conocer las prácticas recomendadas como la validación de los datos que se almacenan en caché, los TTLS para que los datos caduquen en consecuencia y la definición de los RTOs y RPOs adecuados. Profundice en las estrategias de almacenamiento en caché y comprenda las ventajas y desventajas junto con cuándo utilizar cada una, como por ejemplo, cargas diferenciadas y escritura indirecta. Demos un paso atrás en su persistencia de datos y serialización y deserialización de datos para proporcionar persistencia a un almacén de datos. Lo más probable es que trabaje con diferentes tipos de datos en su aplicación. ¿Cuál es su diseño para unificar y cargar los datos en su almacén de datos persistentes para el análisis a fin de obtener mejoras basadas en datos? ¿Qué herramientas de ETL están disponibles en AWS? Profundice en AWS Glue y el catalogo de datos de AWS Glue: EMR, Lambda, Kinesis, Data Pipeline y mucho más. Para este examen debe asegurarse de tener suficiente profundidad para los conceptos básicos, pero también debe asegurarse de poder agregar mejoras. Por ejemplo, piense en qué sucedería si necesitara añadir la capacidad de crear, leer, actualizar y eliminar elementos de una tabla DynamoDB. ¿Qué servicios de AWS podría utilizar para actualizar su aplicación? Puede crear una API sin servidor que cree, lea, actualice y elimine elementos de una tabla de DynamoDB mediante Lambda y API Gateway. Para este diseño, cuando invoque su API HTTP, API Gateway dirigirá la solicitud a su función de Lambda, Lambda interactuará con la tabla de DynamoDB y API Gateway le dará una respuesta finalmente. Además, ¿cómo puede asegurarse de elegir la clave de partición correcta para un diseño de esquema de DynamoDB? Asegúrese de profundizar en las claves primarias de DynamoDB y comprender por qué necesita una clave de partición. ¿Cuáles son las prácticas recomendadas para las claves de partición en DynamoDB? Utilice atributos de alta cardinalidad que son atributos que tienen valores distintos para cada elemento. Utilice atributos compuestos para combinar más de un atributo para formar una clave única. Copie los elementos populares cuando haya un alto volumen de tráfico de lectura utilizando a Amazon DynamoDB Accelerator (o Dax). Añada números o dígitos aleatorios de un rango predeterminado para casos prácticos de escritura intensiva. Una estrategia de aleatorización puede mejorar en gran medida el rendimiento de escritura junto con enfoque de partición para leer elementos individuales. Profundice en las estrategias de clave de partición y evalúe los enfoques en función de su patrón de acceso y ingesta de datos para elegir la clave adecuada con los menores problemas de ralentización posibles. Y también, para DynamoDB, conozca las diferencias entre consultas y escaneos y cuándo utilizar cada una. En el próximo vídeo comencemos con la primera pregunta del tutorial. Gracias por seguirnos hasta este punto. Nos vemos pronto.
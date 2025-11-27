![img](https://workoscdn.com/images/v1/BjHwIKiOu2fOOU94cRG-F5tC3MECG5iPfjZf_7LBuio)

CV-LEO

Copy full summary

## Principios de diseño de Lambda

- Operaciones como código (IaC)
- Escalado horizontal para alta disponibilidad

## Configuración básica de una función Lambda

- Definir memoria, tiempo de ejecución, tiempo de espera, concurrencia, capas y extensiones
- Variables de entorno para parámetros dinámicos
- Configurar desencadenadores (eventos, programación, solicitudes externas)

## Concurrencia y control de costos

- Concurrencia reservada divide la concurrencia disponible en subconjuntos
- Ajustar límites de concurrencia para equilibrar carga entre funciones idénticas
- En flujos Kinesis/DynamoDB, la unidad de concurrencia son las particiones

## Solución de problemas de rendimiento

- Usar CloudWatch para comparar métricas entre funciones idénticas
- Incrementar o reducir el límite de concurrencia según el caso
- Verificar particiones activas en streams para identificar cuellos de botella

## Variables de etapa vs variables de entorno

- Variables de etapa (stage variables) recomendadas para cambiar comportamiento según la etapa de la API
- Usar variables de etapa para seleccionar tablas DynamoDB distintas por etapa

## Mapeo de origen de eventos

- Configurar origen (SQS, Kinesis, DynamoDB) que envíe lotes a Lambda
- Definir reintentos y política de redireccionamiento en caso de fallos
- Configurar destinos separados para invocaciones exitosas y fallidas

## Manejo de errores en Lambda

- Tipos de error: de invocación (request, throttling, access) y de función (function, runtime)
- Estrategias: reintentos, envío a cola de depuración, ignorar error
- Lambda reintenta automáticamente 2 veces en invocaciones asíncronas
- Configurar colas de mensajes fallidos (DLQ) para capturar eventos no procesados

## Invocación síncrona vs asíncrona

- Síncrona: Lambda espera respuesta, devuelve datos y metadatos (versión, etc.)
- Asíncrona: cliente entrega evento y Lambda gestiona el resto, sin respuesta inmediata
- CLI AWS: aws lambda invoke para invocaciones síncronas

## Integración con otros servicios de AWS

- Registro y monitoreo: CloudWatch, AWS X‑Ray
- Envío de resultados a SQS, SNS, EventBridge, otra Lambda
- Uso de VPC: ENI automática, grupos de seguridad y subredes compartidas

## Seguridad y permisos en VPC

- Configurar ENI mediante VPC, subred y SG específicos para Lambda
- Condiciones de política IAM: lambda:VpcId, lambda:SubnetIds, lambda:SecurityGroupIds

## Pruebas de funciones Lambda

- Pruebas unitarias: invocar punto de entrada y validar lógica interna
- Pruebas de integración: validar interacción con servicios externos
- Pruebas de extremo a extremo y automatización en pipelines CI/CD

## Optimización de rendimiento

- Reducir latencia de arranque en frío: evitar dependencias pesadas en código de inicialización
- “Warm‑up” con EventBridge no siempre efectivo (escala, AZ diferentes)
- Concurrencia provisionada para garantizar latencia mínima

## Memoria y CPU

- A mayor memoria, aumenta CPU asignada automáticamente
- Balancear velocidad vs costo al elegir memoria
- Herramienta **AWS Lambda Power Tuning** (Step Functions) para probar distintas configuraciones

## Herramientas de análisis de costo y rendimiento

- **AWS Lambda Power Tuning** para medir tiempo y coste por configuración de memoria
- Herramientas de cost‑optimization para comparar rendimiento vs gasto

## Cuándo evitar Lambda

- Funciones que solo coordinan llamadas a otros servicios → usar Step Functions
- Transferencia de datos sin lógica empresarial → usar integraciones directas (API Gateway + VTL, Service Integration)

## Filtrado de eventos para reducir invocaciones

- Filtrar en API Gateway (VTL) o en S3/ SNS antes de llegar a Lambda
- EventBridge y reglas de contenido para activar Lambda solo en eventos relevantes
- SNS permite filtros de prefijo/sufijo en topics

## Buenas prácticas adicionales

- Minimizar tamaño del paquete de implementación (dependencias, código estático)
- Utilizar variables de entorno para configuraciones sensibles
- Supervisar logs y métricas continuamente (CloudWatch, X‑Ray)
- Automatizar pruebas y despliegues en la canalización de CI/CD



Comencemos con el segundo tema: Desarrollar código para AWS Lambda. En la lección anterior hablamos sobre el desarrollo con Lambda, pero en esta lección profundizaremos más en eso. Para Lambda hay dos principios de diseño clave bajo el pilar de excelencia operativa del Marco de AWS Well-Architected y el pilar de fiabilidad que me llaman la atención. Uno es realizar operaciones como código y el otro es escalar horizontalmente para aumentar la disponibilidad de la carga de trabajo agregada. Lambda es un excelente servicio de cómputo sin servidor para ejecutar el código de tu aplicación. Cuando creas tu función de Lambda, escribes código para hacer algo. Cuando se invoca Lambda, hay un entorno de ejecución que tiene un tiempo de ejecución que coincide con el lenguaje del código de tu función. El entorno de ejecución también administra los recursos necesarios para ejecutar tu función, al tiempo que proporciona soporte de ciclo de vida para el tiempo de ejecución de tu función y cualquier extensión externa. Cuando creas la función de Lambda, especificas la información de configuración, como la memoria, los tiempos de ejecución, entre otras configuraciones. Profundiza en el ciclo de vida de tu entorno de ejecución. Comprende los desencadenadores para invocar tus funciones y las formas de invocación, como los eventos de ciclo de vida, las solicitudes externas, los servicios de AWS, la programación y también los manuales que pueden ser sincrónos, asíncronos o de sondeo. Comprende cómo configurar funciones de Lambda y definir variables de entorno y parámetros para memoria, concurrencia, tiempo de espera, tiempo de ejecución, controlador, capas, extensiones, desencadenadores y destinos. ¿Sabes qué utilizar para evitar que una función utilice demasiada concurrencia reservada? En lo que hace a la optimización de costos, es posible que desees controlar tu concurrencia y se podría utilizar la concurrencia reservada que divide el grupo de la concurrencia disponible en subconjuntos. Aquí hay una pregunta que atañe un poco a la solución de problemas también. ¿Qué sucedería si implementaras una aplicación que utiliza dos funciones de Lambda idénticas con exactamente el mismo código para procesar solicitudes ad hoc, pero las funciones tienen un rendimiento diferente? Por fortuna, has configurado CloudWatch para realizar un seguimiento de tus métricas y puedes ver que la primera función de Lambda está procesando las solicitudes como se esperaba, pero la segunda función está tardando más en hacerlo. ¿Qué puedes hacer para resolver este problema? Bueno, primero necesitamos conocer la unidad de escala de Lambda, que es la ejecución concurrente. Por lo tanto, se podría establecer el límite de ejecución concurrente de ambas funciones en un número mayor o disminuir el límite de ejecución concurrente de la primera función que está funcionando como se esperaba. Para este examen también debes comprender cómo las funciones de Lambda procesan registros en Data Streams. Para las funciones de Lambda que procesan flujos de Kinesis o DynamoDB, el número de particiones es la unidad de concurrencia. Si el flujo tiene 100 particiones activas, habrá como máximo 100 invocaciones de funciones de Lambda en ejecución simultánea. Esto se debe a que Lambda procesa los eventos de cada partición en secuencia. ¿Qué ocurre si necesitas utilizar la misma función de Lambda para varias etapas de tu API, pero esta función necesita leer datos de diferentes tablas de DynamoDB en función de la etapa de las que se llame? ¿Qué solución implementarías? ¿Deberías crear variables de entorno en tu función o utilizar variables de etapa? Lo correcto es utilizar variables de etapa que puedes definir como atributos de configuración, en la etapa de implementación de tu API de REST. No bastaría con crear una variable de entorno en la función. Sería necesario integrar la función de Lambda con la API Gateway mediante una variable de escenario y añadir también la configuración de mapeo adecuada. ¿Y si necesitas procesar elementos de un flujo o una cola, qué configurarías? Yo elegiría un mapeo de origen de eventos, que es un recurso de Lambda que lee elementos de una cola de SQS, un flujo de Kinesis o un flujo de DynamoDB, y envía elementos a la función por lotes. Además, el mapeo de origen de eventos puede manejar reintentos por errores o por limitación. Hablemos del manejo de errores. ¿Qué puedes utilizar para ayudar con los errores mediante el uso de código en Lambda? Cuando invocas una función, puede haber dos tipos de errores. Errores de invocación y errores de función. Según el tipo de error, el tipo de invocación y el cliente o servicio que invoca la función, el comportamiento de reintento y la estrategia de administración de errores varia. ¿Cuáles son algunos errores de invocación frecuentes para las funciones de Lambda? Están request, caller y account. ¿Y los errores frecuentes de la función? Esos son function y runtime. Parte de su diseño y desarrollo con Lambda debe incluir una estrategia para manejar los errores. Puedes reintentar, enviar el evento a una cola para depuración, o ignorar el error. Si utilizas una estrategia de reintento, debes asegurarte de que tu código pueda manejar el mismo evento varias veces sin causar duplicados o problemas. Asegúrate de comprender el comportamiento de reintento del invocador para las funciones invocadas indirectamente. Para la invocación asíncrona, Lambda gestiona los reintentos y puede enviar registros de invocación a un destino, como SQS, SNS, Lambda o EventBridge. Sepa configurar esto y los permisos necesarios también. Con Lambda, puedes configurar destinos separados para invocaciones exitosas y eventos que fallen en el procesamiento. También puedes configurar una cola de mensajes fallidos para añadir más control sobre el manejo de mensajes para todas las innovaciones asincrónas, incluidos S3, SNS, IoT, entre otros servicios. ¿Cuantas veces reintentará Lambda un error de función? La respuesta es dos veces y si la función no tiene suficiente capacidad para manejar todas las solicitudes entrantes, los eventos podrían esperar en la cola durante horas o días hasta su envío a la función. De nuevo, puedes configurar una cola de mensajes fallidos en la función para capturar los eventos que no fueron procesados con éxito. Ya hemos hablado de los mapeos de origen de eventos, pero para los mapeos de origen de eventos que leen de una cola, puedes configurar el tiempo entre reintentos y el destino de los eventos fallidos, configurando el tiempo de espera de visibilidad y la política de direccionamiento en la cola de origen. Los servicios de AWS también pueden invocar una función de forma síncrona o asíncrona. Cuando se invoca una función de forma síncrona, Lambda ejecuta la función y espera una respuesta. Cuando la función finaliza, Lambda devuelve la respuesta del código de la función con datos adicionales como la versión de la función invocada. Para invocar una función de forma síncrona con la CLI de AWS, ¿qué comando se utiliza? El comando invoke. Varios servicios de AWS, como Amazon S3 y SNS, invocan funciones de forma asíncrona para procesar eventos. Cuando invocas una función de forma asíncrona, no esperas una respuesta del código de la función. Tú entregas el evento a Lambda y Lambda se encarga del resto. Puedes configurar la forma en que Lambda maneja los errores y puedes enviar registros de invocación a un recurso posterior para encadenar componentes de tu aplicación. Para ayudar con los errores en las aplicaciones de Lambda, ¿qué servicios de AWS puedes integrar? Siempre recomiendo utilizar una combinación de registros, métricas, alarmas y rastreo para detectar e Identificar rápidamente problemas en el código de tu función, API u otros recursos que den soporte a tu aplicación, como Cloud Watch y AWS X-Ray. Hace unos minutos mencionamos la configuración de permisos. Asegúrate de saber cómo acceder a los recursos privados en las VPCs desde tu código Lambda. Puedes utilizar una interfase de red elástica con un grupo de seguridad. Ten en cuenta que varias funciones pueden compartir la ENI, pero únicamente si esta función comparte la misma subred y grupo de seguridad en tu VPC. Lambda también utiliza automáticamente el permiso de tu función para crear y gestionar la ENI. También puedes utilizar claves de condición específicas de Lambda para la configuración de la VPC con el fin de proporcionar controles de permisos adicionales para tus funciones de Lambda. Si profundizamos un poco más, ¿sabes cuáles son las claves de condición en las políticas de IAM? - lambda:VpcIds - lambda:SubnetIds - o lambda:SecurityGroupIds AWS tiene tutoriales para esto, así que tómate un tiempo para poner manos a la obra y profundizar. Siempre es una práctica recomendada probar las funciones Lambda. Asegúrate de saber cómo escribir y ejecutar código de prueba utilizando los servicios y herramientas de AWS. ¿Qué sucede con las pruebas de unidad? Digamos que tienes una serie de funciones que proporcionan gran parte del comportamiento de tu aplicación. Puedes utilizar una prueba de unidad para llamar a una función de punto de entrada que invoque a otras y probar estas funciones juntas como una sola unidad. También puedes utilizar pruebas de integración para probar cómo interactúan los servicios entre sí. Cuando pruebas una función de Lambda, estás probando su lógica, carga e invocación. Deberías incluir pruebas de extremo a extremo. Y, a medida que tu aplicación escala, utiliza pruebas automatizadas para obtener información sobre el estado actual de tu aplicación. Y no te olvides de estudiar la automatización de las pruebas en tu canalización de creación. Concluyamos esta lección y hablemos sobre el ajuste y hablemos sobre el ajuste de tus funciones de Lambda para un rendimiento óptimo. Lambda administra el escalado automáticamente, que ya es de alto rendimiento con la paralización y la concurrencia. Pero también podemos optimizar nuestras funciones de Lambda individuales para reducir la latencia y aumentar el rendimiento. Profundicemos en algunas formas de añadir más optimización. Empecemos por latencia. Cuando el servicio Lambda recibe una solicitud para ejecutar una función a través de la API de Lambda, el servicio prepara primero un entorno de ejecución. Durante este paso, el servicio descarga el código de la función que se almacena en un bucket de S3 interno o en Amazon o en Amazon ECR si la función utiliza empaquetado de contenedor. A continuación, crea un entorno con la memoria, el tiempo de ejecución y la configuración especificados. Una vez completado, Lambda ejecuta cualquier código de inicialización fuera del controlador de eventos antes de ejecutar finalmente el código del controlador. En cuanto al costo, no se cobra por este arranque en frío, pero añade latencia a la duración total de la invocación. Una vez finalizada esta ejecución, el entorno de ejecución se congela para garantizar una mejor administración de los recursos y un mejor rendimiento. Así, cuando llega otra solicitud para la misma función, el servicio puede reutilizar el entorno. Esta solicitud suele ser más rápida y se denomina “arranque en caliente”. Los arranques en frío suelen ser más frecuentes en funciones de desarrollo y prueba. Ahora bien, no se debe depender de este entorno de ejecución para su reutilización con el fin de optimizar el rendimiento. Profundiza en por qué, por ejemplo, si actualizas tu código o cambias la configuración funcional, el siguiente arranque será en frío. Un plan mejor es usar reglas EventBridge para programar invocaciones a cada minuto para ayudar a mantener el entorno activo y caliente. De nuevo, profundiza en por qué esto tampoco es lo mejor. Por ejemplo, calentar el entorno no ayudará si las funciones se escalan para satisfacer el tráfico o si la función se ejecuta en una zona de disponibilidad diferente. Una mejor solución es usar concurrencia aprovisionada para asegurar la mejor latencia posible. Sigamos adelante y hablemos de cómo optimizar su memoria y potencia de cómputo en Lambda. En sus configuraciones de Lambda, cuando añada más memoria, también aumentará la cantidad de CPU. Por lo tanto, si su función está limitada por la CPU o la memoria, puede cambiar la configuración de la memoria para mejorar el rendimiento. Sin embargo, elegir la memoria asignada a las funciones de Lambda es un proceso de optimización que equilibra velocidad y costo. Y si se siguen las prácticas recomendadas con la automatización y no se ejecutan manualmente pruebas en sus funciones y se seleccionan diferentes asignaciones de memoria, puede utilizar la herramienta AWS Lambda Power Tuning que se sirve de Step Functions para ejecutar múltiples versiones concurrentes de su función de Lambda en diferentes asignaciones de memoria y lograr mediciones de rendimiento. Por otra parte, Cost Optimizer es otra herramienta que puede utilizar para automatizar un análisis de rendimiento de costos para todas sus funciones de Lambda. Profundice también en la optimización de su inicialización estática que puede contribuir al arranque en frío general del que hablábamos antes. Una aplicación de sistemas distribuidos consiste en múltiples servicios que se comunican mediante mensajes a través de una red. Debido a los retrasos de la red, el tráfico, los reintentos de mensajes, las communtaciones por error del sistema y por los perfiles de rendimiento individuales de los servicios, el tiempo necesario para completar una unidad de trabajo puede variar. AWS X-Ray puede ayudar a identificar el rendimiento de sus valores atípicos. Para el examen, sepa también cuándo no utilizar una función de Lambda, porque puede haber otras alternativas que mejoren el rendimiento. En el caso de las funciones que actúan como organizadores, llamando a otros servicios y funciones y coordinando el trabajo, esto puede provocar tiempo ocioso en la función y un aumento de los costos. Trasladar el flujo de coordinación a AWS Step Functions crea una máquina de estado más mantenible y resiliente, y puede ayudar a reducir los costos. Otra cosa para agregar es que las funciones de Lambda que transportan datos de un servicio a otro sin realizar ninguna lógica empresarial en esos datos a menudo pueden sustituirse por integraciones de servicios. Por ejemplo, no suele ser necesario colocar una función de Lambda entre API Gateway y DynamoDB para leer un elemento de una tabla. Esto se puede conseguir utilizando Velocity Template Language (o VTL) en una integración de servicios de API Gateway directamente con DynamoDB. Esto puede ayudar a mejorar la escalabilidad y reducir los costos. Si un microservicio envía todos los eventos a una función de Lambda para su filtrado, y solo opera en un pequeño subconjunto de eventos, es posible que pueda implementar el filtrado antes de invocar la función. Por ejemplo: - Los eventos de S3 se pueden filtrar en función de patrones de prefijos y sufijos. - SNS puede filtrar mensajes antes de invocar objetivos -Y con Amazon EventBridge, puede utilizar lógica de filtrado de contenido dentro de las reglas para ser muy selectivo en los eventos que activan sus funciones. El uso de filtros puede reducir los costos y mejorar la eficiencia, ya que solo invoca funciones de Lambda para eventos que le interesan a su aplicación. Profundice más en Lambda y en serverless para entender cómo usar el contexto de ejecución para la reutilización. Cómo usar variables de entorno. Cómo manejar las dependencias en el código de la función. Cómo reducir su paquete de implementación para el tiempo de ejecución. Cómo y por qué manejar la memoria de su Lambda. El tiempo de ejecución de Lambda. Y cómo supervisar los registros de Lambda, entre otras optimizaciones. En el próximo vídeo empecemos con el tercer tema del Dominio 1: Utilizar almacenes de datos en el desarrollo de aplicaciones. Gracias por seguirnos hasta este punto. Nos vemos pronto.
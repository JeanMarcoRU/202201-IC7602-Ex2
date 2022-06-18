# Jean Marco Rojas - 2015040717

1.
(Código inspirado del diagrama del libro. Pag 543).
![image](https://user-images.githubusercontent.com/15478613/174422878-112d33e1-92ff-4fcd-a64e-e01a01ad20cb.png)

![image](https://user-images.githubusercontent.com/15478613/174423799-500daa34-1c65-4b08-8158-f445ada297fa.png)

![image](https://user-images.githubusercontent.com/15478613/174423864-44d81435-bbc7-4e43-ba6f-24635e2fd882.png)

![image](https://user-images.githubusercontent.com/15478613/174423883-09308a69-6925-41d5-91e6-cae16beb92d9.png)

Enviamos el mensaje que recibe de parámetro y poner un temporizador, intenta recibir un paquete, con la función reciveudp, si todo ok, cancela el temporizador, ya que se inicia antes de solicitar una respuesta, luego preguntamos si es de tipo CRC invalido para retransmitir, si no es de ese tipo, revisa el CRC, y mientras ese paquete que llego sea inválido, lo envía de nuevo, si esta bueno lo retorna si no lo puede retornar es por que el mensaje nunca llegó (se puede revisar el temporizador), luego preguntamos si quedan intentos por transmitir hacemos una llamada recursiva y si no quedan intentos devolvemos error (-1).
En la función de solicitar coneccion del cliente primero se envía el mensaje de solicitud de conexión al servidor, de esa solicitud se toma el número de secuencia y se envía y se espera una respuesta válida y de la respuesta se toma de nuevo el número de secuencia, después se crea el segmento de la confirmación y se envía al server, entonces la coneccion ya está establecida para el cliente y se retorna la secuencia y si no se pudo establecer conexión con el server se devuelve error (-1)
En la función de conectar al server, según el libro (pág 518) se busca por un espacio en la tabla de conexiones disponibles y cuando la encuentra (si es que existe) toma el número de secuencia del mensaje que se recibe y crea una respuesta hacia el cliente (con el ack), se envía al cliente y espera una respuesta que tiene que ser de éxito o rechazo.
asumimos la existencia de la función create_sec crea el mensaje (segmento).
(SEC. 6.3, Pág 515-543, Tanenbaum, A. Computer Networks. 4ta edición).


2.
a)
Aunque parezca una solución fácil proporcionar la suficiente capacidad de enrutador, espacio en búfer y ancho de banda como para que los paquetes fluyan con facilidad. El problema con esta solución es que es costosa. Conforme pasa el tiempo y los diseñadores tienen una mejor idea de cuánto es suficiente, esta técnica puede ser práctica. En cierta medida, el sistema telefónico tiene un sobreaprovisionamiento. Es raro levantar un auricular telefónico y no obtener un tono de marcado instantáneo. Simplemente hay mucha capacidad disponible ahí que la demanda siempre se puede satisfacer. Por ejemplo para el almacenamiento en búfer los flujos pueden almacenarse en el búfer en el lado receptor antes de ser entregados. Almacenarlos en el búfer no afecta la confiabilidad o el ancho de banda, e incrementa el retardo, pero atenúa la fluctuación. Para el vídeo o audio bajo demanda, la fluctuación es el problema principal, por lo tanto, esta técnica es muy útil. (SEC. 5.4, Pág 398-399, Tanenbaum, A. Computer Networks. 4ta edición).

b)
Si es posible y no solo es posible sino que ya se hace actualmente en muchas redes ya que las herramientas de monitoreo de red permiten incorporar inteligencia artificial y machine learning, ya que ambas prosperan en torno a los datos. Con machine learning, las herramientas de monitoreo de red pueden adaptarse al entorno de red y proporcionar sugerencias basadas en los datos disponibles, lo que abre muchas posibilidades como cargas compartidas basadas en el uso, perfiles de notificación más inteligentes, adaptación de red y la capacidad de tomar medidas correctivas de forma automática, también para pronósticos. También un tema clave en el que una IA puede influir es la automatización. En el monitoreo de red, la automatización ayuda a las herramientas de monitoreo de red a reaccionar con base en umbrales o un conjunto de reglas/criterios que se deben cumplir. Con la automatización, la herramienta de monitoreo puede detectar y solucionar problemas automáticamente (monitoreo proactivo), enviar notificaciones de alertas y también proporcionar sugerencias para un mejor rendimiento y mantenimiento de la red con base en el uso y la prioridad (aumentando la escabilidad). (SEC. 5.4, Pág 397-409, Tanenbaum, A. Computer Networks. 4ta edición)

3.
a)
Cuando hay saltos entre routers el RTT se ve afectado de 2 maneras, Si se hace demasiado corto, ocurrirán retransmisiones innecesarias, cargando la Internet con paquetes inútiles. Si se hace demasiado largo, el desempeño sufrirá debido al gran retardo de retransmisión de cada paquete perdido. Es más, la varianza y la media de la distribución de llegadas de confirmaciones de recepción pueden variar con rapidez en unos cuantos segundos, a medida que se generan y se resuelven congestionamientos. Cada red tiene una unidad máxima de transferencia (MTU) y cada segmento debe caber en la MTU. En la práctica, la MTU es, generalmente, de 1500 bytes (el tamaño de la carga útil en Ethernet) y, por tanto, define el límite superior del tamaño de segmento. El protocolo básico usado por las entidades TCP es el protocolo de ventana corrediza. Cuando un transmisor envía un segmento, también inicia un temporizador. Cuando llega el segmento al destino, la entidad TCP receptora devuelve un segmento (con datos, si existen, de otro modo sin ellos) que contiene un número de confirmación de recepción igual al siguiente número de secuencia que espera recibir. Si el temporizador del emisor expira antes de la recepción de la confirmación, el emisor envía de nuevo el segmento. Es importante saber el máximo y mínimo MTU ya que cuando dos dispositivos inician una conexión y empiezan a intercambiar paquetes, estos se enrutan a través de múltiples redes, no solo hay que tener en cuenta la MTU de los dos dispositivos al final de cada comunicación, sino también todos los enrutadores, conmutadores y servidores intermedios. Los paquetes que excedan la MTU en cualquier punto de la ruta de red se fragmentan. Supongamos que el servidor A y el cliente A están conectados, pero los paquetes de datos que se envían mutuamente tienen que atravesar los enrutadores B y C. El servidor A, el ordenador A y el enrutador B tienen todos una MTU de 1500 bytes. Sin embargo, el enrutador C tiene una MTU de 1400 bytes. Si el servidor A y el ordenador A no detectan la MTU del enrutador C y envían paquetes de 1500 bytes, el enrutador B fragmentará todos sus paquetes de datos en tránsito. (SEC. 6.5, Pág 535-536,551, Tanenbaum, A. Computer Networks. 4ta edición).

b)
Los caches regionales, están ubicados entre el servidor de origen y los puntos de presencia: ubicaciones de borde globales que distribuyen contenido directamente a los clientes. A medida que los objetos se hacen menos populares, los puntos de presencia individuales podrían quitar dichos objetos para dejar espacio a contenido más popular. Las cachés perimetrales regionales tienen una caché mayor que un punto de presencia individual, de modo que los objetos permanecen más tiempo en la ubicación de caché perimetral regional más cercana. De esta manera, es posible conservar un mayor volumen de contenido más cerca de los clientes, lo que reduce el RTT y que los paquetes vayan al servidor de origen lo que mejora drásticamente mejora el rendimiento general para los clientes, haciendo un uso eficiente del ancho de banda y a su vez aligera el balanceo de cargas de los servidores.


4.
IP es un protocolo sin conexión, lo que significa que no se crea ninguna conexión dedicada de extremo a extremo antes de enviar los datos. Conceptualmente, la comunicación sin conexión es similar a enviar una carta a alguien sin notificar al destinatario con anticipación.

![image](https://user-images.githubusercontent.com/15478613/174421817-fad35063-d6d3-40f7-ae8a-b63e2e2ae381.png)

Como se muestra en el diagrama, el servicio postal utiliza la información en una carta para entregarla a un destinatario. La dirección en el sobre no proporciona datos que indiquen si el receptor está presente, si la carta llegará a destino o si el receptor puede leerla. De hecho, el servicio postal no está al tanto de la información contenida dentro del paquete que entrega y, por lo tanto, no puede proporcionar ningún mecanismo de corrección de errores.

Las comunicaciones de datos sin conexión funcionan según el mismo principio.

IP es un protocolo sin orientación a conexión y, así es mejor por que no requiere ningún intercambio inicial de información de control para establecer una conexión de extremo a extremo antes de reenviar los paquetes. Además, tampoco requiere campos adicionales en el encabezado de la unidad de datos del protocolo (PDU) para mantener una conexión establecida. Este proceso reduce en gran medida la sobrecarga del IP. Sin embargo, sin una conexión de extremo a extremo preestablecida, los emisores no saben si los dispositivos de destino están presentes y en condiciones de funcionamiento cuando envían los paquetes, y tampoco saben si el destino recibe el paquete o si puede acceder al paquete y leerlo.

![image](https://user-images.githubusercontent.com/15478613/174421834-7ba753fd-e684-459e-955f-c25282aff4ed.png)

En este diagrama, se muestra un ejemplo de comunicación con Internet Protocol.


Referencias Bibliográficas
* Herramientas de monitoreo de red | Tráfico de red - ManageEngine OpManager. (2022). Retrieved 18 June 2022, from https://www.manageengine.com/latam/network-monitoring/herramientas-monitoreo-de-red.html
* Web Services, A. (2022). Cómo funcionan las cachés regionales. Aws. https://docs.aws.amazon.com/es_es/AmazonCloudFront/latest/DeveloperGuide/HowCloudFrontWorks.html
* Características del protocolo IP. (2022). Retrieved 17 June 2022, from http://itroque.edu.mx/cisco/cisco1/course/module6/6.1.2.2/6.1.2.2.html


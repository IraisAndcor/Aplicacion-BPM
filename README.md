*****ARDUINO******

El sensor  de pulso MAX30102 es dispositivo que integra un pulsioxímetro y  monitor de frecuencia cardiaca. Cuenta con infrarrojo, detectores fotoeléctricos, dispositivos ópticos y circuitos electrónicos de baja frecuencia con supresión de luz ambiental. 

El Sensor de Pulso MAX30102 es útil para intégralo en proyectos donde se mida el pulso y pulso cardiaco , ya que funciona de la siguiente manera:
* Por Método de foto disolución: La medida del pulso y saturación de oxigeno en la sangre es realizado por medio del tejido humano que provoca diferentes transmitancias en la luz cuando los vasos sanguíneos laten.
* Fuente de luz: Una longitud de onda especifica de luz emitida por un diodo para medir la oxihemoglobina (HbO2) y la hemoglobina (Hb) de la sangre arterial.
* La transmitancia se convierte en señal eléctrica: El cambio en el volumen de las pulsaciones arteriales provoca que la transmitancia de la luz cambie. En este momento la luz reflejada por el tejido humano es recibida por el transductor fotoeléctrico, transformándola en una señal eléctrica.


Este código está diseñado para medir el ritmo cardíaco utilizando el sensor MAX30105, y luego enviar los datos del ritmo cardíaco a través de Bluetooth usando un módulo Bluetooth conectado a los pines 2 y 3 del Arduino.

Se incluyen las librerías necesarias para el funcionamiento del código. SoftwareSerial es utilizada para comunicarse con el módulo Bluetooth a través de pines digitales, Wire es necesaria para la comunicación I2C con el sensor MAX30105, y MAX30105.h y heartRate.h son utilizadas para interactuar con el sensor de ritmo cardíaco.

Se declaran las variables globales necesarias para almacenar y procesar los datos del ritmo cardíaco.

En la función setup(), se inicia la comunicación con el módulo Bluetooth y se configura el sensor MAX30105. Si el sensor no puede ser inicializado, el programa quedará bloqueado en un bucle infinito.

En el bucle principal loop(), se obtiene el valor de la intensidad infrarroja (irValue) del sensor. Se verifica si se detectó un latido cardíaco llamando a la función checkForBeat(). Si se detecta un latido, se calcula la frecuencia cardíaca en latidos por minuto (beatsPerMinute). Se almacena esta información en un array para su posterior procesamiento y se envía la frecuencia cardíaca medida a través del módulo Bluetooth.

Arduino limita que la comunicación bluetooth no pase del rango de 250, ya que la comunicación uint8 que utiliza el bluetooth solo maneja un rango de 0 - 255, y en caso de tener un número mayor a eso el dispositivo receptor no podría interceptarlo. Es por eso que cualquier valor superior a 250 sera sustituido por un 250.

*****COMUNICACIÓN BLUETOOTH*****


Este es un código para genera una conexión con Arduino que utiliza un módulo Bluetooth para enviar datos de lecturas analógicas a un dispositivo Bluetooth conectado, como un teléfono inteligente. A continuación, describiré paso a paso lo que hace cada parte del código: Esta línea incluye la librería SoftwareSerial, que permite la comunicación serie a través de pines digitales que no son los pines de hardware RX y TX. Se inicializa un objeto bluetooth de la clase SoftwareSerial en los pines digitales 2 y 3 del Arduino para la comunicación con el módulo Bluetooth. En la función setup(), se inicializa la comunicación serial con una velocidad de 9600 baudios tanto para la comunicación con el monitor serial (a través del puerto USB) como para la comunicación con el módulo Bluetooth. En el bucle principal loop(), se lee el valor analógico del pin A0 (0-1023) y se divide por 4 para convertirlo a un rango de 0-255, que es el rango de valores admitido por Bluetooth. Si el valor excede 250, se establece en 250. Luego, el valor se envía a través de Bluetooth usando bluetooth.println(val), seguido de un retraso de 10 milisegundos antes de la siguiente iteración del bucle.

En resumen, este código está configurado para leer un valor analógico de un sensor conectado al pin A0 del Arduino, convertirlo a un rango de 0-255 y luego enviar ese valor a través de Bluetooth a otro dispositivo cada 10 milisegundos.

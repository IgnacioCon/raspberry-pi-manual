# Capitulo 3: GPIO

## 3.1 Entradas/Salidas de Propósito General

Una de las características más poderosas de Raspberry Pi es la fila de pines de entrada y salida de propósito general (GPIO, por sus siglas en ingles).  Estos pines son una interfaz física entre el mundo exterior y la Raspberry Pi.  Al nivel más simple se pueden ver como interruptores que el usuario o que por otro medio puede apagar o encender (entrada), o que la Raspberry Pi puede apagar o encender (salida).  Con ellos se pueden llevar a cabo vario proyectos de los más simples, como hacer parpadear un LED hasta los más complejos como crear un drone funcional.

Los GPIO tienen varios tipos de conexiones:

* Pines GPIO que se utilizan como entrada o salida. 
  * Como salida se pone un pin en estado ALTO (3.3 V) o BAJO (0 V).
  * Como entrada se detecta si un pin está en estado ALTO o BAJO.
* Pines de interfaz I2C que permiten conectar módulos de hardware con solo dos pines de control.
* Pines de interfaz SPI que permiten interactuar con dispositivos SPI, un concepto similar al I2C pero con un estándar diferente.
* Pines seriales Tx (transmison de datos) y Rx (recepción de datos) para comunicación con periféricos seriales.


## Pines de entrada

Un pin GPIO de entrada solo debe experimentar  niveles de voltaje de 0V a 3.3V máximo.   Se debe tener cuidado al momento de conectarse a otros circuitos que utilicen lógica TTL donde se utilizan 5V.  Se puede dañar el SoC ya que no es tolerante a sobretensiones.  Los diseños de los circuitos de entrada deben de estar bien diseñados para prevenir que los GPIO de entrada no experimenten un potencial de entrada negativa.

## Pines de salida


Al utilizar un pin GPIO como salida el usuario debe tener en mente la limitación de corriente.  Raspberry Pi no provee limitación de corriente.  Cuando un pin de salida está en un estado ALTO, como una fuente de voltaje, trata de suministrar 3.3 V (dentro los límites de un transistor).  Si la salida está conectada a la tierra, en el peor de los casos, entonces toda la corriente que se puede suministrar fluirá. Esto causara daño permanente.

## Configuración GPIO
Para poder utilizar la los pines GPIO se tiene que descargar la biblioteca GPIO de Python.  La biblioteca RPi.GPIO de Python permite crear y configurar con facilidad un script para poder leer-escribir a los pines de entrada o salida de la cabecera GPIO.  Hay varias bibliotecas disponibles pero se recomienda utilizar la biblioteca que se encuentra en el sitio https://pypi.python.org/pypi/RPi.GPIO. Al tiempo de escritura la versión actual de la biblioteca es la 0.6.2. Hay diferentes formas de hacerlo aquí se demostrara una de ellas. 

1.	Abrir una terminal nueva.
2.	Actualizar la lista de repositorios con el comando:
  3.	 ``` $ sudo apt-get update ```
3.	Instalar el paquete python-dev:  
  4.	 ``` $ sudo apt-get python-dev ```
4.	Escribir el siguiente comando para descargar la biblioteca RPi.GPIO en el directorio principal.  Si hay una nueva versión disponible solo se tiene que cambiar el número de la versión con el de la más reciente: 
  5.	``` $ wget http://pypi.python.org/packages/source/R/RPi.GPIO/RPi.GPIO-0.6.2.tar.gz ```
5.	Extraer los contenidos del archivo descargado: 
  6.	``` $  tar xvzf RPi.GPIO-0.6.2.tar.gz ```
6.	Cambiar al nuevo directorio creado, si es que hay una nueva versión recordar cambiar el número de versión a la versión que se descargó:  
  7.	``` $ cd RPi.GPIO-0.6.2 ```
7.	Instalar la biblioteca a Python. 
  8.	``` $ sudo python setup.py install ```
8.	Una vez terminado el proceso se remueve el directorio y su contenido: 
  9.	``` $ cd ```
  10.	``` $ sudo rm RPi.GPIO-0.6.2/ ```
9.	Borrar el archivo descargado:
  10.	``` $  rm Rpi.GPIO-0.6.2.tar.gz ```
	
Ahora la biblioteca de GPIO está instalada en Python y puede ser utilizada en un script pero no está cargada por defecto. Para poder utilizar la biblioteca en Python se debe empezar un programa con ``` 
Rpi.GPIO as GPIO``` en la cabecera del archivo.  



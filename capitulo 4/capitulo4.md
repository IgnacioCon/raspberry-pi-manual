# Capítulo 4: "¡Hola, Mundo!" con Raspberry Pi

## 4.1 Proyecto
Ahora que contamos con una Raspberry Pi configurada y lista para trabajar con los pines GPIO es tiempo de realizar un proyecto.  Este proyecto es sencillo, el “¡Hola, Mundo!” de la Raspberry Pi.  El gran reto será hacer que un LED parpadee puede sonar algo trivial pero no lo es.

## 4.2 Material
* Raspberry Pi
* LED
* Resistencia de 330 ohm
* Cables para conectar el circuito 
* Placa de prototipo sin soldar
* Cable hembra-macho para conectar pines GPIO a la placa



Los pines GPIO están conectados directamente a los pines del CPU en la Raspberry Pi así que no existe algún tipo de protección y se debe tener mucho cuidado.  Se utilizara una placa de prototipo sin soldar para crear el circuito.  En la figura 4.1 se puede ver el circuito que se creara.  El pin 7 de la Raspberry Pi está conectado al final positivo del circuito mientras que el pin 6 el cual es tierra (GND) está conectado al lado negativo del circuito.


![figura4.1](images/circuit.jpg)
###### Figura 4.1 Circuito a implementar.


Con el conocimiento de cómo se armara el circuito se procede a implementarlo. La figura 4.2 muestra el circuito armado en la placa de prototipo.  Con el circuito implementado ahora se puede proceder programar los pines GPIO.

![](images/ledoff.JPG)
###### Figura 4.2 Circuito implementado.


## 4.3 Código 
En esta parte del proyecto se desarrollara el código que nos permitirá controlar los pines GPIO.  Este programa lograra que el LED parpadee de forma continua y así crear el “¡Hola, Mundo!” de Raspberry Pi.  A lo largo de esta sección se es estará explicando detalladamente las partes del código de arriba hacia abajo. Esto con el fin de que el usuario pueda entender el código y que es lo que se está haciendo.

#### 4.3.1 Importar el módulo RPi.GPIO
El paquete RPi,GPIO que se instaló en el capítulo 3 nos permite controlar los pines GPIO a través de clases.  Para poder utilizar este módulo debemos importarlo en la cabecera del código que se está desarrollando. Esto se hace escribiendo al principio del archivo:

```python
import RPi.GPIO as GPIO
```

Esto nos permite referirnos al módulo con solo escribir GPIO y no todo el nombre de RPi. GPIO.

#### 4.3.2 Especificar el modo de operación
Lo siguiente es especificar en qué modo de operación se usara el módulo GPIO.  Se tiene que tener en cuenta que la Raspberry Pi y el CPU tienen diferentes números de pines.  Es por eso que es muy importante designar que modo se usara. Existen dos modos de operación.  El modo BOARD, que utiliza el sistema de numeración de pines de la Raspberry Pi. El modo BCM que utiliza el sistema de numeración del CPU.  En nuestro código es donde especificamos que modo se va a usar simplemente con escribir:

```python
GPIO.setmode(GPIO.BOARD) # para usar numeración Raspberry Pi
  # o
GPIO.setmode(GPIO.BCM)   # para usar numeración CPU
```


#### 4.3.3 Crear un canal
Ahora se tiene que crear un canal ya sea como entrada o salida.  Esto se puede hacer escribiendo dentro de nuestro código:

```python
GPIO.setup(canal, GPIO.IN)   # canal de entrada
  # o
GPIO.setup(canal, GPIO.OUT)  # canal de salida
```

Donde canal es una variable que contiene el número del pin que se usara.  En este caso, el LED se conectó al pin 7 de la Raspberry Pi. Esto significa que se debe configurar ese pin como un canal de salida.  Si es que se utiliza el modo BCM, el pin 7 esta como el GPIO4 en el CPU.  Esto es lo que se debe agregar al código:

```python
GPIO.setup(7, GPIO.OUT)  # si modo BOARD es usado
  # o 
GPIO.setup(4, GPIO.OUT)  # si modo BCM es usado
```

**Nota: se recomienda utilizar el sistema de numeración de la Raspberry Pi (BOARD) ya que es más fácil de seguir y utilizar.  Aunque no importa mucho cual sistema se utiliza si es importante ser consistente y utilizarlo en todo el proyecto.**

#### 4.3.4 Conducir un canal
Lo que sigue es conducir el canal que se utilizara a ALTO o BAJO.  Esto se puede hacer de una de las tres formas, cualquiera de las tres es válida:

```python
GPIO.output(7,True)
  # o
GPIO.output(7, GPIO.HIGH)
  # o
GPIO.output(7, 1)
```

Para conducir el mismo pin 7 a BAJO se puede utilizar cualquiera de los tres comandos:

```python
GPIO.output(7, False)
   # o
GPIO.output(7, GPIO.LOW)
   # o
GPIO.output(7, 0)
```

#### 4.3.5 Leer un canal
Para leer el valor de cualquier pin GPIO se utiliza:

```python
GPIO.input(canal)
```

Donde canal es el canal que se quiere leer.  

#### 4.3.6 Limpiar
Una vez que se terminen todas las operaciones del módulo GPIO se debe de limpiar y liberar los recursos utilizados por el programa.  No es necesario hacer esto pero si una buena costumbre de programación. 

```python
GPIO.cleanup()
```

#### 4.3.7 Una consideración sobre el tiempo

Otra cosa que se debe considerar es el concepto de retraso.  Al momento de que el LED parpadee se quiere ver que parpadee.  No debería de parpadear tan rápido o tan lento que no se pueda apreciar el momento en el que enciende y apaga.  Para poder lograr esto se debe controlar el tiempo en el que el LED pasa encendido y apagado.  Python tiene una biblioteca “time” la cual contiene una función sleep() que ayudara a cumplir este objetivo.  Para poder utilizarla se debe importar de misma forma que RPi.GPIO.  

```python
import time    # importar la biblioteca "time"
time.sleep(n)  # dormir por n segundos
```

Con estos conceptos se puede codificar el programa para controlar los pines GPIO y hacer que el LED parpadee.  

#### 4.3.8 Programa

Aplicando los conceptos previamente explicados se codifica el siguiente programa en un editor de texto en la Raspberry Pi.  El siguiente paso es abrir un editor de texto y escribir el siguiente programa.  **Nota: el archivo debe ser guardado con la extensión .py la cual significa que es un programa de Python.  Para este ejemplo se nombró el archivo blink.py** 
```python
import RPi.GPIO as GPIO         # importar biblioteca RPi.GPIO
import time                     # importar biblioteca "time" para la funcion sleep()
 
pin = 7                         # pin 7 es el pin que se utiliza
GPIO.setmode(GPIO.BOARD)        # usar modo BOARD
GPIO.setup(pin, GPIO.OUT)       # poner el pin 7 como salida
 
while True:                     # bucle infinito, presionar ctrl + c en terminal para cerrar
    GPIO.output(pin, GPIO.HIGH) # enciende GPIO pin (ALTO)
    time.sleep(1)               # esperar 1 segundo
    GPIO.output(pin, GPIO.LOW)  # apagar pin GPIO (BAJO)
    time.sleep(1)               # esperar 1 seguno
 
GPIO.cleanup()                  # limpiar y liberar recursos utilizados
```

#### 4.3.9 Correr el programa 
El usuario debe de abrir una terminal nueva y moverse al directorio donde se guardó el archivo donde se codifico el programa.  Una vez que se encuentre en el directorio correcto  se corre el programa con el siguiente comando:

```bash
$ sudo python nombre_del_programa.py
```

Si el programa está escrito correctamente y todas las conexiones están correctas el LED debería de encender y apagar.  Si no, verifiqué que el código este correcto y que las conexiones estén bien.  La figura 4.3 muestra el resultado cuando todo está funcionando correctamente.  ¡Hola, Mundo! 

![](images/ledon.JPG)
###### Figura 4.3 LED encendido.



## 4.4 Resumen  
En este capítulo se desarrolla el primer proyecto con la Raspberry Pi. Un simple y sencillo proyecto, el “Hola, Mundo!” de la Raspberry Pi.  Aunque parezca simple este proyecto tiene muchos conceptos útiles que sirven como base para proyectos más complejos.  Se explica la estructura de un código de Python y como es que se utiliza el módulo RPi.GPIO para usar los pines GPIO.  La figura 4.4 muestra el resultado final de este proyecto.


![](images/fullset.JPG)
###### Figura 4.4 ¡Hola, Mundo! de Raspberry Pi.

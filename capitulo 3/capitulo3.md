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
# SISTEMAS DIGITALES
## Apuntes de clase

**Asignatura:** Sistemas Digitales

---

# Índice

1. [Primera clase: Introducción a los sistemas digitales](#1-primera-clase-introducción-a-los-sistemas-digitales)
2. [Segunda clase: Buses, arquitecturas, memorias y periféricos](#2-segunda-clase-buses-arquitecturas-memorias-y-periféricos)
3. [Tercera clase: Registros y operaciones con pines](#3-tercera-clase-registros-y-operaciones-con-pines)
4. [Cuarta clase: Del AVR al ESP32](#4-cuarta-clase-del-avr-al-esp32)
5. [Quinta clase: Comunicación UART, SPI y características del ESP32](#5-quinta-clase-comunicación-uart-spi-y-características-del-esp32)
6. [Sexta clase: Temporizadores de hardware en el ESP32](#6-sexta-clase-temporizadores-de-hardware-en-el-esp32)
7. [Séptima clase: Sondeo e interrupciones](#7-séptima-clase-sondeo-e-interrupciones)
8. [Declaración de uso de inteligencia artificial](#declaración-de-uso-de-inteligencia-artificial)

---

# 1. Primera clase: Introducción a los sistemas digitales

## 1.1. Conceptos fundamentales

| Concepto | Descripción |
|---|---|
| Sistema embebido | Sistema que puede ejecutar una tarea en tiempo real. |
| Microcontrolador | Computadora que cumple con una función. Ejemplos: memoria SRAM y periféricos de entrada/salida (E/S). |
| Microprocesador | Solo es el CPU; los componentes externos se conectan a él. Ejemplo: memoria RAM. |

## 1.2. Fundamentos de los sistemas digitales

- Todo nace de un transistor.
- Depende de la información de la *datasheet* para saber si nos devuelve un 0 lógico o un 1 lógico.

## 1.3. Microprocesadores y microcontroladores

| Característica | Microprocesadores | Microcontroladores |
|---|---|---|
| Bits de trabajo | 64 bits | 8, 16 y 32 bits |
| Referencia | CPU | Registros de memoria |

---

# 2. Segunda clase: Buses, arquitecturas, memorias y periféricos

## 2.1. Tipos de buses

| Bus | Función | Dirección |
|---|---|---|
| Bus de direcciones | Indica qué casillero se va a utilizar. | Hacia afuera. |
| Bus de datos | Transporta el contenido que se va a llevar. | Ambos sentidos. |
| Bus de control | Utiliza 1 o 2 cables que permiten leer o escribir. | Señales sueltas. |

## 2.2. Arquitecturas de Von Neumann y Harvard

| Característica | Von Neumann | Harvard |
|---|---|---|
| Buses | Tiene un bus de datos que se utiliza una sola vez. | Tiene varios buses. |
| Instrucciones y datos | Las instrucciones y los datos se traen por turnos mediante el mismo bus. | Tiene un bus para ingresar a la memoria de programa y otro para ingresar a la memoria de datos. |

## 2.3. Tipos de memoria

| Memoria | Características | Uso |
|---|---|---|
| Flash | No se borra. Se reescribe al subir un programa. | Almacena el programa que ejecutamos. |
| SRAM | Se borra, es rápida y pequeña. | Guarda las variables mientras el programa corre. |
| EEPROM | No se borra. | Guarda pocos datos que el programa cambia y que deben sobrevivir al apagado. |

### Datos importantes

| Elemento | Valor o característica |
|---|---|
| Tamaño de un `int` | 2 bytes. |
| Ciclos de escritura de Flash | 10 000 ciclos. |
| Ciclos de escritura de EEPROM | 100 000 ciclos. |

## 2.4. Periféricos

| Periférico | Función |
|---|---|
| GPIO | Poner un pin en 0 o 1, o leerlo. |
| Timer | Contar pulsos para medir tiempo. |
| Interrupción | Avisar a la CPU que algo pasó. |
| ADC | Convierte voltaje en número. Ejemplo: sensor LM35. |
| DAC | Convierte número en voltaje. |
| PWM | Encender y apagar rápidamente. Ejemplo: servo. |
| UART | Comunicación serial por 2 cables (TX, RX). |
| I2C | Bus de 2 cables con direcciones. |
| SPI | Bus rápido de 4 cables. |

## 2.5. Comparación entre ATmega328P y ESP32

### ATmega328P

| Característica | Descripción |
|---|---|
| Fabricante | Microchip. |
| Placa típica | Arduino Uno. |
| Bits y núcleos | 8 bits y 1 núcleo. |
| Reloj | 16 MHz en el Uno. |
| Voltaje | 5 V. |
| Wi-Fi y Bluetooth | No. |
| Uso en el curso | Semana 1, en simulación. |

### ESP32

| Característica | Descripción |
|---|---|
| Fabricante | Espressif. |
| Placa | ESP32 DevKit V1. |
| Bits y núcleos | 32 bits y 2 núcleos. |
| Reloj | 240 MHz. |
| Voltaje | 3.3 V. |
| Wi-Fi y Bluetooth | Sí. |
| Uso en el curso | Semana 2 a 16. |

## 2.6. Criterios para seleccionar un microcontrolador

- ¿Necesitamos Wi-Fi?
- ¿Cuántos pines y cuánta memoria?
- ¿De dónde sale la energía?

## 2.7. Bits, operaciones bit a bit y E/S mapeada en memoria

### Valores registrados en clase

```text
5, 32, 0x81, 255
```

### Niveles lógicos del ESP32

| Nivel | Rango de voltaje |
|---|---|
| Bajo | 0 - 0.8 V |
| Alto | 2.5 - 3.3 V |

### Representación binaria

```text
1000 0001
```

### Operaciones bit a bit

| Operación | Funcionamiento |
|---|---|
| AND | 1 si ambos son 1. |
| OR | 1 si alguno es 1. |
| XOR | 1 si son distintos. |
| NOT | Invierte. |

---

# 3. Tercera clase: Registros y operaciones con pines

## 3.1. Registros del puerto B

| Registro | Función |
|---|---|
| DDRB | Configura los pines: 0 = entrada, 1 = salida. |
| PORTB | En salida: establece el valor que sale. En entrada: activa la resistencia pull-up. |
| PINB | Permite leer el voltaje real del pin: 1 significa que está alto y 0 significa que está bajo. |

### Funcionamiento de PORTB

| Configuración | Comportamiento |
|---|---|
| 0 | 0 V. |
| 1 | 5 V. |

## 3.2. Alta impedancia

La alta impedancia significa que el pin está flotando (aislar).

- Sirve para conectar sensores principalmente.
- Se utiliza para sensores frágiles (analógicos), en los cuales cualquier ruido puede cambiar el voltaje.

## 3.3. Bits, bytes y dígitos hexadecimales

| Concepto | Descripción |
|---|---|
| Bit | Es un nivel de voltaje. |
| Byte | Son 8 bits. |
| Dígito hexadecimal | Son 4 bits. |

## 3.4. Operaciones bit a bit

Las operaciones bit a bit aplican AND, OR, XOR y NOT columna por columna.

### Máscaras de bits

Con una máscara:

```c
1 << n
```

Se puede tocar un solo bit sin cambiar los demás.

## 3.5. Control de periféricos mediante registros

- Los periféricos se controlan con registros que tienen dirección, como la memoria.
- DDR elige entrada o salida.
- PORT pone el valor.
- PIN lee el pin.

### Resumen de los registros

| Registro | Acción principal |
|---|---|
| DDR | Elegir entrada o salida. |
| PORT | Poner el valor. |
| PIN | Leer el pin. |

---

# 4. Cuarta clase: Del AVR al ESP32

## 4.1. Registros y periféricos

- Existen 2 tipos de registros: memoria y periféricos.
- Un periférico es un circuito interno que cumple una función específica.
- Un pin es una conexión física entre el mundo exterior y el circuito interior del microcontrolador.

## 4.2. Multiplexor

Circuito combinacional que recibe múltiples señales de entrada y permite transmitir una sola de ellas hacia una única salida.

## 4.3. GPIO

GPIO significa entrada y salidas de propósito general.

## 4.4. Registros W1TS y W1TC

| Registro | Función |
|---|---|
| W1TS | Setear los 1. |
| W1TC | Clear, limpia ese 1, apagar. |

## 4.5. Temas abordados en clase

- Cómo funcionan los pines y periféricos.
- Cómo se relacionan W1TS y W1TC con el problema.

---

# 5. Quinta clase: Comunicación UART, SPI y características del ESP32

## 5.1. Comunicación UART

UART es un protocolo que permite al microcontrolador enviar y recibir datos con otros dispositivos.

## 5.2. Alimentación del ESP32

| Pin | Característica |
|---|---|
| VIN | Sin regular. |
| 3V3 | Regulada. |

## 5.3. Pines Strapping

Strapping: lee los pines que se deben encender cuando se enciende el ESP32.

| GPIO | Condición o característica |
|---|---|
| GPIO0 | En bajo al arrancar: modo de carga. Es el botón BOOT. |
| GPIO2 | Debe estar en bajo o al aire para cargar. Suele tener el LED azul de la placa. |
| GPIO12 | En alto al arrancar: Flash a 3.3 V. La placa no arranca. |

## 5.4. Cálculo de corriente del LED

Datos registrados:

- LED rojo.
- Resistencia de 330 ohmios.
- Voltaje de alimentación: 3.3 V.
- Voltaje del LED (Vf): 2.0 V.

Cálculo:

```text
(3.3 - 2.0) / 330 = 4 mA
```

Fórmula:

```text
R = (3.3 V - Vf) / I
```

**Observación:** La carga determina la corriente.

## 5.5. Comunicación SPI

SPI es un protocolo de comunicación que permite al microcontrolador conectarse con dispositivos externos.

### Pines relacionados con la memoria Flash

- GPIO6 al GPIO11 sirven para conectar de forma interna el microcontrolador a la memoria Flash SPI que almacena el programa.

## 5.6. Bootloader ROM

El Bootloader ROM arranca el sistema.

## 5.7. Deep Sleep

Si no tiene tareas, da vueltas en modo ahorro de energía para no gastar.

---

# 6. Sexta clase: Temporizadores de hardware en el ESP32

## 6.1. Características generales

- Temporizadores de hardware en el ESP32.
- Del GPIO34 al GPIO39 solo nos sirven como entrada.

## 6.2. Conceptos fundamentales de temporizadores

| Concepto | Descripción |
|---|---|
| Temporizador | Circuito dentro del microcontrolador que cuenta pulsos de reloj. |
| Periférico | Circuito dentro del microcontrolador. |
| Contador | Es un registro del temporizador. |
| Registro | Espacio pequeño de almacenamiento de bits. |
| Reloj | Señal que sube y baja a ritmo fijo. Cada subida es un pulso. |

### Representación de una señal de reloj

```text
_|-|_|-
```

## 6.3. Bus APB

APB significa Advanced Peripheral Bus.

- Es el bus de periféricos del ESP32.
- Frecuencia: 80 MHz.
- No todos los ESP32 trabajan a esos MHz.

### Características de 80 MHz

| Característica | Valor |
|---|---|
| Frecuencia | 80 MHz. |
| Pulsos por segundo | 80 millones. |
| Duración de cada pulso | 12.5 ns. |

## 6.4. Prescaler, resolución y ticks

| Concepto | Descripción |
|---|---|
| Prescaler | Divide la velocidad del contador. |
| Resolución | Lo que dura un tick. Es el tiempo más pequeño que el temporizador puede distinguir. |
| Ticks | Cantidad de pulsos. |

### Fórmula de resolución

```text
r = 1 / f
```

Donde:

- `r`: resolución.
- `f`: frecuencia.

## 6.5. Alarma del temporizador

La alarma es un número que se guarda en un registro. Cuando el contador lo alcanza, el temporizador genera un aviso.

### Fórmulas

```text
tiempo = alarma * resolución
```

Despejando:

```text
alarma = tiempo * f
```

Otra expresión registrada para el prescaler:

```text
prescaler: 8000 / f
```

## 6.6. Ejercicio de cálculo de ticks

Datos:

- 10 000 ticks por segundo.
- Alarma que suene en 2500 ticks.
- Calcular la resolución.

Cálculo registrado:

```text
r = 1 / 10000
r = 0.0001
r = 1 ms = 100 micro s
```

## 6.7. Autorecarga y desbordamiento

| Concepto | Descripción |
|---|---|
| Autorecarga | El aviso se repite solo. El contador se compara con la alarma y vuelve a 0. |
| Desbordamiento | Es la capacidad que tiene de almacenar esa información. Nosotros lo elegimos. Vuelve a 0 sin llegar a la alarma. |

## 6.8. Características de los temporizadores del ESP32

| Característica | Descripción |
|---|---|
| Cantidad de timers | 4. |
| Capacidad | Todos de 64 bits. |
| Prescaler | De 16 bits. |
| Grupos | TIMG0, TIMG0. |
| Rango del prescaler | De 2 a 65 535 en ESP32. |

### Pregunta registrada en clase

¿Cuál es el límite del controlador?

## 6.9. API y Core

### API

Conjunto de funciones que alguien ya programó para que uno las use sin saber cómo están hechas por dentro.

- Llama a una función.
- El API calcula el prescaler y la alarma.
- Registros del temporizador: guarda los valores y habilita el contador.

### Core

Paquete de software que se instala en el Arduino IDE para programar una placa concreta.

- Trae compilador.
- Trae la API para esa placa.

## 6.10. Interrupciones y funciones relacionadas

| Concepto | Descripción |
|---|---|
| Interrupción | Señal que manda un periférico a la CPU para decirle que se detenga porque algo pasó. |
| ISR | Rutina de servicio de interrupción. |
| Callback | Función que tú escribes, pero no llamas tú. |
| IRAM_ATTR | Guardar la ISR donde siempre esté a la mano. |
| IRAM | Memoria interna rápida para instrucciones, dentro del ESP32 siempre disponible. |

### Volátil

Volátil: traduce el código a instrucciones del chip y toma atajos para que el programa sea más rápido.

### Patrón bandera

```text
Patrón bandera
```

---

# 7. Séptima clase: Sondeo e interrupciones

## 7.1. Sondeo e interrupciones

| Concepto | Descripción |
|---|---|
| Sondeo (Polling) | Preguntar una y otra vez, voy a ver si llegó. |
| Interrupción | Es cuando te avisan. Está definido: suena el timbre, vas a abrir y vuelves a lo tuyo. Se atiende y se siguen las instrucciones. |
| Interrupción externa | El circuito está trabajando, alguien aplasta el botón y se interrumpe el programa. No está definido. |

## 7.2. ISR

ISR es la función que se ejecuta al llegar el aviso; la llama el hardware.

## 7.3. Flancos y niveles

- Flanco: constante de una señal que cambia de 1 a 0 o de 0 a 1.
- Nivel: es el tiempo que tarda en cambiar de estado.
- Flanco es la respuesta que se da en ese momento.

### Tipos de flancos

| Modo | Funcionamiento |
|---|---|
| Rising | Cambio de 0 a 1. |
| Falling | Cambio de 1 a 0. |
| Change | Detecta los 2 estados. |

## 7.4. Watchdog

Watchdog (perro guardián): reinicia el chip si algo se queda trabado mucho tiempo.

## 7.5. Periférico encargado de vigilar el pin

El periférico GPIO es el encargado de vigilar el pin.

## 7.6. Pines del ESP32

| Pines GPIO | Características |
|---|---|
| GPIO16 al GPIO33 | Sirven para interrupciones. |
| GPIO34 al GPIO39 | Solo entrada, con cuidado; no tienen pull-up interna. |
| GPIO0, GPIO2, GPIO5, GPIO12 y GPIO15 | Pines Strapping. Evitar si están presionados al encender, porque el chip arranca mal. |
| GPIO6 al GPIO11 | Son de la Flash. No utilizarlos; los usa la memoria del programa. Son los canales de comunicación con la CPU. |

### Consideraciones para utilizar interrupciones

- Primero activo el `INPUT_PULLUP` y luego la interrupción.
- Guardar datos en la memoria Flash es igual a que se apague el caché.
- La información debe quedar en la memoria SRAM.

## 7.7. Memoria e interrupciones

Cuando hay una interrupción:

- La CPU se va a la SRAM y lee la IRAM, que contiene las instrucciones.

---

# Declaración de uso de inteligencia artificial

Se utilizó inteligencia artificial como herramienta de apoyo para organizar, estructurar y dar formato a los apuntes recopilados durante las clases de la asignatura de Sistemas Digitales. Su utilización se limitó a mejorar la presentación de la información mediante encabezados, tablas y organización del contenido, conservando la información original registrada en clase.

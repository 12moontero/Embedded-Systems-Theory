
# SDK: C/C++ Básico para Sistemas Embebidos

La programación en C++ para embebidos no es "escribir código", es **gestionar recursos limitados**. Aquí no hay espacio para errores; cada bit cuenta.

## Indice

- **1.** ¿Qué es C/C++ embebido
- **2.** Normas de C/C++
- **3.** Estructura embebida
---

## **1.** ¿Que es C/C++ embebido?

Primero de todo C/C++ es uno de los lenguajes mas potentes y rapidos que existe actualmente. A eso se la llama lenguaje de bajo nivel que signigica que no se parece al idioma del ser humano. Mira esta imagen para que entiendas como se diferencia los lenguajes de programaccion.:

![imagen Visual Guia](https://raw.githubusercontent.com/12moontero/Embedded-Systems-Theory/refs/heads/main/02-C-Language/assets/GU%C3%8DA%20NIVEL%20DE%20LENGUAJES.png)

Lo que vas a aprender es el 20% - 30% de lo que es en realidad C/C++, lo que voy a enseñar aqui es todo eso poco a poco, para no perderte.

## **2.** Normas de C/C++

Estas son las normas mas importantes de este lenguaje de programaccion, si no te saltara error.

#### 1. La regla del punto y coma (;)
Toda instruccion simple debe terminar obligatoriamente con ;.
- ✅ **SE USA** en Declaración de variables, llamadas a funciones y retornos.
- ❌ **NO SE USA** en `#include`, `#define`, funciones `(void ...())`, ni estructuras de control (if, while, for).

#### 2. La regla del punto y coma (;)
Todo bloque de código debe ir delimitado por { }.
- Aunque un if solo tenga una línea, pon las llaves siempre. Esto evita errores críticos cuando añadas más lógica en el futuro

## **3.** Estructura embebida

Todo lenguaje de programaccion tiene una estructura. Antes de todo en un codigo siempre lo va a leer de arriba abajo tenlo en cuenta. En C/C++ es esta:

**1. librerias:**

Simepre se empieza poniendo las librerias que vas a usar en todo el codigo se pone al princpio porque va a ser lo primero que va a leer.


Cuando quieras añadir una libreria entrada/salida simepre se pone depues del #include con signos de mayor y menor < ... >   
` #include <stdio.h> `  

Cuando quieras poner una libreria tuya propia se pone despues del #inlude con comillas "..."   
`#include "pico/stdlib.h"`

**2. Definiciones:**

Esta zona es donde vamos a poner las constantes que vamos a usar de hardware.

Se pone siempre esta estructura solo que cambaindo lo que vas a usar y los nombres de las variables que quieras.

const uint [Nombre de variable] = [Lo que quieras que va dentro] ;  
Ej: `const uint PIN_LED_ROJO = 14;`

Puedes definir lo que quieras


**3. int main:**

La definición de `int main() {}` es la función que siempre debe estar obligatoriamente.

Siempre en el `int main() {}` pondrás lo que vas a usar, lo que quieres, como variables, resistencias internas y todo eso. 
Definirás lo que quieres que sea salida/entrada en los pines.

Pondrás esto:

   gpio_init(PIN_LED_BLUE);  
   gpio_init(PIN_LED_RED);  
   gpio_init(PIN_BOTTON);

   gpio_set_dir(PIN_LED_BLUE, GPIO_OUT);  
   gpio_set_dir(PIN_LED_RED, GPIO_OUT);  
   gpio_set_dir(PIN_BOTTON, GPIO_IN);

Básicamente, hay como dos zonas, donde dices que vas a usar como los pines, si no pones esto, no sabrá qué pines usar.

Y la otra zona, la de abajo, que básicamente dices si la placa lo quiere como entrada para leer o de salida para sacar la electricidad.

- OUT ---- Salida  // Para encender LEDs, dar energía a sensores
- IN  ---- Entrada // Para leer sensores, botones...

**3. Bucle  `while`**

Dentro del `int main() {}` siempre hay un bucle, esto es obligatorio poner.

Cuando ya has definido todo lo que tenías que poner, toca ahora poner el bucle donde se va a repetir todo el rato lo que quieras.

Normalmente se ponen los if, elif, else y todo lo que quieres que se repita todo el rato.

Ejemplo:

    while (true) {
        bool boton = gpio_get(PIN_BOTTON);

        if (boton == true) {
            gpio_put(PIN_LED_BLUE, 1);
            gpio_put(PIN_LED_RED, 0);
            sleep_ms(120);

            gpio_put(PIN_LED_BLUE, 0);
            gpio_put(PIN_LED_RED, 1);
            sleep_ms(120);
        } else {
            gpio_put(PIN_LED_BLUE, 0);
            gpio_put(PIN_LED_RED, 0);
            sleep_ms(20);
        }
    }

En este código, básicamente estás diciendo que haga una sirena de policia.

Usando if y else para que cuando pulses el botón, se enciendan las luces y cuando sueltes, se apaguen.

Cuando pones todo esto, se termina así de simple.

## Todo el codigo aquí:

    #include <stdio.h>
    #include "pico/stdlib.h"

    const uint PIN_LED_BLUE = 12;
    const uint PIN_LED_RED = 13;
    const uint PIN_BOTTON = 14;

    int main() {
        stdio_init_all();

        gpio_init(PIN_LED_BLUE);
        gpio_init(PIN_LED_RED);
        gpio_init(PIN_BOTTON);

        gpio_set_dir(PIN_LED_BLUE, GPIO_OUT);
        gpio_set_dir(PIN_LED_RED, GPIO_OUT);
        gpio_set_dir(PIN_BOTTON, GPIO_IN);          

        gpio_set_pulls(PIN_BOTTON, false, true);

        while (true) {
            bool boton = gpio_get(PIN_BOTTON);

            if (boton == true) {
                gpio_put(PIN_LED_BLUE, 1);
                gpio_put(PIN_LED_RED, 0);
                sleep_ms(120);

                gpio_put(PIN_LED_BLUE, 0);
                gpio_put(PIN_LED_RED, 1);
                sleep_ms(120);
            } else {
                gpio_put(PIN_LED_BLUE, 0);
                gpio_put(PIN_LED_RED, 0);
                sleep_ms(20);
            }
        }
    } 


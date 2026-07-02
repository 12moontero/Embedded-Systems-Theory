# El Procesador

## Índice

**1.** ¿Qué es un Procesador?    
**2.** Arquitectura Interna - Registros   
**3.** Bus de Datos  

## **1.** ¿Qué es un Procesador?

Imagínate que es una persona que tiene mucha información y lo que hace es:  
* **Copiar** información.
* **Trabajar** (procesar) esa información.
* **Soltar** el resultado final.

En diferentes velocidades, pero antes de enseñarte qué velocidades hay, quiero que veas una cosa para que no te líes desde el principio, que es qué lleva por dentro.

## **2.** Arquitectura Interna - Registros

Un procesador tiene contenido dentro que se llaman **registros** pero para nosotros lo llamaremos estanterias.

Los registros son **estanterías fijas** dentro de la CPU donde se guardan los datos para trabajar. No se mueven; lo que cambia es su contenido (se copia y se sobrescribe).

![Registro](https://raw.githubusercontent.com/12moontero/Embedded-Systems-Theory/refs/heads/main/01-Hardware-Basics/assets/Registro.png)     
![Concepto-CPU](https://raw.githubusercontent.com/12moontero/Embedded-Systems-Theory/refs/heads/main/01-Hardware-Basics/assets/Concepto-CPU.png)

### ¿Cómo funcionan los bits?
Un registro tiene un tamaño fijo. Ese tamaño determina cuánta información puede "copiar" de una sola vez:

| Tipo | Capacidad | Significado |
| :--- | :--- | :--- |
| **32 bits** | 32 "bolas" | Mueve 32 piezas de información por turno. |
| **64 bits** | 64 "bolas" | Mueve 64 piezas de información por turno. |

> **Importante:** El tamaño del registro es fijo por diseño. Un procesador de 32 bits **siempre** copia información de 32 en 32. Ni más, ni menos.


## **3.** Bus de Datos

El **Bus de Datos** es el peaje por donde viajan las bolas (bits) de información. El número de carriles de este peaje es exactamente el mismo que con el tamaño de los registros.

![Bus de datos](https://raw.githubusercontent.com/12moontero/Embedded-Systems-Theory/refs/heads/main/01-Hardware-Basics/assets/BUS-datos-Dise%C3%B1o.png)

Existen dos tipos de buses:

*  **Bus Interno:** Conexiones dentro del procesador. Se encarga de mover datos entre los registros y la unidad de cálculo (ALU).

*  **Bus Externo:** Son las líneas de cobre, que ves en la placa (PCB). Conectan el procesador con lo exterior: memoria RAM, sensores y pines GPIO.

### Resumen del proceso
El procesador nunca mueve las "estanterías" (registros), **copia** los datos que contienen y los lanza a los buses para que lleguen a su destino.

# README.md

¿Qué es esto?

Un script en C simple para entender cómo se puede codificar y decodificar un payload (shellcode) usando XOR con clave de 1 byte. El ejemplo incluye un shellcode simulado que abre la calculadora de Windows (`calc.exe`).
La idea es que veas cómo funciona la ofuscación con XOR, que es un método clásico para evitar detecciones básicas y proteger tu código.

¿Cómo funciona?

1. El script tiene un array con un shellcode acotado (simulado).
2. Se imprime el shellcode original en consola, en formato hexadecimal.
3. Se codifica el shellcode con XOR usando una clave fija de 1 byte.
4. Se muestra el shellcode codificado, para que veas cómo queda ofuscado.
5. Se decodifica nuevamente con XOR (igual que codificar, por la simetría).
6. Se muestra el shellcode decodificado, listo para usar o ejecutar.
7. Opcionalmente, se puede ejecutar el shellcode para abrir la calculadora (líneas comentadas para que lo hagas bajo tu propio riesgo).

Requisitos

* Compilador C para Windows (Visual Studio, MinGW, etc).
* Conocimientos básicos de C y sistemas Windows.
* Entorno seguro para probar código que ejecuta shellcodes.


Cómo compilar y correr

Con MinGW, por ejemplo:
gcc xor_encoder_decoder.c -o xor_encoder_decoder.exe
./xor_encoder_decoder.exe


Advertencias

* Ejecutar shellcodes puede ser peligroso. Solo correr en ambientes controlados.
* Este código es para fines educativos y experimentales.
* No usar en máquinas productivas ni sin autorización.

¿Querés aprender más?
Hecho con paciencia, mate y teclado.

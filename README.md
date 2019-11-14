# Tarea Programada: Pipeline.

---
##### Escuela de Ciencias de la Computación e Informática, UCR.

##### Curso del proyecto: Programación II.

##### Equipo de trabajo:

* ##### Jorge Isaac Porras Rojas
* ##### Jorge Paolo Arellano Maroto

##### Año: 2019.

---

## Descripción General:

El objetivo del proyecto es crear un juego en terminal de comandos que se asemeja
al videojuego "Pipe Mania" o sus diversas variantes como "Pipe Dreams" donde una
matriz que representa el sistema de tuberías es dada al usuario y esta debe
generar un recorrido desde uno o varios puntos de inicio hasta una o varias salidas,
sin que existan fugas en el camino.

En esta versión del juego el usuario es capaz de dar comandos para efectuar alguna de
las operaciones fundamentales del programa: **Validar el juego dado, resolverlo o
convertirlo.**

Así mismo puede elegir cómo interpretar las entradas (ya sea en forma textual o
en binario) y de dónde tomarlas (de un archivo dado o de la entrada estándar). Las
mismas opciones están disponibles para la salida, añadiendo la opción de mostrar
las salidas de la misma manera en que se indicó la entrada.

Más detalles sobre el programa pueden ser encontrados en
[este enlace](http://jeisson.ecci.ucr.ac.cr/progra2/2019b/proyectos/pipe_leak/ "Fuga en la tubería").

---
#  Manual del desarollador:
## Análisis:

En esta sección se proveen ideas adicionales para ahondar el análisis del programa
y adapatarlo al consecuente diseño e implementación.

El programa puede ser dividido en siete grandes problemas a resolver, cada uno
con su conjunto de subtareas en las que se dividirá. Estos problemas son:

* Lectura de parámetros.
* Manejo de archivos.
* Creación de estructuras de datos.
* Validación de un juego.
* Resolución de un juego.
* Conversión entre binario y texto.
* Representación de la solución.

El análisis de cada uno se muestra a continuación:

### Lectura de parámetros:

La lectura de parámetros consta en obtener los datos que el usuario envíe por la
terminal de comandos junto con el comando de ejecución del programa.

El primer comando indica la operación a efectuar, ***validate*** indica que se debe
validar la matriz de entrada, ***solve*** indica que esta se debe resolver, y
***convert*** indica que se debe dar la conversión de texto a binario o viceversa.
Cualquier entrada que no se apegue a estos tres casos es considerada inválida y
mostrará al usuario una advertencia junto con ayuda.

Los siguientes comandos constan de una etiqueta y el archivo correspondiente. Se
deben analizar tanto etiquetas como nombres de archivo, lo cuál puede ser
implementado en una subtarea que analice la función de las etiquetas y casos
especiales (cuando no se provee una etiqueta o archivo, o cuando se provee la
etiqueta -o para la salida)

### Manejo de archivos:

### Creación de estructuras de datos:
Para la creacion de estructuras de datos , necesitaremos tener en cuenta la entrada
que se ingrese con los valores de las tuberías, el primer numero será asignado a una
variable de tipo entero llamada *filas*, el segundo numero correspoderá a la variable
de tipo entero nombrada *columnas*, la tercera y cuarta se asignaran a las variables
tambien de tipo entero *entradas* y *salidas* respectivamente. Se inicializará un struct llamada *celda* (nombre dado por que será una estructura que represente la celda de cada tubería) Tendrá dentro de su estructura 4 variables de tipo int que nos servirá como booolean, las cuales representan los puntos cardinales, todos inicializadas en 0. Seguidamente inicializaremos una matriz de structs llamada *tuberías* , a esta se le asignará las tuberias que vienen despues de las entradas y salidas.
### Validación de un juego:

A tomar en consideración:

* Cada espacio de la matriz tiene conexiones con sus cuatro puntos cardinales.
* El tipo de tubería indica cuales de estas conexiones están abiertas.
* Los tipos de tubería equivalentes al rotarlos son los conjuntos: {1,2,4,8},
{3,6,9,12}, {5,10}, {7, 11, 13, 14} o sus equivalentes en hexadecimal (útil para
  la resolución).
* La matríz consta de dos filas y dos columnas extra, correspondientes a los
posibles espacios de entradas y salidas de fluído.

![Tabla de tuberías](https://i.imgur.com/fi3kcuz.png)

Figura 1: Tabla de tuberías.

Una subrutina analiza los bordes de la matriz con un recorrido circular, cada vez
que esta encuentre una entrada, llama a otra subrutina que recibirá la matríz y
la casilla de la entrada.

La subrutina revisa el punto hacia el que conecta la entrada y revisa sus
conexiones mediante otra subrutina. Si hay una conexión entre la entrada y la
tubería adyacente en la dirección de su conexión, se mueve hacia este punto.

Luego repite el proceso de revisar conexiones para cada tubería a la que conecte.
La condición de parada es que el flujo llegue a una salida, ante lo cuál se dará
un mensaje al usuario en el que se indica que la solución es exitosa, si
en cambio el flujo  llegó a una tubería sin conexión o a una casilla sin tubería,
se envía un mensaje de que la solución es fallida.

La subrutina que revisa si hay conexión entre dos casillas recibe la casilla actual
y su casilla adyacente, junto con las direcciónes de sus conexiones. Si la casilla
actual tiene una conexión hacia una dirección, y su casilla adyacente en esa dirección
tiene una conexión en el lado contrario, quiere decir que están conectadas. Por
ejemplo: Si una casilla tiene una conexión hacia el este, y su casilla adyacente
al este tiene una conexión al oeste, ambas casillas están conectadas.

![Ejemplo básico](https://i.imgur.com/GCiBeGk.png)

Figura 2: Ejemplo básico del ciclo.


### Resolución de un juego:

---

### Conversión entre binario y texto:

---

## Diseño:
Para el diseño iniciaremos con lo que se pasará por archivo, aunque bien se sabe
que esta parte de leer archivos tiene que estar en el diseño, se explicará mas
 adelante, conforme los pasos se vayan dando.
1. Leer el archivo.
2. inicializar variables de tipo entero llamadas *filas* *columnas* *entradas* y
 *salidas*.
3. Crear un struct llamado *celda* con 4 enteros booleanos incializados, cada uno
llamado *Norte* *Sur* *Este* *Oeste* .
4. Leer cantidad de filas, columnas, entradas y salidas.
5. Crear Matriz de structs 2+filas por 2+columnas.
6. Declarar una subrutina  para la lectura de las entradas desde el salto de linea
hasta la cantidad de entradas, donde cada salto de linea se sume.
7. Declarar otra subrutina para la lectura de las salidas desde la finalizacion de
la anterior subrutina, donde cada salto de linea se sume
hasta la cantidad de salidas.
8. Una vez establecidas las salidas y entradas procedemos a asignarlas en la matriz.
9. Declarar una subrutina que permita leer caracter por caracter y asignarlos en
la matriz, cada caracter modificará el struct por lo que se condicionará sus
direcciones.
10. Cerrar el archivo.
11. Recorrer la matriz para darnos cuenta de las fugas.
//Falta de terminar el diseño.

---
# Manual del Usuario:


_1. Se tiene un archivo con 10 caracteres en total formado por tres caracteres distintos (ej:ABC). De todos los archivos posibles con estas características mostrar el archivo de máxima entropía que se pueda comprimir mejor usando LZ77. No es necesario comprimir el archivo._

    Para tener máxima entropía en un archivo de 10 mensajes con 3 símbolos {A,B,C}, se requiere por ejemplo esta tabla de frecuencias: {A:4, B: 3, C: 3}. 
    
    LZ77 aprovecha repeticiones en una ventana, por lo que el archivo elegido tendrá que tener los caracteres iguales a continuación. En nuestro ejemplo: "AAAABBBCCC" el archivo de estas características que mejor podría comprimirse.

---
_2. Explique en que casos sería una buena idea usar un compresor aritmético estático de orden 3._

    Para que se pueda usar un compresor estático (aritmético o no y de cualquier orden) se requiere poder hacerle dos pasadas al archivo. Si además de estático es de orden 3 sólo va a convenir usar un compresor así si el alfabeto es pequeño o el archivo muy grande. Caso contrario, el tamaño de las tablas de frecuencia deja de ser insignificante.
    Un caso de uso podría ser un archivo que contenga direcciones MAC cercanas entre sí. El alfabeto en ese caso es hexadecimal (16 símbolos de 0 a F) con lo cual las tablas de frecuencia no llegan a ser demasiado grandes. Si las direcciones son cercanas entre sí, se aprovecharían los contextos.  
 

---
_3. Tenemos un compresor aritmético dinámico de orden 0 que trabaja procesando bit por bit. Si comprimimos un archivo que está formado por una serie de 1000 bits en 1 y luego dos bits en 0. ¿cuántos bits ocupará el archivo comprimido?_

    NS/NC


---
_4. Una planta industrial decidió instalar un sistema monitor de temperatura, a fin de obtener registro de las variaciones que existen, y poder tomar acciones de ser necesario. Dicho monitor cuenta con un sensor que emite cada 5 segundos un registro (fecha: AAAAMMDD, hora: HH:MM:SS, Temperatura: XX.XX, Variación: Numérico, puede ser positivo o negativo). Más allá de las acciones inmediatas que se puedan tomar, esta información se quiere almacenar para realizar consultas o análisis a futuro. Se pide proponer una solución que permita almacenar estos datos comprimidos. Se pueden utilizar uno o más algoritmos de los vistos en clase, o proponer variantes adaptadas a la estructura específica de los datos con los que se cuentan. Se debe explicar cómo queda la estructura final del archivo, y el análisis en el que se basó la solución._



---
_5. Determinar si las siguientes afirmaciones son V / F justificando la respuesta:_

- A. La entropia es una aproximacion de cuanto se puede comprimir, dado que no podemos
calcular cuanto se puede comprimir un string.

 _Verdadero_: la entropía es una medida de la cantidad de información que contiene un archivo y sirve como aproximación de límite de compresión.

- B. Una forma posible de comprimir un stream de datos es utilizar un huffman estático.

 _Falso_: los métodos estáticos no sirven para comprimir streams de datos, ya que requieren realizar pasadas completas al archivo para generar tablas de frecuencia.

- C. La entropia puede utilizarse para construir clasificadores de texto.

_Falso_: la entropía se basa en las probabilidades de los símbolos y sólo indica cantidad de información, pero por sí sola no se puede usar para clasificar textos.

- D. Un compresor estadistico estático comprime siempre mejor que un compresor estadístico
dinámico.

_Falso_: el tamaño de las tablas de frecuencia puede contrarestar la ventaja del compresor estático, sobre todo en órdenes superiores o con abecedarios grandes. 

- E. Podemos determinar la longitud final del archivo comprimido utilizando huffman estático de orden 1, calculando la entropía y multiplicándola por la cantidad de caracteres del archivo.

_Falso_: 

- F. Tenemos 2 archivos, uno con longitud pequeña y el otro muy grande que se comprimen
utilizando huffman estático de orden 5. Si observamos que tienen la mismas tablas de
frecuencias podemos afirmar que el cociente entre el tamaño del archivo sin comprimir y el
tamaño del archivo comprimido será similar.

_Falso_: usando Huffman estático de orden 5, el orden de los caracteres incide en el tamaño del archivo comprimido. Los archivos podrían tener la misma tabla de frecuencias pero lograr compresiones muy distintas.

- G. Todo archivo con complejidad de kolmogorov baja tendrá una entropía de Shannon baja.

_Falso_: podría tener un archivo con entropía alta que se pueda generar con un programa  pequeño (por ejemplo dígitos de pi).

- H. Es imposible que un archivo comprimido mediante huffman estático de orden 1 iguale la
máxima compresión dada por la entropía del mismo.

_Falso_: Para códigos de longitudes enteras de bits, huffman da la compresión óptima.
# Pandas
# Spark
# Compresión
## Complejidad de Kolmogorov K(x)
Sea x un string, K(x) es igual a la cantidad de bits mı́nimos que debe tener un programa que genera x.

__K(x) es intractable (incomputable). Se aproxima por el mejor compresor.__
## Random
Sea x un string, se dice que x es random/aleatorio si y sólo si K(x) = |x|. Es decir que  a complejidad del string es igual a la longitud del mismo.
## Distancia de Kolmogorov
KD(x, y) = K(xy) − min{K(x), K(y)}
## Distancia normalizada de Kolmogorov
N KD(x, y) = K(xy) − min{K(x), K(y)} / max{K(x), K(y)}
## Entropía de una fuente H(x)
Esperanza (valor esperado) de la longitud de sus códigos. Mide la cantidad de información representada. Nos da la longitud promedio en bits de cada mensaje de la fuente.

Se maximiza cuando todos los mensajes son equiprobables y se minimiza cuando un mensaje tiene probabilidad 1 es decir que se trata de una fuente determinı́stica. __Si la entropía es máxima, todos los mensajes son equiprobables y el archivo es random.__
### Entropía Conjunta H(X1,X2,Xn)
Mide la cantidad de información contenida por las n variables al mismo tiempo.
### Entropía Condicional
Mide la cantidad de información de una variable dado que se conoce el valor de otra.
### Información Mutua
La cantidad de información que comparten dos variables. Si fueran independientes, es cero.
### Entropía Relativa
Mide la distancia (diferencia) entre dos distribuciones para los mismos datos. Se usa para saber cuánta información se pierde por aproximar una distribución por otra. Para calcularla se usa la ecuación de divergencia de Kullback Leibler.
### Entropía Cruzada
Cálculo de la entropía de una variable usando la distribución de otra. Sirve para aproximar y medir error.
## Huffman
Códigos de una cierta longitud entera de bits que representan probabilidades/frecuencias.
### Huffman Estático
En la primer pasada se arma una tabla de frecuencias, en la segunda se genera un árbol binario que dará los códigos. Los códigos generados son siempre prefijos, por lo que se pueden decodificar instantáneamente. Se puede usar cualquier bit como padding.
### Huffman Dinámico
Se inicia suponiendo que todos los mensajes posibles son equiprobables y se va agregando cada mensaje al árbol y emitiendo en cada paso. Requiere un código especial para indicar EOF.

__Nunca puede comprimir mejor que el método estático, a lo sumo igual si el archivo es completamente aleatorio (mensajes equiprobables).__
## Modelos de Orden Superior (n)
Usan información contextual (los n caracteres anteriores). Para Huffman, no es muy útil porque tarda mucho en aprender (problema de frecuencia cero).

__Huffman Estático:__ Requiere una tabla de frecuencia para cada contexto, muy caro para órdenes mayores a 2.

__Huffman Dinámico:__ Va armando árboles para cada contexto a medida que lee. 

## Compresión Aritmética
Transforma un archivo en un número en el intervalo [0, 1).  Puede comprimir los mensajes de una fuente en una cantidad no-entera de bits. Puede ser estática o dinámica y también de órdenes superiores.

### PPMC: Prediction by Partial Matching
Compresión aritmética, con variación de modelos dependiendo de la frecuencia. Arranca en orden 0 y va subiendo hasta un máximo. El máximo óptimo suele ser cercano a 5 o 6.

### DMC: Dynamic Markov Compression
Modelo aritmético dinámico y de orden 2 que predice bit a bit. 

## LZ
Se basa en reemplazar secuencias repetidas por punteros a las posiciones originales. La longitud de ventana (buffer) define qué tan rápido y qué tan bien puede comprimir. Descomprimen muy rápido, porque sólo deben reemplazar.

### LZSS (LZ77)
Un bit indica si lo que sigue es un byte literal o una repetición. Se define una longitud de ventana y una longitud mínima de match. La longitud de la ventana define cuántos bits se requieren para indicar una repetición.

Flexible Parsing (vs lazy parsing): optimización que en cada paso analiza si conviene buscar un match más largo o parar en esa posición. 

### Deflate (LzHuf)
Mismo concepto que LZSS, pero se utiliza un árbol de Huffman dinámico en donde conviven los 256 caracteres posibles y además todas las longitudes posibles desde LMIN hasta LMAX. Este árbol se utilizará para codificar los caracteres literales cuando no hay un match y para las longitudes cuando hay un match.

### LZW (LZ78)
Arma una tabla donde va almacenando las repeticiones y comprime usando punteros a esa tabla. Cuando se llena, la duplica. Requiere alguna política de _clearing_ para limpiar la tabla si el nivel de compresión es malo.
Usar compresión aritmética en la tabla mejora mucho la capacidad de compresión.

__Cálculo de complejidad:__ se puede estimar la complejidad del archivo mediante las probabilidades de los patrones que encontró LZW (cantidad de veces que aparece cada patrón sobre cantidad total de patrones).

### Snappy
__Muy rápido, pero bajo nivel de compresión__. En cada bloque, el primer byte indica en sus primeros dos bits:

- 00 = literales
- 01 = 1 byte match
- 10 = 2 byte match

_Literales:_ los siguientes 6 bits (0-64) indican la cantidad de bytes de literales k que vienen a continuación. - Si 0 < k < 60: k literales.
- Si k=60: k = el próximo byte
- Si k=61: k = los dos próximos bytes
- Si k=62: k = los tres próximos bytes
- Si k=63: k = los cuatro próximos bytes

Se usa formato de longitud variable: el primer bit de cada byte indica si el número termina en dicho byte (0) o continua en el siguiente.

### LZMA
El LZ que mejor nivel de compresión logra. Usa 7 tipos de códigos y compresión aritmética.

### Block Sorting
__1. Transformación de Burrows y Wheeler__

Transforma un archivo cualquiera en uno localizado (junta grupos similares) y es reversible.

__2. MTF (Move To Front)__

Comienza  con una tabla de 256 caracteres posibles. Procesa caracter por caracter emitiendo el índice en la tabla y moviendo el caracter al comienzo de la tabla. En archivos localizados disminuye la entropía, porque emite números bajos.

__3. Cualquier compresor estadístico o aritmético__

Aprovechando que se tiene un archivo con mayoría de bits bajos y repetidos, se obtiene un muy buen nivel de compresión.

# Hashing
# Reducción de Dimensiones
# Information Retrieval
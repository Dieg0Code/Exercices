# Ejercicios Hackerrank

## 1. Plus Minus

Dado un array de integers, calcular la fracción de elementos positivos, negativos y ceros que contiene. Imprimir el valor de cada fracción en una nueva línea.

Ejemplo:

```java
int[] arr = {1, 1, 0, -1, -1};
```

- Son 5 elementos en el array.
- 2 elementos son positivos, su fracción es 2/5.
- 2 elementos son negativos, su fracción es 2/5.
- 1 elemento es cero, su fracción es 1/5.

El resultado impreso sería:

```
0.400000
0.400000
0.200000
```

Debe tener 6 decimales de precisión.

### Solución

Tenemos que contar la cantidad de elementos totales del array, la cantidad de elementos positivos, negativos y ceros. Luego, dividimos la cantidad de elementos positivos, negativos y ceros entre la cantidad total de elementos y lo imprimimos con 6 decimales de precisión.

```java
    public static void plusMinus(List<Integer> arr) {
        int positiveNumbers = 0;
        int negativeNumber = 0;
        int zeros = 0;
        int listSize = arr.size();
        
        for (int i = 0; i < listSize ; i++) {
            if (arr.get(i) > 0) {
                positiveNumbers++;
            } else if (arr.get(i) < 0) {
                negativeNumber++;
            } else {
                zeros++;
            }
        }
        
        
        
        System.out.printf("%.6f\n", (double) positiveNumbers / listSize);
        System.out.printf("%.6f\n", (double) negativeNumber / listSize);
        System.out.printf("%.6f\n", (double) zeros / listSize);

    }
```

#### Apuntes

- Hay que considerar que en la función que nos entregan el parámetro es un ``List<Integer>`` y no un array de integers, es por eso que para obtener el tamaño del array se utiliza el método ``size()`` y para obtener un elemento en una posición específica se utiliza el método ``get()``.
- También tenemos cuatro datos que nos interesan, la cantidad total de elementos ``listSize``, la cantidad de elementos positivos ``positiveNumbers``, la cantidad de elementos negativos ``negativeNumber`` y la cantidad de ceros ``zeros``, en este caso todos son del tipo ``int``.
- La solución es simple, iterar sobre cada uno de los elementos y mediante condiciones ``if`` determinar si es positivo, negativo o cero, para incrementar en uno la cantidad de elementos correspondiente, positivos, negativos o ceros.
- Hay que considerar también que se nos pide que imprimamos con 6 decimales de precisión, para eso utilizamos el método ``printf()`` y le pasamos como primer parámetro el formato de impresión ``%.6f`` y como segundo parámetro el valor que queremos imprimir.
- `%.6f` quiere decir que se imprimirá un número decimal con 6 decimales de precisión.
- `(double) positiveNumbers / listSize` es la operación que se realiza para obtener la fracción de elementos positivos, se hace un cast a double para que el resultado sea un número decimal y no un número entero.

## 2. Mini-Max Sum

Dado una lista de 5 integers, debemos encontrar el valor mínimo y máximo que se puede obtener sumando 4 de los 5 integers. Luego debemos imprimir el resultado en una sola línea, primero el valor mínimo y luego el valor máximo, separados por un espacio.

Ejemplo:

```java
int[] arr = {1, 3, 5, 7, 9};
```

La suma minima es 1 + 3 + 5 + 7 = 16 y la suma máxima es 3 + 5 + 7 + 9 = 24. Por lo tanto, la salida sería:

```
16 24
```

### Solución

```java
 public static void miniMaxSum(List<Integer> arr) {
        
        arr.sort(null);
        
        long minSum = 0;
        long maxSum = 0;
        int arrSize = arr.size();
        
        for (int i = 0; i < arrSize - 1; i++) {
            minSum += arr.get(i);
        }
        
        for (int i = 1; i < arrSize; i++) {
            maxSum += arr.get(i);
        }
        
        System.out.println(minSum + " " + maxSum);

    }
```

#### Apuntes

- Hay que tener en cuenta que para la lista puede venir desordenada. La solución simple podría ser sumar los cuatro primero y excluir el último que sería el mayor, y luego sumar los cuatro últimos y excluir el primero que sería el menor, pero como no sabemos si la lista viene ordenada o no, lo mejor es ordenarla primero, es por eso que se utiliza el método ``sort()``.
- También tenemos 3 datos que nos interesan, la suma mínima ``minSum``, la suma máxima ``maxSum`` y el tamaño de la lista ``arrSize``. En el ejercicio también se menciona que hay que tener en cuenta que los valores de la suma pueden ser muy grandes, por lo que se utiliza el tipo de dato ``long`` para almacenar los valores.
- La solución consiste en, primero ordenar la lista, luego iterar sobre los primeros 4 elementos, esto se hace con un ciclo for y el iterador partiendo en 0 y terminando en ``arrSize - 1`` para llegar solo hasta el penúltimo elemento, y sumar los valores en la variable ``minSum``. Luego, se itera sobre los últimos 4 elementos, esto se hace con un ciclo for y el iterador partiendo en 1 y terminando en ``arrSize`` para empezar desde el segundo elemento y sumar los valores en la variable ``maxSum``.
- Posteriormente, se imprime el valor de ``minSum`` y ``maxSum`` en una sola línea, separados por un espacio.

## 3. Time Conversion

Dada una hora en formato de 12 horas, convertirlo a formato de 24 horas.

Ejemplo:

```
s = "07:05:45PM"
```

La hora en formato de 24 horas sería:

```
19:05:45
```

### Solución

```java
public static String timeConversion(String s) {
    
    String amPm = s.substring(s.length() - 2);
    String timeString = s.substring(0, s.length() - 2);
    
    String[] timeParts = timeString.split(":");
    int hour = Integer.parseInt(timeParts[0]);
    String minutes = timeParts[1];
    String seconds = timeParts[2];
    
    if(amPm.equals("AM")) {
        if(hour == 12) {
            hour = 0;
        }
    } else if (amPm.equals("PM")) {
        if (hour != 12) {
            hour += 12;
        }
    }
    
    String hourFormat = String.format("%02d", hour);
    
    return hourFormat + ":" + minutes + ":" + seconds;

    }
```

#### Apuntes

- La hora se nos entrega en formato String.
- Tenemos que considerar 4 cosas, la hora, los minutos, los segundos y si es AM o PM.
- Comenzamos sacando la parte de AM o PM, esto se hace creando un substring ``amPm`` que contiene los últimos dos caracteres de la hora, para obtener estos dos últimos caracteres se utiliza el método ``substring()``, este método crea una String a partir de otra, para esto toma como parámetro el indice desde donde se va cortar la String, en este caso le pasamos la longitud total y le restamos 2 que seria el AM o el PM, entonces corta desde dos caracteres antes del final hasta el final.
- Luego, creamos otra substring ``timeString`` que contiene la hora sin el AM o PM, para esto se utiliza el método ``substring()`` y se le pasa como parámetros el índice desde donde se va a cortar y el índice hasta donde se va a cortar, en este caso se corta desde el inicio hasta dos caracteres antes del final.
- Creamos un array de Strings ``timeParts`` para almacenar las partes de el tiempo, hora, minutos y segundos. El tiempo está dividido por `:`, entonces usamos esto como separador para dividir la hora en partes, en donde el primer elemento sería la hora, el segundo los minutos y el tercero los segundos.
- Sacamos cada uno de estos valores y los almacenamos en variables, la hora la convertimos a entero con el método ``parseInt()``, esto es porque posteriormente vamos a hacer operaciones matemáticas con la hora.
- Primero comenzamos comprobando si es que la marca de tiempo que nos dieron es AM, si es el caso y la hora es 12, entonces la hora se convierte en 0, esto es porque en un formato de 24 horas las 12 AM son las 00 horas.
- Comprobamos si es que la marca de tiempo es PM, si es el caso y la hora no es 12, entonces sumamos 12 a la hora, esto es porque por ejemplo si son las 1 PM, en un formato de 24 horas serían las 13 horas, osea 1 + 12, etc.
- Formateamos la hora con el método ``format()``, este método nos permite formatear un número a un String, en este caso le pasamos el formato ``%02d`` que quiere decir que se formateará un número entero a dos dígitos, si el número tiene un solo dígito se le añadirá un 0 al principio, la `d` es para indicar que es en base `d`ecimal.
- Retornamos la hora formateada, los minutos y los segundos, separados por `:`.
- También hay que recalcar que para hacer la comprobación de si es AM o PM se utiliza el método ``equals()`` y no `==`, esto es porque `==` compara referencias de objetos y no el contenido de los objetos, en cambio ``equals()`` compara el contenido, para String hay que utilizar ``equals()``.

## 4. Sparse Array

Dado un array de strings y un array de queries, determinar cuantas veces aparece cada query en el array de strings.

Ejemplo:

```java
String[] strings = {"aba", "baba", "aba", "xzxb"};
String[] queries = {"aba", "xzxb", "ab"};
```

El resultado sería:

```
2
1
0
```

Es decir, el string "aba" aparece 2 veces, el string "xzxb" aparece 1 vez y el string "ab" no aparece en el array de strings.

El primer array contiene un conjunto de strings y el segundo un conjunto de consultas, hay que determinar cuantas veces aparecen en el primer conjunto las strings que están en el segundo conjunto.

### Solución

```java
public static List<Integer> matchingStrings(List<String> strings, List<String> queries) {
    // Write your code here
    Map<String, Integer> frecuencyMap = new HashMap<>();
    List<Integer> result = new ArrayList<>();
    
    for (String s : strings) {
        frecuencyMap.put(s, frecuencyMap.getOrDefault(s, 0) + 1);
    }
    
    for (String q : queries) {
        result.add(frecuencyMap.getOrDefault(q, 0));
    }
    
    return result;
        
    }
```

#### Apuntes

- Creamos un conjunto de elementos clave - valor, en vamos a guardar, el elemento y la cantidad de veces que aparece en el conjunto de strings.
- También creamos una lista de enteros que va a contener la cantidad de veces que aparece cada string en el conjunto de queries.
- Iteramos cada uno de los elementos en el primer conjunto de strings, y vamos guardando en el mapa la cantidad de veces que aparece cada string, para esto utilizamos el método ``getOrDefault()``, este método nos permite obtener el valor de una clave en un mapa, si la clave no existe, entonces se retorna el valor por defecto que se le pasa como segundo parámetro, en este caso 0, y se le suma 1, esto es para contar la cantidad de veces que aparece cada string.
- Luego, iteramos cada uno de los elementos en el segundo conjunto de queries, y vamos guardando en la lista la cantidad de veces que aparece cada string en el conjunto de strings, para esto utilizamos el método ``getOrDefault()``, si la clave no existe, entonces se retorna el valor por defecto que se le pasa como segundo parámetro, en este caso 0.
- Finalmente, retornamos la lista con la cantidad de veces que aparece cada string en el conjunto de queries.
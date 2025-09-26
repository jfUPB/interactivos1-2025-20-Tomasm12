
# Evidencias de la unidad 5

### Actividad 01


1. ¿Describe cómo se están comunicando el micro:bit y el sketch de p5.js? ¿Qué datos envía el micro:bit?  

El micro:bit y p5.js se comunican mediante el **puerto serial** a través del cable USB.  
El micro:bit envía cuatro datos:  

- **xValue** → valor del acelerómetro en el eje X.  
- **yValue** → valor del acelerómetro en el eje Y.  
- **aState** → estado del botón A (True/False).  
- **bState** → estado del botón B (True/False).  

2. ¿Cómo es la estructura del protocolo ASCII usado?  

Los datos se envían como texto en formato **ASCII**, separados por comas y terminados en salto de línea `\n`.  

Ejemplo de envío desde el micro:bit:  

```python
data = "{},{},{},{}\n".format(xValue, yValue, aState, bState)
```
y los dats 
-123,456,True,False\n

3. ¿Muestra y explica la parte del código de p5.js donde lee los datos del micro:bit y los transforma en coordenadas de la pantalla?
En el código, la lectura y transformación ocurre en la función draw():

```python
if (port.availableBytes() > 0) {
  let data = port.readUntil("\n");
  if (data) {
    data = data.trim();
    let values = data.split(",");
    if (values.length == 4) {
      microBitX = int(values[0]) + windowWidth / 2;
      microBitY = int(values[1]) + windowHeight / 2;
      microBitAState = values[2].toLowerCase() === "true";
      microBitBState = values[3].toLowerCase() === "true";
      updateButtonStates(microBitAState, microBitBState);
    } else {
      print("No se están recibiendo 4 datos del micro:bit");
    }
  }
}
```

- port.readUntil("\n") → lee lo recibido hasta el salto de línea.
- data.split(",") → separa los valores por comas.
- values[0] y values[1] → son xValue y yValue, convertidos en microBitX y microBitY.
- values[2] y values[3] → son aState y bState, convertidos en valores booleanos.

4. ¿Cómo se generan los eventos A pressed y B released que se generan en p5.js a partir de los datos que envía el micro:bit?
``` python
function updateButtonStates(newAState, newBState) {
  if (newAState === true && prevmicroBitAState === false) {
    lineModuleSize = random(50, 160);
    clickPosX = microBitX;
    clickPosY = microBitY;
    print("A pressed");
  }

  if (newBState === false && prevmicroBitBState === true) {
    c = color(random(255), random(255), random(255), random(80, 100));
    print("B released");
  }

  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}
```
5. **Capturas de pantalla de los algunos dibujos que hayas hecho con el sketch.**

<img width="878" height="798" alt="image" src="https://github.com/user-attachments/assets/cb85352e-66fa-4f1b-aace-d59087e435e6" />
<img width="889" height="795" alt="image" src="https://github.com/user-attachments/assets/a67a55e7-071c-4fa8-b2be-69f72ebae212" />
<img width="884" height="802" alt="image" src="https://github.com/user-attachments/assets/3be19504-fffc-459d-b3c1-5e360c0b4f5c" />

### Actividad 02

<img width="1310" height="773" alt="image" src="https://github.com/user-attachments/assets/43afebb3-f493-44e3-a2b5-c9ea067c3a8b" />
<img width="1462" height="1005" alt="image" src="https://github.com/user-attachments/assets/5f3425f6-b8ff-4995-9ae6-d98b642fedd8" />

**¿Por qué se ve este resultado?**
El resultado observado se debe a que el programa no transmite caracteres legibles, sino datos en formato binario empaquetados mediante struct.pack. Dichos datos representan valores numéricos en binario y no en codificación ASCII. Al visualizar la recepción en modo “Texto”, la aplicación SerialTerminal intenta interpretarlos como caracteres, pero la mayoría de esos bytes no corresponde a símbolos imprimibles, por lo que se generan caracteres y signos aparentemente aleatorios.


<img width="1552" height="504" alt="image" src="https://github.com/user-attachments/assets/4f6ba087-57ae-4ff3-bd52-13c3710882c9" />

**Captura el resultado del experimento anterior. Lo que ves ¿Cómo está relacionado con esta línea de código?**
``` python
data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
```
**No te parece que el resultado es un poco más difícil de leer que el texto en ASCII?**

Lo que se ve en la pantalla cuando se elige “Mostrar datos como: Todo en HEX” son los mismos bytes que genera la línea data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState)). Esa línea junta dos números enteros de 16 bits y dos valores de un byte en un solo bloque binario. Al mostrarlos en hexadecimal, el programa enseña cada byte convertido a base 16, es decir, exactamente cómo se están enviando los datos por el puerto serie.

Dificultad de lectura en HEX frente a ASCII
La vista en hexadecimal es más difícil de leer que en ASCII porque no se muestran caracteres que las personas podamos reconocer, sino códigos numéricos en base 16.

**¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII?**
Una ventaja importante del formato binario es que reduce significativamente el tamaño de la información transmitida, lo que lo hace más rápido y eficiente para enviar grandes volúmenes de datos sin tener que convertirlos a texto. Sin embargo, su principal desventaja es la falta de legibilidad directa: los datos no pueden interpretarse fácilmente a simple vista y requieren de herramientas o programas específicos para decodificarlos.

 **Captura el resultado del experimento. ¿Cuántos bytes se están enviando por mensaje? ¿Cómo se relaciona esto con el formato '>2h2B'? ¿Qué significa cada uno de los bytes que se envían?**

<img width="1323" height="684" alt="image" src="https://github.com/user-attachments/assets/4669a88a-340f-4d9d-bd61-c8ab63238a23" />

En cada sacudida se mandan 6 bytes. Esto pasa porque el formato '>2h2B' indica dos números enteros de 16 bits (2 × 2 bytes = 4 bytes) más dos bytes para los botones (2 × 1 byte = 2 bytes). Al sumar todo son 6 bytes. El símbolo > significa que se envían primero los bytes más importantes (big-endian).

Ese formato dice cómo se organizan los datos. Los dos primeros bytes son el valor X del acelerómetro, los dos siguientes el valor Y, y los dos últimos son para saber si el botón A y el botón B estaban presionados (0 = no, 1 = sí). Por eso en la pantalla, cada vez que hay una sacudida aparecen grupos de seis números en hexadecimal.

Los dos primeros bytes son el eje X en binario, los dos siguientes son el eje Y y los dos últimos indican el estado de los botones A y B. Como se usa big-endian, siempre se ve primero el byte alto y luego el bajo en cada número de 16 bits.

**Recuerda de la unidad anterior que es posible enviar números positivos y negativos para los valores de xValue y yValue. ¿Cómo se verían esos números en el formato '>2h2B'?**

En el formato '>2h2B' los valores de xValue y yValue se codifican como enteros con signo de 16 bits en orden big-endian. Esto significa que los números positivos aparecen en hexadecimal tal cual su valor (por ejemplo +100 se vería como 00 64 y +1000 como 03 E8), mientras que los negativos usan la representación estándar de enteros con signo el complemento a dos, que en hex parece un número muy alto pero en realidad corresponde a un valor negativo (por ejemplo −100 como FF 9C o −1000 como FC 18). Al comprender este detalle se vuelve más claro por qué los datos se ven así en la captura.

**Captura el resultado del experimento. ¿Qué diferencias ves entre los datos en ASCII y en binario? ¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII? ¿Qué ventajas y desventajas ves en usar un formato ASCII en lugar de binario?**

<img width="1187" height="561" alt="image" src="https://github.com/user-attachments/assets/c5305577-b6c4-4457-b68a-950a7d73f6eb" />

En la captura se ve que los datos en binario aparecen encerrados entre corchetes [] en forma de bytes (HEX), mientras que justo después se muestran en ASCII ya convertidos en texto comprensible. Básicamente son los mismos valores, pero en dos representaciones distintas: una cruda y compacta y otra legible para las personas.

En binario, la principal ventaja es que cada paquete ocupa muy pocos bytes y por eso resulta más eficiente y rápido cuando se envían muchos datos seguidos. Sin embargo, la desventaja es que no podemos leerlo a simple vista; siempre se necesita un programa o una herramienta que haga la interpretación para nosotros.

En ASCII, por el contrario, la ventaja está en que todo se ve y se entiende directamente sin conversión extra, lo que facilita revisar o depurar los datos. La desventaja es que cada valor ocupa más espacio y la transmisión puede ser más lenta cuando se trabaja con volúmenes grandes de información.

### Actividad 03

**Explica por qué en la unidad anterior teníamos que enviar la información delimitada y además marcada con un salto de línea y ahora no es necesario.**

los datos enviados en ASCII no tenían siempre la misma longitud. Dependiendo de cuántos dígitos tuviera cada número, el tamaño del mensaje cambiaba y sin un delimitador era difícil para p5.js saber dónde terminaba un conjunto de valores y empezaba el siguiente.

En cambio, ahora estamos usando un formato binario con estructura fija. Cada envío ocupa exactamente 6 bytes (2 para xValue, 2 para yValue y 1 para cada botón), así que p5.js puede leer los datos en bloques de 6 bytes sin confundirse. Por eso ya no hace falta añadir saltos de línea ni otros delimitadores: el tamaño fijo del paquete cumple esa función de manera automática.

**Compara el código de la unidad anterior relacionado con la recepción de los datos seriales que ves ahora. ¿Qué cambios observas?**

En el código anterior, la lectura de los datos se hacía usando port.readUntil("\n") y luego se separaban los valores con split(","). Eso era necesario porque los datos venían en formato ASCII y su longitud variaba según la cantidad de dígitos, por lo que había que usar un delimitador para reconocer dónde terminaba cada paquete.

En cambio, ahora la lectura se hace con port.readBytes(6) y se usa un DataView para interpretar los bytes directamente como enteros o booleanos. Esto es posible porque el formato binario tiene un tamaño fijo (6 bytes) y no hace falta dividir ni convertir texto: p5.js ya sabe exactamente cuántos bytes corresponden a cada valor. El cambio principal es que pasamos de procesar cadenas de texto con delimitadores a leer datos binarios de longitud fija usando posiciones de memoria específicas.

**¿Qué ves en la consola? ¿Por qué crees que se produce este error?**
aparecen números extraños o muy grandes  y algunas líneas con valores que no deberían estar ahí. Esto indica que en esos momentos p5.js no está leyendo exactamente los 6 bytes que forman un paquete, sino que toma bytes “corridos” o mezclados con el paquete anterior o el siguiente.

Este problema ocurre porque la comunicación serial es continua, los datos llegan uno detrás del otro y no se alinean correctamente. Si el código de p5.js lee en un momento en que no han llegado los 6 bytes completos, o empieza a leer desde el byte equivocado, se pierde la sincronización y los valores se interpretan mal. Por eso aparecen números incoherentes en la consola.

**Analiza el código, observa los cambios. Ejecuta y luego observa la consola. ¿Qué ves?**

Revisando el código se nota que ahora se implementa framing: se añade un byte de inicio y un checksum al final para que p5.js pueda reconocer los paquetes completos y validar que no estén dañados.
Al ejecutarlo en la consola se ven lecturas ordenadas y coherentes de microBitX, microBitY y los botones, además de mensajes como “Microbit ready to draw” cuando se conecta el micro:bit. También pude ver que, si se simula un error o se reciben datos malos, aparece “Checksum error in packet” y ese paquete se descarta sin romper la lectura.
Esto confirma que el cambio en el código hace la comunicación más estable y fácil de depurar.

**¿Qué cambios tienen los programas y ¿Qué puedes observar en la consola del editor de p5.js?**

En las versiones finales, del lado del micro:bit ya no se envían solo los 6 bytes de datos, sino que se sumaron dos más: un header al inicio para marcar claramente dónde empieza cada paquete y un checksum al final para comprobar que la información llegó bien. Así cada paquete pasa de 6 a 8 bytes.

En p5.js se incorporó un buffer que acumula los bytes recibidos. Este buffer permite buscar ese header especial para alinear correctamente los datos antes de leerlos y, además, recalcular el checksum para verificar si el paquete es válido o descartarlo si está corrupto.

El checksum se calcula sumando los 6 bytes de datos y tomando el resultado módulo 256; es decir, se obtiene un número entre 0 y 255 que el receptor compara con el valor recibido para confirmar que todo está bien.

En la consola ahora se ven mensajes ordenados: al conectar aparece algo como “Microbit ready to draw” y los valores de X, Y y botones salen estables. Si ocurre un error de transmisión se muestra “Checksum error in packet” indicando que ese paquete se ignoró.


### Actividad 04
**Vas a documentar en tu bitácora todo el proceso de construcción de la aplicación, mostrando las pruebas intermedias que hiciste, los errores que encontraste y cómo los solucionaste.**
**Vas a realizar múltiples experimentos analizando el comportamiento de la aplicación que construiste. Reporta el proceso de experimentación en la bitácora. Con estas evidencias debes demostrar que has comprendido los conceptos y técnicas vistas en esta unidad.**

[Programa funcional](https://editor.p5js.org/Tomasm12/full/_CvDumbL3)

1. Conexión p5.js y lectura inicial (ASCII)

Se partió del código anterior que leía port.readUntil("\n") con split(",").

Prueba: conectar micro:bit.
Resultado: no llegaban datos legibles (porque ahora no hay saltos de línea ni texto).
Solución: cambiar la lógica a lectura de bytes (port.read() y buffers).
<img width="891" height="108" alt="image" src="https://github.com/user-attachments/assets/f1bc7ae8-32e7-45da-bdf3-40836dfb66b0" />

2. Implementación de lectura binaria

Se implementó un buffer que busca el byte de inicio 0xAA.

Al detectar 0xAA, se esperan los 7 bytes siguientes (2h2B + checksum).

Se calculó el checksum y se descartaron paquetes inválidos.

Prueba intermedia: imprimir en consola los valores X,Y,A,B.
Resultado: valores numéricos correctos (-1024 a 1024).

3 Integración con dibujo

Se mapeó microBitY → número de lados (3 a 12).

Se mapeó microBitX → radio (20 a 200).

Botón A mantenido → dibujar polígono.

Botón B presionado → limpiar lienzo.

Prueba: mover micro:bit y presionar botones.
Resultado: figura se dibuja, el radio y los lados cambian.

4. Ajuste de opacidad

Se agregó opacidad a la línea:

stroke(0, 50); 

<img width="743" height="337" alt="image" src="https://github.com/user-attachments/assets/d371c236-29d0-4595-9758-da5664e5feba" />

### Actividad 05
**En la unidad anterior abordaste la construcción de un protocolo ASCII. En esta unidad realizaste lo propio con un protocolo binario. Realiza una tabla donde compares, según la aplicación que modificaste en la fase de aplicación de ambas unidades, los siguientes aspectos: eficiencia, velocidad, facilidad, usos de recursos. Justifica con ejemplos concretos tomados de las aplicaciones modificadas.**

| Aspecto                         | Protocolo ASCII                                                                  | Protocolo binario                                             | Ejemplo concreto en la aplicación                                                                       |
| ------------------------------- | -------------------------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| **Eficiencia**                  | Menos eficiente: cada número se envía como caracteres de texto, ocupa más bytes. | Más eficiente: valores se envían directamente en bytes fijos. | Al enviar `xValue=1000`, ASCII envía “1”,“0”,“0”,“0” y coma; binario envía dos bytes.                   |
| **Velocidad**                   | Más lento: más bytes por paquete y necesidad de conversión texto→número.         | Más rápido: menos bytes y sin parseo de texto.                | La p5.js con ASCII usa `split(",")`; con binario no hay split, se leen bytes directamente.              |
| **Facilidad de implementación** | Fácil de depurar: legible en monitor serial.                                     | Requiere más cuidado: ilegible y se necesita framing.         | Con ASCII se podía abrir cualquier terminal y ver “1000,200,true,false”.    |
| **Uso de recursos**             | Más consumo de memoria y CPU en parseo.                                          | Menor uso de memoria y CPU al leer bytes crudos.              | En micro\:bit el `struct.pack()` produce paquete corto (7 u 8 bytes) frente a los \~20 bytes del ASCII. |

**¿Por qué fue necesario introducir framing en el protocolo binario?**
En ASCII hay separadores como comas y salto de línea \n que indican claramente el final de un paquete.
En binario cualquier byte puede valer cualquier cosa, no hay separadores naturales, por eso el receptor podría perder sincronización.
El framing es necesario para marcar de forma explícita el inicio de cada paquete y saber cuántos bytes leer.

**¿Cómo funciona el framing?**
El transmisor envía:

- Un byte de cabecera especial (por ejemplo 0xAA) para señalar el inicio.

- Una longitud conocida de datos (2 enteros + 2 bytes + checksum = 8 bytes).

- El receptor busca la cabecera y, cuando la encuentra, lee exactamente ese número de bytes para reconstruir el paquete.

**¿Qué es un carácter de sincronización?**

Es el byte especial que permite sincronizar emisor y receptor, marcando el inicio del paquete.
En este caso es 0xAA (hexadecimal 170).

**¿Qué es el checksum y para qué sirve?**

Es un valor calculado como suma de todos los bytes del paquete módulo 256.
Sirve para que el receptor compruebe si los datos llegaron íntegros. Si el checksum calculado no coincide con el recibido, se descarta el paquete.

**En la función readSerialData() del programa en p5.js:**
**¿Qué hace la función concat? ¿Por qué?**

``` javascript
serialBuffer = serialBuffer.concat(newData);
```
La función concat() une dos arreglos sin modificar los originales y devuelve un nuevo arreglo.
En este caso, se usa para acumular en serialBuffer los nuevos bytes recibidos (newData) desde el puerto serie. Esto es necesario porque los datos pueden llegar en trozos y se deben guardar hasta tener paquetes completos.


**En la función readSerialData() tenemos un bucle que recorre el buffer solo si este tiene 8 o más bytes ¿Por qué?**

El bucle se ejecuta únicamente si el serialBuffer tiene al menos 8 bytes porque el protocolo de comunicación define que cada paquete completo mide 8 bytes.
Si no hay 8 bytes, no se tiene suficiente información para procesar un paquete válido y por lo tanto se espera a que lleguen más datos.

**En el código anterior qué significa 0xaa?**

0xAA es un valor hexadecimal (decimal 170) que se usa como cabecera o carácter de sincronización.
Permite al receptor identificar el inicio de un paquete.


**En el código anterior qué hace la función shift y la instrucción continue? ¿Por qué?**
``` javascript
if (serialBuffer[0] !== 0xaa) {
  serialBuffer.shift();
  continue;
}
```
shift() elimina y devuelve el primer elemento de un arreglo.
En este caso, si el primer byte no coincide con 0xaa, se descarta ese byte porque no forma parte de un paquete válido.

continue hace que el bucle pase inmediatamente a la siguiente iteración, sin ejecutar el resto del bloque actual.
Aquí se usa para que, tras eliminar un byte inválido, el código vuelva a comprobar el siguiente byte del buffer.

Esto es necesario para resincronizar el buffer con el inicio correcto del paquete.


**Si hay menos de 8 bytes qué hace la instrucción break? ¿Por qué?**
```
if (serialBuffer.length < 8) break;
```
break sale del bucle while. Se hace porque no hay suficientes bytes para armar un paquete completo y se debe esperar a que lleguen más datos en la próxima ejecución de readSerialData().


**¿Cuál es la diferencia entre slice y splice? ¿Por qué se usa splice justo después de slice?**

``` javascript
let packet = serialBuffer.slice(0, 8);
serialBuffer.splice(0, 8);
```
- slice(0,8) crea una copia de los primeros 8 bytes sin modificarlos.

- splice(0,8) elimina esos 8 bytes del array original.

Primero se extrae el paquete para procesarlo y luego se eliminan esos bytes del buffer para no procesarlos de nuevo.

A la siguiente parte del código se le conoce como programación funcional ¿Cómo opera la función reduce?
``` javascript
    let computedChecksum = dataBytes.reduce((acc, val) => acc + val, 0) % 256;
```

reduce aplica una función acumuladora a cada elemento del array.
Aquí suma todos los bytes del paquete empezando en 0, y al final se toma módulo 256 para calcular el checksum.

**¿Por qué se compara el checksum enviado con el calculado? ¿Para qué sirve esto?**
``` javascript
if (computedChecksum !== receivedChecksum) {
    console.log("Checksum error in packet");
    continue;
}
```
Se compara para verificar la integridad del paquete.
Si no coinciden, significa que los datos llegaron corruptos o incompletos y se descartan con continue para no usar valores erróneos.

**En el código anterior qué hace la instrucción continue? ¿Por qué?**

Hace que el bucle while salte directamente a la siguiente iteración, ignorando el resto del código de esa vuelta.
Esto permite descartar el paquete con error y seguir procesando el siguiente sin detener el programa.

**¿Qué es un DataView? ¿Para qué se usa?**
``` javascript
let buffer = new Uint8Array(dataBytes).buffer;
let view = new DataView(buffer);
```

DataView es un objeto que permite interpretar bytes crudos de un ArrayBuffer en distintos formatos (enteros de 8, 16, 32 bits, con o sin signo, y con distintos órdenes de bytes).
Se usa para reconstruir correctamente los valores enviados desde el micro:bit.

**¿Por qué es necesario hacer estas conversiones y no simplemente se toman tal cual los datos del buffer?**
``` javascript
    microBitX = view.getInt16(0) + windowWidth / 2;
    microBitY = view.getInt16(2) + windowHeight / 2;
    microBitAState = view.getUint8(4) === 1;
    microBitBState = view.getUint8(5) === 1;
```

Porque los datos binarios pueden ocupar más de un byte y tener diferente endianness.
Si se leen como bytes individuales, los valores serían incorrectos.
Con DataView se pueden leer los dos primeros bytes como un entero de 16 bits con signo (X), los siguientes dos como entero de 16 bits con signo (Y), y los bytes individuales como enteros sin signo (botones). Esto garantiza que los valores sean exactamente los enviados.

### Autoevaluacion 

| Criterio                               | Nivel / Nota | Justificación                                                                                                                                                                                                                                                                                                        |
|----------------------------------------|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1. Profundidad de la Indagación         | **Excelente – 4.6** | Quise entender por qué y para qué se hacía cada paso. Y cunaod no entendia buscaba de que forema hacerlo o que otras formas habia para relizar esa actividad de forma correcta   |
| 2. Calidad de la Experimentación        | **En Desarrollo – 4.0** | Realicé varios experimentos para verificar que mi implementación del protocolo binario funcionara . Sin embargo, reconozco que me faltó documentar más a fondo cada paso y aislar mejor los errores antes de corregirlos. En esta parte me centré más en lograr que funcionara que en diseñar pruebas muy sistemáticas. |
| 3. Análisis y Reflexión                 | **Excelente – 4.6** | No me limité a describir resultados; traté de entender las causas. y profundizar en cada uno de ellos paar tener claor los temas|
| 4. Apropiación y Articulación de Conceptos | **Excelente – 4.8** | Fui capaz de explicar con mis propias palabras conceptos como *header*, *checksum*, `DataView` y `struct.pack` en MicroPython. Creo que ya me desenvuelvo mejor en estos temas|



Nota: 4.5




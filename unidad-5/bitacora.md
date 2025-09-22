
# Evidencias de la unidad 5

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

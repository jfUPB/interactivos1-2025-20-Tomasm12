
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
port.readUntil("\n") → lee lo recibido hasta el salto de línea.
data.split(",") → separa los valores por comas.
values[0] y values[1] → son xValue y yValue, convertidos en microBitX y microBitY.
values[2] y values[3] → son aState y bState, convertidos en valores booleanos.

4. ¿Cómo se generan los eventos A pressed y B released que se generan en p5.js a partir de los datos que envía el micro:bit?

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

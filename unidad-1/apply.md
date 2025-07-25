# Unidad 1

## 🛠 Fase: Apply

## Actividad 05
En esta actividad hicimos un sistema físico interactivo usando p5.js y el editor de micro:bit. La idea fue conectar el micro:bit con la computadora para que, al presionar el botón A, cambie el color de un cuadro en pantalla.

Con el código del micro:bit, se manda una letra por puerto serial:  
- Si el botón A está presionado, manda una "A".  
- Si no está presionado, manda una "N" (que se actualiza cada 100 milisegundos (0.1 segundos).

El código en p5.js recibe esa letra y cambia el color del cuadro:
- Si recibe "A", lo pinta rojo.  
- Si recibe "N", lo pinta verde.

También se usa un botón en la pantalla para conectar o desconectar el micro:bit. Esto ayuda a saber si el dispositivo está bien conectado. 

### Input 

- Presionar o no el botón A del micro:bit.

###  Proceso

- El micro:bit detecta si el botón está presionado y envía una letra por serial.
- El programa en p5.js lee esa letra y decide qué color mostrar.
  
###  Output 

- El cuadro se vuelve rojo si el botón A está presionado.
- Se vuelve verde si no lo está.


## Actividad 06
Control de movimiento con micro:bit  
### Enlace a mi programa  
[Programa en p5.js](https://editor.p5js.org/Tomasm12/sketches/ZiX_B9kpo)

### Código de mi programa
```
  let port;
  let connectBtn;
  let connectionInitialized = false;
  let cirx=200 
  let ciry=200 

  function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton("Connect to micro:bit");
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
  }

  function draw() {
    background(220);

    if (port.opened() && !connectionInitialized) {
      port.clear();
      connectionInitialized = true;
    }

    if (port.availableBytes() > 0) {
      let dataRx = port.read(1);
      if (dataRx == "A") {
        cirx -=10;
      } else if (dataRx == "B") {
        cirx +=10;
      }
    }

    ellipseMode(CENTER);
    ellipse(cirx,ciry,100,100 );

    if (!port.opened()) {
      connectBtn.html("Connect to micro:bit");
    } else {
      connectBtn.html("Disconnect");
    }
  }

  function connectBtnClick() {
    if (!port.opened()) {
      port.open("MicroPython", 115200);
      connectionInitialized = false;
    } else {
      port.close();
    }
  }
```
### Código del micro:bit
```
from microbit import *
import microbit

uart.init(baudrate=115200)

while True:
    if button_a.is_pressed():
        uart.write("A")
        sleep(200)  
    elif button_b.is_pressed():
        uart.write("B")
        sleep(200)
```

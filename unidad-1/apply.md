# Unidad 1

## 🛠 Fase: Apply

## Actividad 05
Interacción básica con micro:bit

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

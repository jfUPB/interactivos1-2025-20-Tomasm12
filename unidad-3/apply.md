# Unidad 3


## 🛠 Fase: Apply

## Actividad 06

``` python
let password = ['A','B','A'];
let keyEntered = []; 
let keyIndex = 0; 
let count = 20;
let startTime;
let state = "CONFIG"; 

function setup () { 
  createCanvas(400, 400); 
  background(220);
  startTime = millis();
  textAlign(CENTER, CENTER);
  textSize(40);
}

function draw () { 
  background(0);
  
  if (state === "CONFIG") { 
    fill(0, 0, 200);
    text("CONFIG", width / 2, height / 3);
    text(count, width / 2, height / 2);
  }
  
  else if (state === "ARMED") { 
    fill(200, 0, 0);
    text("ARMED", width / 2, height / 3);

    if (millis() - startTime > 1000) { 
      count--; 
      startTime = millis();
    }

    text(count, width / 2, height / 2);

    if (count <= 0) {
      state = "EXPLODED";
    }
  }

  else if (state === "EXPLODED") {
    fill(0, 200, 0);
    text("EXPLODED", width / 2, height / 2);
  }
}

function keyPressed() { 
  let k = key.toUpperCase(); 
  if (state === "CONFIG") { 
    if (k === 'A') {
      count = min(count + 1, 60); 
    }
    if (k === 'B') {
      count = max(count - 1, 10);
    }
    if (k === 'S') { 
      state = "ARMED";
      startTime = millis();
    }
  }
  
  else if (state === "ARMED") {
    if (k === 'A' || k === 'B') {
      passwordInput(k);
    }
  }
  
  else if (state === "EXPLODED") {
    if (k === 'R') { 
      count = 20;
      state = "CONFIG";
      startTime = millis();
    }
  }
}

// FUNCION PARA MANEJAR LA CLAVE
function passwordInput(k) {
  keyEntered[keyIndex] = k;
  keyIndex++;

  if (keyIndex === password.length) {
    let passIsOK = true;
    for (let i = 0; i < password.length; i++) {
      if (keyEntered[i] !== password[i]) {
        passIsOK = false;
        break;
      }
    }

    if (passIsOK) {
      count = 20;
      state = "CONFIG";
    }
    keyIndex = 0;
    keyEntered = [];
  }
}
```
## Actividad 07


[Enlace al editor de p5.js](https://editor.p5js.org/Tomasm12/sketches/B7xhzXYqT)

**Código p5.js**

``` python
let password = ['A', 'B', 'A'];
let keyEntered = [];
let keyIndex = 0;
let count = 20;
let startTime;
let state = "CONFIG";

let port;
let reader;
let connectBtn;

function setup() {
  createCanvas(400, 400);
  startTime = millis();
  textAlign(CENTER, CENTER);
  textSize(32);
  connectBtn = createButton("Conectar micro:bit");
  connectBtn.position(10, 10);
  connectBtn.mousePressed(initSerial);
}

function draw() {
  background(0);

  if (state === "CONFIG") {
    fill(0, 0, 200);
    text("CONFIG", width / 2, height / 3);
    text(count, width / 2, height / 2);
    text("A=+1 B=-1 S=Armar", width / 2, height - 50);
  }

  else if (state === "ARMED") {
    fill(200, 0, 0);
    text("ARMED", width / 2, height / 3);

    if (millis() - startTime > 1000) {
      count--;
      startTime = millis();
    }

    text(count, width / 2, height / 2);
    if (count <= 0) state = "EXPLODED";
  }

  else if (state === "EXPLODED") {
    fill(200);
    text("EXPLODED", width / 2, height / 2);
    text("R para reiniciar", width / 2, height - 50);
  }
}

function keyPressed() {
  handleInput(key.toUpperCase());
}

async function initSerial() {
  if ("serial" in navigator) {
    try {
      port = await navigator.serial.requestPort();
      await port.open({ baudRate: 115200 });
      reader = port.readable.getReader();
      listenToSerial();
    } catch (err) {
      console.error(err);
    }
  }
}

async function listenToSerial() {
  while (true) {
    const { value, done } = await reader.read();
    if (done) break;
    const input = new TextDecoder().decode(value).trim();
    if (input) handleInput(input);
  }
}

function handleInput(k) {
  if (state === "CONFIG") {
    if (k === 'A') count = min(count + 1, 60);
    if (k === 'B') count = max(count - 1, 10);
    if (k === 'S') {
      state = "ARMED";
      startTime = millis();
    }
  }

  else if (state === "ARMED") {
    if (k === 'A' || k === 'B') {
      passwordInput(k);
    }
  }

  else if (state === "EXPLODED") {
    if (k === 'R') {
      count = 20;
      state = "CONFIG";
      startTime = millis();
    }
  }
}

function passwordInput(k) {
  keyEntered[keyIndex] = k;
  keyIndex++;

  if (keyIndex === password.length) {
    let passIsOK = true;
    for (let i = 0; i < password.length; i++) {
      if (keyEntered[i] !== password[i]) {
        passIsOK = false;
        break;
      }
    }
    if (passIsOK) {
      count = 20;
      state = "CONFIG";
    }
    keyIndex = 0;
    keyEntered = [];
  }
}
```

**Código del micro:bit.**
``` python
from microbit import *
import utime

uart.init(baudrate=115200)

while True:
    if button_a.was_pressed():
        uart.write("A\n")
    if button_b.was_pressed():
        uart.write("B\n")
    if accelerometer.was_gesture("shake"):
        uart.write("S\n")
    if pin_logo.is_touched():
        uart.write("R\n")
    utime.sleep_ms(100)

```

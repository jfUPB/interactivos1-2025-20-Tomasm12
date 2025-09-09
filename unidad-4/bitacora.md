
# Evidencias de la unidad 4

## Código

[Enlace a la aplicación a modificar](https://editor.p5js.org/generative-design/sketches/Bkqe595pkN)

Código a modificar:

``` js
// P_2_0_02
//
// Generative Gestaltung – Creative Coding im Web
// ISBN: 978-3-87439-902-9, First Edition, Hermann Schmidt, Mainz, 2018
// Benedikt Groß, Hartmut Bohnacker, Julia Laub, Claudius Lazzeroni
// with contributions by Joey Lee and Niels Poldervaart
// Copyright 2018
//
// http://www.generative-gestaltung.de
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.

/**
 * drawing with a changing shape by draging the mouse.
 *
 * MOUSE
 * position x          : length
 * position y          : thickness and number of lines
 * drag                : draw
 *
 * KEYS
 * del, backspace      : erase
 * s                   : save png
 */
'use strict';

function setup() {
  createCanvas(720, 720);
  noFill();
  background(255);
  strokeWeight(2);
  stroke(0, 25);
}

function draw() {
  if (mouseIsPressed && mouseButton == LEFT) {
    push();
    translate(width / 2, height / 2);

    var circleResolution = int(map(mouseY + 100, 0, height, 2, 10));
    var radius = mouseX - width / 2;
    var angle = TAU / circleResolution;

    beginShape();
    for (var i = 0; i <= circleResolution; i++) {
      var x = cos(angle * i) * radius;
      var y = sin(angle * i) * radius;
      vertex(x, y);
    }
    endShape();

    pop();
  }
}

function keyReleased() {
  if (keyCode == DELETE || keyCode == BACKSPACE) background(255);
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
}

```

[Enlace a la aplicación modificada](https://editor.p5js.org/Tomasm12/sketches/G374NZHLK)

Código modificado:

``` js
'use strict';

let port;
let connectBtn;
let connectionInitialized = false;
let microBitConnected = false;

let microBitX = 0;
let microBitY = 0;
let microBitAState = false;
let microBitBState = false;
let prevmicroBitAState = false;
let prevmicroBitBState = false;

let sides = 5;
let radius = 50;

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(255);
  strokeWeight(2);
  stroke(0,25);
  noFill();

  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(10, 10);
  connectBtn.mousePressed(connectBtnClick);
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
    connectionInitialized = false;
  } else {
    port.close();
  }
}

function updateButtonStates(newAState, newBState) {
  // Botón A MANTENIDO → dibujar figura continuamente
  if (newAState === true) {
    drawShape();
    print("A mantenido → Dibujando figura");
  }

  // Botón B PRESIONADO → borrar lienzo (solo al presionar)
  if (newBState === true && prevmicroBitBState === false) {
    background(255);
    print("B presionado → Borrar lienzo");
  }

  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}

function draw() {
  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
    microBitConnected = false;
  } else {
    microBitConnected = true;
    connectBtn.html("Disconnect");

    if (port.opened() && !connectionInitialized) {
      port.clear();
      connectionInitialized = true;
    }

    if (port.availableBytes() > 0) {
      let data = port.readUntil("\n");
      if (data) {
        data = data.trim();
        let values = data.split(",");
        if (values.length === 4) {
          microBitX = int(values[0]);
          microBitY = int(values[1]);
          microBitAState = values[2].toLowerCase() === "true";
          microBitBState = values[3].toLowerCase() === "true";

          // Eje Y (arriba/abajo) → número de lados
          let newSides = int(map(microBitY, -1024, 1024, 3, 12));
          sides = constrain(newSides, 3, 12);

          // Eje X (izquierda/derecha) → radio
          radius = map(microBitX, -1024, 1024, 20, 200);
          radius = constrain(radius, 20, 200);

          updateButtonStates(microBitAState, microBitBState);
        } else {
          print("No se están recibiendo 4 datos del micro:bit");
        }
      }
    }
  }
}

function drawShape() {
  push();
  translate(width / 2, height / 2); // Centro del lienzo

  let angle = TAU / sides;

  beginShape();
  for (let i = 0; i <= sides; i++) {
    let x = cos(angle * i) * radius;
    let y = sin(angle * i) * radius;
    vertex(x, y);
  }
  endShape(CLOSE);

  pop();
}


```

## Video

[Video demostratativo](https://youtu.be/8PJHvC5degc)




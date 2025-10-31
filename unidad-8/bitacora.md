
# Evidencias de la unidad 8





1. Referentes visuales

Para la propuesta se tomó como referencia la estética de visualizadores musicales reactivos como MilkDrop y VSXu, además de proyectos interactivos con ondas y luces dinámicas realizadas en p5.js. Estos referentes inspiraron la construcción de un entorno visual sensible a los estímulos del usuario.

2. Concepto de las visuales

El sistema genera una composición visual basada en luces flotantes y ondas que reaccionan a la canción “A Million Miles Away”.
El concepto representa una sensación de distancia emocional y movimiento constante, donde los colores, las luces y las ondas varían con las acciones del usuario.

3. Control del sistema

Desde el móvil:
Se controlan dos variables:

Número de luces.

Intensidad de las olas.
Estos parámetros se envían mediante Socket.IO al servidor, que los transmite al cliente de escritorio.

Desde el micro:bit:

- Botón A: cambia el color de los elementos visuales.

- Botón B: cambia el color del fondo.

Agitar: genera ondas en las luces y movimiento en las olas.

<img width="1600" height="868" alt="image" src="https://github.com/user-attachments/assets/2778ac19-e538-4111-9aca-88c36b06cc94" />


Diamgrama 
<img width="1075" height="675" alt="image" src="https://github.com/user-attachments/assets/0fad4cd0-9982-4aff-8098-f2cb700bea5d" />

Eventos:

Micro:bit envía “shake”, “buttonA”, “buttonB”.

Móvil envía “luces” y “olas”.

Servidor retransmite estos eventos al escritorio para modificar las visuales.

### APPLY
1. Documentación del proceso

Durante la construcción del sistema se implementaron los siguientes componentes:

Servidor Node.js: encargado de manejar las conexiones mediante Socket.IO. Recibe los eventos del móvil y del micro:bit y los redistribuye al cliente de escritorio.

Cliente móvil (p5.js): interfaz responsiva que envía en tiempo real los parámetros de control (número de luces y amplitud de olas) al servidor.

Cliente de escritorio (p5.js): genera las visuales del sistema, modificando color, posición y comportamiento de ondas según los eventos recibidos.

Micro:bit (MakeCode / MicroPython): envía eventos físicos (botones A, B y movimiento) a través del puerto serial. El servidor interpreta estos mensajes y los convierte en eventos para las visuales.

Durante la implementación aparecieron varias dificultades, principalmente porque no había completado la Unidad 7, por lo que algunos conceptos como el uso de Dev Tunnels y la lectura de puertos seriales no estaban totalmente claros.
A continuación se describen cuatro errores principales, sus causas y las soluciones aplicadas.

Nota: El sistema fue probado parcialmente en entorno local. No se logró verificar la funcionalidad completa con móvil, escritorio y micro:bit conectados simultáneamente debido a limitaciones de tiempo y recursos.

2. Errores detectados y soluciones
Error 1 – Fallo al abrir el puerto serial

Problema:
El servidor mostraba un error al iniciar (Error: cannot open COM5) porque la ruta del puerto serial estaba fija y no coincidía con la del micro:bit real.
Solución:
Se añadió una variable de entorno (SERIAL_PATH) y manejo de errores para evitar que el servidor se detuviera si no encontraba el puerto.
```Python
// Solución aplicada
const SERIAL_PATH = process.env.SERIAL_PATH || null;
if (SERIAL_PATH) {
  try {
    const port = new SerialPort({ path: SERIAL_PATH, baudRate: 115200 });
    const parser = port.pipe(new Readline({ delimiter: '\n' }));
    parser.on('data', line => io.emit('microbit', line.trim()));
  } catch (err) {
    console.error('No se pudo abrir el puerto serial:', err.message);
  }
}
```
Error 2 – Conexión Socket.IO fallida con Dev Tunnels

Problema:
El cliente móvil no se conectaba al servidor cuando se usaba la URL HTTPS generada por Dev Tunnels.
Solución:
Se configuró la conexión para aceptar explícitamente la URL pública del servidor.

// Solución aplicada
```Python
const SERVER_URL = window.SERVER_URL || 'https://mi-tunel.devtunnels.ms';
socket = io(SERVER_URL);
```
Error 3 – Coordenadas táctiles fuera de rango

Problema:
Las luces en el escritorio se movían de forma errática porque el móvil enviaba coordenadas sin normalizar.
Solución:
Se normalizaron las coordenadas antes de enviarlas y se validaron al recibirlas.

Solución aplicada
```Python
socket.emit('movil', { 
  x: constrain(mouseX / width, 0, 1), 
  y: constrain(mouseY / height, 0, 1) 
});
```
Error 4 – Carga de scripts en orden incorrecto

Problema:
En algunos navegadores, el socket no se inicializaba correctamente porque los scripts se cargaban en desorden.
Solución:
Se reorganizó el orden en el HTML y se agregó verificación antes de usar io().
```Python
<script src="/socket.io/socket.io.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.6.0/p5.min.js"></script>
<script src="sketch.js"></script>
```
3. Resultado y limitaciones

Tras corregir los errores, el sistema logró comunicarse correctamente entre móvil → servidor → escritorio.
El micro:bit respondió en pruebas locales cuando se especificó correctamente el puerto serial.
No obstante, no se verificó completamente la integración simultánea (móvil + micro:bit + escritorio) debido a problemas de tiempo y configuración del entorno remoto.




a. Servidor 
```Python
Archivo: server.js

const express = require('express');
const http = require('http');
const { Server } = require('socket.io');
const SerialPort = require('serialport');
const Readline = require('@serialport/parser-readline');

const app = express();
const server = http.createServer(app);
const io = new Server(server);

app.use(express.static('public'));
server.listen(3000, () => console.log('Servidor en http://localhost:3000'));

// --- Configuración del puerto serial para micro:bit ---
const port = new SerialPort({ path: 'COM5', baudRate: 115200 }); 
const parser = port.pipe(new Readline({ delimiter: '\n' }));

parser.on('data', data => {
  const evento = data.trim();
  console.log('Evento micro:bit:', evento);
  io.emit('microbit', evento);
});

io.on('connection', socket => {
  console.log('Cliente conectado');

  socket.on('movil', data => {
    io.emit('movil', data);
  });

  socket.on('disconnect', () => console.log('Cliente desconectado'));
});
```
b. Cliente móvil (p5.js)
```Python
Archivo: public/movil/sketch.js

let socket;
let luces = 10;
let olas = 5;

function setup() {
  createCanvas(windowWidth, windowHeight);
  socket = io();

  createP("Número de luces:");
  lucesSlider = createSlider(5, 50, 10);
  lucesSlider.input(() => enviarDatos());

  createP("Intensidad de olas:");
  olasSlider = createSlider(1, 20, 5);
  olasSlider.input(() => enviarDatos());
}

function enviarDatos() {
  let data = {
    luces: lucesSlider.value(),
    olas: olasSlider.value()
  };
  socket.emit('movil', data);
}
```
c. Cliente escritorio (p5.js)

```Python
Archivo: public/escritorio/sketch.js

let socket;
let luces = 10;
let olas = 5;
let colorLuces;
let colorFondo;

function setup() {
  createCanvas(windowWidth, windowHeight);
  socket = io();
  colorLuces = color(255, 200, 0);
  colorFondo = color(0, 0, 50);

  socket.on('movil', data => {
    luces = data.luces;
    olas = data.olas;
  });

  socket.on('microbit', evento => {
    if (evento === 'A') colorLuces = color(random(255), random(255), random(255));
    if (evento === 'B') colorFondo = color(random(255), random(255), random(255));
    if (evento === 'shake') generarOnda();
  });
}

function draw() {
  background(colorFondo);
  for (let i = 0; i < luces; i++) {
    let x = (i * width) / luces;
    let y = height / 2 + sin(frameCount * 0.05 + i) * olas * 5;
    fill(colorLuces);
    noStroke();
    ellipse(x, y, 20);
  }
}

function generarOnda() {
  olas = random(5, 20);
}
```


Versión MicroPython:

```Python
from microbit import *

while True:
    if button_a.is_pressed():
        print("A")
        sleep(300)
    if button_b.is_pressed():
        print("B")
        sleep(300)
    if accelerometer.was_gesture("shake"):
        print("shake")
        sleep(300)
```


## Autoevaluación — Unidad 8

| **Criterio** | **Descripción** | **Calificación (0–5)** | **Justificación** |
|---------------|------------------|-------------------------|-------------------|
| **Seek** | Investigación inicial y definición del concepto interactivo. | **3.8** | Se realizó la búsqueda de referentes y la definición del objetivo del proyecto, aunque no se profundizó en algunos aspectos técnicos por falta de tiempo. |
| **Actividad 1** | Diseño del flujo y diagramas de interacción entre los componentes. | **3.8** | Se completó el diagrama y la relación entre móvil, servidor y escritorio, pero la documentación pudo ser más clara en la parte visual. |
| **Actividad 2** | Implementación del sistema con Node.js, p5.js y micro:bit. | **3.0** | Se desarrolló gran parte del código, sin embargo, la integración final no pudo ser verificada completamente por errores en la conexión entre el micro:bit y el servidor. |
| **Evidencia (Bitácora)** | Registro del proceso, errores y soluciones aplicadas. | **3.5** | La bitácora documenta las pruebas, fallos y correcciones, aunque no se incluye evidencia funcional completa del sistema. |

---

Nota final propuesta:3.5 / 5.0


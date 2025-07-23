# Unidad 1

## 🔎 Fase: Set + Seek 

## Actividad 01
¿Qué es un sistema físico interactivo?  
Es un sistema que combina sensores, tecnología y objetos físicos para que las personas puedan interactuar con ellos en tiempo real. O sea, cosas que reaccionan cuando uno las toca, mueve o hace algo, como sensores de movimiento, pantallas táctiles o controles que responden al cuerpo.  

¿Cómo podrías aplicar lo que has visto en tu perfil profesional?  
En mi carrera, que es Ingeniería en Diseño de Entretenimiento Digital, y enfocándome en animación, puedo usar este tipo de sistemas para crear experiencias más inmersivas.

Por ejemplo:  
- Hacer lugares donde las animaciones reaccionen al movimiento de la gente.

- Usar sensores para capturar los gestos o movimientos de alguien y animarlos en tiempo real.

- Diseñar entornos interactivos en videojuegos o en experiencias de realidad virtual, donde la animación responda a lo que hace el usuario.
  
- me ayuda a hacer que mis animaciones no solo se vean bien, sino que también respondan e interactúen con las personas.

## Actividad 02

¿Qué es el diseño/arte generativo?  
El diseño generativo es una forma de crear arte y visuales usando programacion, algoritmos y datos. En lugar de diseñar todo dde forma manual, se crean sistemas que generan resultados visuales de forma automatica, respondiendo a inputs como datos del entorno, comportamiento del usuario o incluso decisiones aleatorias.  
Este tipo de diseño se trata de combinar creatividad con programación, permitiendo que cada resultado sea único y cambiante. tambine esto no se enfoca solo en hacer algo bonito, si no de hacer una experiencia para los usuarios.  


¿Cómo podrías aplicar lo que has visto en tu perfil profesional?  

- Crear animaciones que cambian según los datos (que pueda cambiar con el clima, con los sonidos o con movimientos de gente).    
- Hacer narrativas dinámicas, donde una historia animada cambia dependiendo de elecciones, sonidos, emociones o sensores conectados.  
- Integrar arte generativo en videojuegos, instalaciones  o VR , haciendo que cada experiencia sea unica.  

## Actividad 03

En este sistemas físico interactivo identifica los inputs, outputs y el proceso.  
- Inputs
  - Botón A
  - Botón B
  - sacudida el micro:bit
  - Botón “Send Love” de la pagina web
- Outputs
  - cambia el color
  - mostrar el caracter pedido como el corazon en el micro:bit
- Proceso
  - El micro:bit detecta las entradas (botones o sacudida) y envía una letra por puerto serial (A, B o C).
  - El programa hecha en p5.js recibe esa letra y cambia el color.
  - Si se presiona el botón “Send Love”, se envía una letra "h" al micro:bit, que muestra un corazón en la pantalla.

## Actividad 04
```
function setup() {
  createCanvas(400, 400);
  noStroke();
  background(120,10);
}

function draw() {
  background(0, 30); 

  for (let i = 0; i < 50; i++) {
    let angle = frameCount * 0.02 + i;
    let x = width / 2 + cos(angle) * random(50, 150);
    let y = height / 2 + sin(angle) * random(50, 150);

    fill(random(255), random(255), random(255), 150);
    circle(x, y, random(5, 15));
  }
}
```
<img width="783" height="553" alt="image" src="https://github.com/user-attachments/assets/31bda173-7775-418d-9b2f-255342531dd3" />

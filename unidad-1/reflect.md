# Unidad 1

## 🤔 Fase: Reflect
# Actividad 7
## Parte 1: recuperación de conocimiento (Retrieval Practice)

**Basándote en los ejemplos que vimos de sistemas físicos interactivos al iniciar el curso, describe las tres características que definen a un sistema físico interactivo.**
- **Inputs**: es cuando el sistema capta información del entorno mediante sensores o algún objeto físico como un botón.
- **Outputs**: el sistema responde a la persona o al sistema de alguna forma que se pueda ver.
- **Proceso**: la información se interpreta y toma alguna forma dependiendo de la programación.

**Explica el modelo input-process-output de Patrick Hübner usando como ejemplo el sistema que construiste con micro:bit y p5.js en la Actividad 06. ¿Cuál fue el input, cuál fue el proceso y cuál fue el output?**
Input: Presionar el botón A o B del micro:bit.
Proceso: El micro:bit detecta qué botón se presiona y envía un mensaje (“A” o “B”). Luego, en p5.js, el programa recibe ese dato y se mueve a la derecha o izquierda dependiendo de qué letra se presione.
Output: El círculo en la pantalla se mueve a la izquierda o a la derecha.

**¿Cuál es la función de la línea uart.write('A') en el código del micro:bit y qué función en p5.js se encarga de “escuchar” ese mensaje?**
La función sirve en micro:bit para mandar la letra A desde el micro:bit a la computadora, para que esta sepa que el botón A fue presionado.

La función en p5.js que sirve para escuchar ese mensaje creo que sería `port.read();`

**¿Cuál es la diferencia fundamental entre el arte/diseño tradicional y el arte/diseño generativo?**
La diferencia principal puede ser que el arte/diseño tradicional es algo estático, normalmente solo una persona es la que hace y controla la obra, mientras que el arte/diseño generativo es algo más interactivo, capaz de cambiar en tiempo real, dependiendo de los datos introducidos o interacciones de usuarios con sensores.

**Imagina que quieres que un círculo en p5.js cambie a un color aleatorio cada vez que sacudes el micro:bit. Describe qué tendrías que programar en el micro:bit y qué tendrías que programar en p5.js para lograrlo.**
Primero, en el micro:bit tengo que programar una forma de detectar el movimiento, así cuando se sacuda este le pueda mandar un mensaje (como una letra) a la computadora indicando que está siendo sacudido. Ya en p5.js debo crear un canvas donde salga un círculo. Además, debo programar una forma para que p5.js lea el mensaje que le llega y que cada vez que el micro:bit sea sacudido, el círculo cambie de color a uno aleatorio.

## Parte 2: reflexión sobre tu proceso (Metacognición)

**¿Qué fue más desafiante para ti en esta unidad: la parte conceptual (entender qué es un sistema físico interactivo) o la parte técnica (hacer que el micro:bit y p5.js se comunicaran)? ¿Por qué?**
La parte técnica se me complicó más, ya que toca trabajar con dos programas y esperar que lo que hice en el micro:bit funcione, y que p5.js sea capaz de leer y entender lo que le pedí, y que me dé el resultado esperado. Además, a mí aún se me complica programar cosas.


**Describe el momento “¡Aha!” que tuviste cuando lograste que una acción en el micro:bit (presionar un botón, sacudirlo) tuviera un efecto visible en el canvas de p5.js por primera vez. ¿Qué fue lo que entendiste en ese instante?**
Ese momento fue cuando por fin logré que el círculo se moviera con la tecla B. Antes, había programado el micro:bit para que enviara otra letra, así que p5.js no tenía ninguna forma de entender el mensaje que le estaba llegando. Después de devolverme y cambiar eso en el micro:bit, logré que todo funcionara. Eso me ayudó a ver que siempre hay que revisar qué cosa le estoy pidiendo al micro:bit que envíe y qué cosa le estoy pidiendo a p5.js que lea.

**Al inicio de la unidad te pregunté: “¿Este curso para qué me sirve?”. Después de experimentar y construir tu primer prototipo, ¿Cómo ha cambiado o se ha vuelto más concreta tu respuesta a esa pregunta?**

Pues, siendo estudiante de Ingeniería en Diseño de Entretenimiento Digital, esta tecnología me puede servir bastante, ya que mi propósito es ser capaz de crear productos que entretengan a la gente. También quiero lograr que la experiencia sea aún más inmersiva usando sensores y haciendo que el usuario interactúe con lo que cree.


**El tutorial de la Actividad 05 te llevó paso a paso. ¿Cómo te sentiste con ese método de aprendizaje? ¿Te dio seguridad o preferirías haberlo intentado por tu cuenta desde el principio?**

Me gustó que me mostrara el paso a paso. Sí me dio seguridad y se me hizo más fácil entender la actividad.

# Actividad 8  

[Coevaluación compañera](https://github.com/jfUPB/interactivos1-2025-20-VanDiosa/blob/unidad1/apply/unidad-1/apply.md)

Comparación con el trabajo de mi compañero

Ambos usamos un código muy parecido, pero hay algunas diferencias importantes:

- Mi compañero agregó `display.show(Image.COW)` en el micro:bit para mostrar una imagen. para verificar si la informacion si esta funcionando
- También usó un `sleep(100)` que hace que el movimiento del círculo sea más rápido y fluido.
- Su código está un poco más limpio.

¿Qué aprendí?

Aprendí que es útil mostrar una imagen en el micro:bit para confirmar que está enviando datos. También que un `sleep` más corto hace que el movimiento sea más suave.

¿Qué hice yo?

Yo controlé el movimiento de un círculo en p5.js usando los botones A y B del micro:bit. Si se presiona A, el círculo va a la izquierda, y si se presiona B, va a la derecha. Mi enfoque fue más simple, sin imagen ni mucha interacción visual en el micro:bit.

# Actividad 9

Continuar: ¿Qué actividad, video o ejemplo de esta unidad te resultó más inspirador o te ayudó más a entender el potencial de los sistemas físicos interactivos?
El vidoe que mostaron en clase del pianista y la persona que se encargaba de los sistemas físicos interactivos.

Dejar de hacer: ¿Hubo alguna parte que te pareció demasiado abstracta, muy rápida o confusa? ¿Hay algo que crees que podríamos cambiar para que sea más claro?
No tanto, solo al inicio como funcionaba micro.bit y p5.js
Empezar a hacer: ¿Qué te genera más curiosidad ahora? ¿Te gustaría explorar más sensores del micro:bit (luz, temperatura), crear visualizaciones más complejas en p5.js o ver más ejemplos de proyectos artísticos?

Me gustaria crear visualizaciones más complejas y que estas puedan cambiar con sensores.

Balance inspiración vs. técnica: ¿Cómo sentiste el equilibrio entre ver los videos inspiradores de la Actividad 01 y la parte técnica de conectar las herramientas en las actividades 03-06?

Me parecio bine hecho primero mostra el potencial de lo que podemos hacer y como lo podiamos usar y depues introducirnos a esta tecnologia con actividades sensillas 

Comentario adicional: ¿Hay algo más que quieras compartir sobre tu experiencia en esta unidad introductoria?
No

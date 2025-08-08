# Unidad 2


## 🤔 Fase: Reflect

## Actividad 06

**Parte 1: recuperación de conocimiento (Retrieval Practice)**

**1. Describe con tus palabras qué es una máquina de estados. ¿Cuáles son sus cuatro componentes fundamentales que has utilizado en esta unidad?
Aquí tienes tus respuestas simplificadas y con un tono más de estudiante de pregrado, como si fueran para un trabajo de clase:**

Una máquina de estados es una forma de organizar un sistema que cambia entre diferentes situaciones (estados) según lo que pase (eventos).
Los cuatro componentes que usamos son:

Estados: los diferentes modos o situaciones en los que puede estar el sistema.
Eventos: cosas que pasan y que pueden provocar un cambio de estado.
Transiciones: las reglas que dicen a qué estado ir cuando ocurre un evento.
Acciones: lo que hace el sistema cuando entra a un estado o cuando sucede un evento.


**2. Explica por qué la técnica de máquina de estados es tan útil para gestionar la “concurrencia” (atender un temporizador y botones “al mismo tiempo”) en un dispositivo con un solo hilo de ejecución como el micro:bit. ¿Qué problema soluciona en comparación con usar funciones como sleep()?**
El micro:bit solo ejecuta una cosa a la vez. Con la máquina de estados se revisan continuamente todos los eventos (botones, tiempo, sensores) sin bloquear el programa.
Esto evita usar "sleep()", que detiene todo, y permite que el micro:bit pueda “escuchar” y reaccionar a varias cosas casi al mismo tiempo.


**3. Imagina que tienes que añadir una nueva funcionalidad a la bomba temporizada: si se agita (shake) el micro:bit mientras la cuenta regresiva está activa, el tiempo se reduce a la mitad. ¿Cómo modificarías tu diagrama de máquina de estados para incluir este nuevo evento y acción?**
Agregaria 
- Acciones:
  - `tiempo = tiempo / 2` (asegurando que sea al menos 1 segundo).
  - Actualizar el display para mostrar el nuevo tiempo.
- Diagrama: Se añadió una flecha desde el estado *Armada* que regresa a sí mismo (self-loop) con la etiqueta:  
  SHAKE a tiempo = tiempo / 2, actualizar display.

**4. Explica qué es un “vector de prueba” y por qué es una herramienta crucial para verificar que una máquina de estados funciona como se espera.**
Un vector de prueba es una lista de casos con eventos y el resultado esperado.
Sirve para comprobar que la máquina de estados funciona bien, encontrar errores y asegurarse de que responde bien incluso en situaciones raras.






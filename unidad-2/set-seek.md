# Unidad 2

## 🔎 Fase: Set + Seek  

## Actividad 01
**Describe detalladamente cómo funciona este ejemplo.**

El programa controla dos píxeles que parpadean en la micro:bit. Cada píxel tiene su propio intervalo de tiempo (1000 ms y 500 ms) y funciona con una máquina de estados que alterna su brillo entre apagado (0) y encendido (9) según el tiempo transcurrido.


**¿Cuáles son los estados en el programa?**
- Init: Inicializa el tiempo y dibuja el píxel.

- WaitTimeout:  Espera el intervalo y cambia el brillo.

**¿Cuáles son los eventos/inputs en el programa?**

el eventos de temporizador Cuando `utime.ticks_diff()` supera el valor de `interval`, y cunaod eso pasa cambia el brillo del pixel.


**¿Cuáles son las acciones en el programa?**
- Guardar el tiempo actual.

- Mostrar el píxel en pantalla.

- Alternar el brillo entre encendido y apagado.

- Cambiar de estado.
  
## Actividad 02

```python
from microbit import *
import utime

class Semaforo:
    def __init__(self):
        self.state = "Rojo"
        self.startTime = 0
        self.interval = 2000  
        self.pos_rojo = (0, 2)
        self.pos_amarillo = (2, 2)
        self.pos_verde = (4, 2)

    def update(self):
        if self.state == "Rojo":
            display.clear()
            display.set_pixel(self.pos_rojo[0], self.pos_rojo[1], 9)
            self.startTime = utime.ticks_ms()
            self.state = "WaitRojo"

        elif self.state == "WaitRojo":
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.interval:
                self.state = "Amarillo"

        elif self.state == "Amarillo":
            display.clear()
            display.set_pixel(self.pos_amarillo[0], self.pos_amarillo[1], 9)
            self.startTime = utime.ticks_ms()
            self.interval = 1000
            self.state = "WaitAmarillo"

        elif self.state == "WaitAmarillo":
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.interval:
                self.state = "Verde"

        elif self.state == "Verde":
            display.clear()
            display.set_pixel(self.pos_verde[0], self.pos_verde[1], 9)
            self.startTime = utime.ticks_ms()
            self.interval = 2000
            self.state = "WaitVerde"

        elif self.state == "WaitVerde":
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.interval:
                self.state = "Rojo"

semaforo = Semaforo()

while True:
    semaforo.update()
```
*Estados*

- Rojo: Se muestra el LED rojo encendido.

- WaitRojo: Espera a que pase el tiempo del estado rojo.

- Amarillo: Se muestra el LED amarillo encendido.

- WaitAmarillo: Espera a que pase el tiempo del estado amarillo.

- Verde: Se muestra el LED verde encendido.

- WaitVerde: Espera a que pase el tiempo del estado verde.

**Eventos**

- Timeout: Cuando el tiempo definido para cada estado se cumple, se dispara el cambio al siguiente estado.

Acciones
- display.clear(): Apaga los LEDs anteriores.

- display.set_pixel(x, y, 9): Enciende el LED correspondiente al color del semáforo.

- utime.ticks_ms() y utime.ticks_diff(): Controlan el tiempo para cambiar de estado.

## Actividad 03

**1. Explica por qué decimos que este programa permite realizar de manera concurrente varias tareas.
   El programa es concurrente porque en el bucle while True verifica de forma continua dos tareas:**

- Eventos de usuario `(button_a.was_pressed())`

- Eventos temporizados `(utime.ticks_diff(...) > interval)`

Esto permite responder a ambos sin bloquear la ejecución.El sistema no se bloquea esperando un solo evento, sino que evalúa constantemente ambos tipos de condiciones, dando la sensación de que realiza múltiples tareas al mismo tiempo

**2. Identifica los estados, eventos y acciones en el programa.**

*Estados*

- STATE\_INIT (inicializa el sistema)
- STATE\_HAPPY (muestra imagen feliz)
- STATE\_SMILE (muestra sonrisa)
- STATE\_SAD (muestra imagen triste)

Eventos

- button\_a.was\_pressed(): cambio manual de estado 
- utime.ticks\_diff(...) > interval: cambio automático de estado por tiempo.

Acciones

- Mostrar imagen en pantalla (display.show(Image.X)).
- Reiniciar temporizador (start\_time = utime.ticks\_ms()).
- Definir intervalo (interval = X\_INTERVAL).
- Actualizar el estado (current\_state = STATE\_X).


**3. Describe y aplica al menos 3 vectores de prueba para el programa. Para definir un vector de prueba debes llevar al sistema a un estado, generar los eventos y observar el estado siguiente y las acciones que ocurrirán. Por tanto, un vector de prueba tiene unas condiciones iniciales del sistema, unos resultados esperados y los resultados realmente obtenidos. Si el resultado obtenido es igual al esperado entonces el sistema pasó el vector de prueba, de lo contrario el sistema puede tener un error.**

**Vector 1**: STATE\_HAPPY → STATE\_SMILE (tiempo)

- Inicio: `STATE_HAPPY`, `interval = 1500 ms`.
- Evento: sin pulsar botón, pasan 1600 ms.
- Esperado/Obtenido: cambia a `STATE_SMILE`, muestra `SMILE`, actualiza `start_time` y `interval = 1000 ms`. **PASA**


**Vector 2**: STATE\_HAPPY → STATE\_SAD (botón)

- Inicio: `STATE_HAPPY`, `interval = 1500 ms`.
- Evento: botón A a los 500 ms.
- Esperado/Obtenido: cambia a `STATE_SAD`, muestra SAD, actualiza `start_time` y `interval = 2000 ms`. **PASA**



**Vector 3**: STATE\_SAD → STATE\_HAPPY (tiempo)

- Inicio: `STATE_SAD`, `interval = 2000 ms`.
- Evento: sin pulsar botón, pasan 2100 ms.
- Esperado/Obtenido: cambia a `STATE_HAPPY`, muestra HAPPY, actualiza `start_time` y `interval = 1500 ms`. **PASA**

No estoy muy seguro si entendi esta parte 3 correcto pero supuse que era hacer algo asi.



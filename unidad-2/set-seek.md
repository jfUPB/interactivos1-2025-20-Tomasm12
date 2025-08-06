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
**Estados**

Rojo: Se muestra el LED rojo encendido.

WaitRojo: Espera a que pase el tiempo del estado rojo.

Amarillo: Se muestra el LED amarillo encendido.

WaitAmarillo: Espera a que pase el tiempo del estado amarillo.

Verde: Se muestra el LED verde encendido.

WaitVerde: Espera a que pase el tiempo del estado verde.

**Eventos**

Timeout: Cuando el tiempo definido para cada estado se cumple, se dispara el cambio al siguiente estado.

Acciones
display.clear(): Apaga los LEDs anteriores.

display.set_pixel(x, y, 9): Enciende el LED correspondiente al color del semáforo.

utime.ticks_ms() y utime.ticks_diff(): Controlan el tiempo para cambiar de estado.



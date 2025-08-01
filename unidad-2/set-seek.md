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

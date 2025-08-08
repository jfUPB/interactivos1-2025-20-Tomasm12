# Unidad 2


## 🛠 Fase: Apply

## Actividad 04

**Construye un diagrama detallado de la máquina de estados, incluyendo estados, eventos, transiciones y acciones.**
<img width="741" height="984" alt="image" src="https://github.com/user-attachments/assets/dad0d3d3-9713-49ba-8752-e29656f04817" />

## Actividad 05

**1.El código que implementa la bomba temporizada.**
``` python
from microbit import *
import utime
import music

STATE_SET_TIME = 0
STATE_COUNTDOWN = 1
STATE_EXPLODE = 2

COUNTDOWN_INTERVAL = 1000

current_state = STATE_SET_TIME
start_time = 0
time_left = 20
interval = COUNTDOWN_INTERVAL

while True:
    if current_state == STATE_SET_TIME:
        display.show(str(time_left))
        if button_a.was_pressed() and time_left < 60:
            time_left += 1
        if button_b.was_pressed() and time_left > 10:
            time_left -= 1
        if accelerometer.was_gesture("shake"):
            start_time = utime.ticks_ms()
            current_state = STATE_COUNTDOWN
    elif current_state == STATE_COUNTDOWN:
        if utime.ticks_diff(utime.ticks_ms(), start_time) >= interval:
            time_left -= 1
            display.show(str(time_left))
            start_time = utime.ticks_ms()
        if time_left <= 0:
            current_state = STATE_EXPLODE
        if pin_logo.is_touched():
            current_state = STATE_SET_TIME
            time_left = 20
    elif current_state == STATE_EXPLODE:
        display.show(Image.SKULL)
        music.play(music.POWER_DOWN)
        utime.sleep_ms(2000)
        current_state = STATE_SET_TIME
        time_left = 20

```

1. Ajuste del tiempo mínimo y máximo
  
- Acción: En el modo de configuración, presionar varias veces el botón B para disminuir el tiempo y el botón A para aumentarlo.
- Resultado esperado: El tiempo no debe bajar de 10 segundos ni subir de 60 segundos.

2. Armar la bomba

- Acción: En el modo de configuración, realizar el gesto de shake (sacudir el micro:bit).

- Resultado esperado: El sistema debe iniciar la cuenta regresiva y mostrar el tiempo en la pantalla.

3. Cuenta regresiva correcta

- Acción: Iniciar la bomba y dejar que la cuenta regresiva avance sin interrupciones.

- Resultado esperado: El tiempo debe disminuir de uno en uno cada segundo hasta llegar a cero.

4. Explosión

- Acción: Dejar que la cuenta regresiva llegue a cero.

- Resultado esperado: En la pantalla aparece la imagen de una calavera y se reproduce un sonido de explosión o tono descendente.

5. Regresar a configuración

- Acción: Durante la cuenta regresiva, tocar el logo táctil del micro:bit.

- Resultado esperado: El sistema debe volver al modo de configuración y reiniciar el tiempo a 20 segundos.

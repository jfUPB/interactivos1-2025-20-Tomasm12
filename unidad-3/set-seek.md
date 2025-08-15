# Unidad 3

## 🔎 Fase: Set + Seek


## Actividad 05

| Estado inicial         | Evento disparador | Acciones                                      | Estado final           |
|------------------------|-------------------|----------------------------------------------|------------------------|
| Apagada                | A                 | Encender bomba                                 | Encendida              |
| Encendida              | B                 | Iniciar temporizador de cuenta regresiva     | Cuenta regresiva       |
| Cuenta regresiva       | S                 | Pausar temporizador                            | Pausada                |
| Pausada                | T                 | Reanudar temporizador                        | Cuenta regresiva       |
| Cuenta regresiva       | Tiempo = 0        | Activar explosión                                | Explosión              |
| Explosión              | A                 | Reiniciar sistema                                | Apagada                |


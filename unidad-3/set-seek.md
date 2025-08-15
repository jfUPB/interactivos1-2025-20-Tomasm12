# Unidad 3

## 🔎 Fase: Set + Seek



Qué ventajas tiene usar una clase (class) en este caso para representar un semáforo?

Permite reutilizar código, organizarlo mejor, crear semáforos con distintos tiempos/posiciones y mantener todo en un solo lugar para facilitar cambios.

Puedes ver cómo la técnica de programación con máquinas de estado y el uso de funciones no bloqueantes te permite que varios semáforos funcionen al mismo tiempo?

Cada semáforo controla su propio estado y tiempo sin usar sleep(), lo que permite que todos funcionen en paralelo con sus propios ritmos.

## Actividad 05

| Estado inicial         | Evento disparador | Acciones                                      | Estado final           |
|------------------------|-------------------|----------------------------------------------|------------------------|
| Apagada                | A                 | Encender bomba                                 | Encendida              |
| Encendida              | B                 | Iniciar temporizador de cuenta regresiva     | Cuenta regresiva       |
| Cuenta regresiva       | S                 | Pausar temporizador                            | Pausada                |
| Pausada                | T                 | Reanudar temporizador                        | Cuenta regresiva       |
| Cuenta regresiva       | Tiempo = 0        | Activar explosión                                | Explosión              |
| Explosión              | A                 | Reiniciar sistema                                | Apagada                |



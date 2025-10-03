
# Evidencias de la unidad 6
### Actividad 01

**¿Qué ocurrió en la terminal cuando ejecutaste npm install? ¿Cuál crees que es su propósito?**

Se descargaron e instalaron 120 paquetes necesarios para el proyecto. Apareció un aviso de que algunos paquetes buscan financiación y que hay una nueva versión de npm disponible. No se encontraron errores ni vulnerabilidades.

<img width="544" height="258" alt="image" src="https://github.com/user-attachments/assets/b3ee0aaa-b05a-456b-b3b8-fa3e705c8f2b" />

Propósito del comando:

El comando `npm install` descarga e instala todas las dependencias definidas en el archivo `package.json` del proyecto. Esto prepara el entorno con las librerías necesarias para que el proyecto pueda ejecutarse correctamente.

**¿Qué mensaje específico apareció en la terminal después de ejecutar npm start? ¿Qué indica este mensaje?**

<img width="573" height="159" alt="image" src="https://github.com/user-attachments/assets/dc5aaa9c-8e7a-41f8-a3ee-d86797e397fb" />

sale que esta escuchando, el proyecto se puso en marcha y ahora hay un servidor en tu máquina que atiende las solicitudes web en el puerto 3000. El mensaje indica que puedes abrir tu navegador y conectarte a esa dirección.

**Describe lo que ves inicialmente en page1 y page2 en tu navegador.**

se observa dos circulos rojos concetados desde sus centro por una linea negra

**¿Qué mensajes aparecieron en la terminal del servidor cuando abriste page1 y page2?**

<img width="614" height="240" alt="image" src="https://github.com/user-attachments/assets/f29a6e6b-f5f9-432b-a5ae-858951956dc1" />

<img width="668" height="361" alt="image" src="https://github.com/user-attachments/assets/9877c68f-e2d9-4798-8734-5fd5ebaaba73" />

Aparecieron mensajes indicando que un usuario se conectó con un ID, que el servidor recibió información sobre la ventana del navegador (posición y tamaño), además de mensajes de depuración mostrando cuántos clientes había conectados, qué página habían abierto y el estado de sincronización.

**Describe qué sucede en ambas páginas del navegador cuando mueves una de las ventanas. ¿Cambia algo visualmente? ¿Qué mensajes aparecen (si los hay) en la consola del navegador (usualmente accesible con F12 -> Pestaña Consola) y en la terminal del servidor?**

cunaod se mueve una de las ventanas los circulos se mueven pero permanece concetado por la linea recta,, la linea se mantiene recta y simpre "conectada" al otro circulo 

en la terminal  los mensajes muestran las coordenadas (x, y), el tamaño de las ventanas y si cambia , y confirma que ambos sigan conectados

<img width="652" height="348" alt="image" src="https://github.com/user-attachments/assets/94fc7b3b-93de-4e0d-91dd-3d6f3b80f236" />

En el navegador aparecen mensajes como “Sync status: SYNCED” y “Received valid remote data”, esto nos dice que los datos si se estan recibiendo de forma correcta y estan sinedo aplicados en cada pestaña.

<img width="2175" height="827" alt="image" src="https://github.com/user-attachments/assets/ba40caa2-6337-45e6-9578-41e99037de7f" />

### Actividad 02

**Piensa en cómo te conectas a Internet en casa o en la Universidad. ¿Usas Wi-Fi? ¿Un cable de red? Eso es simplemente tu “rampa de acceso” a la gran red de carreteras. ¿Qué pasaría si esa rampa se corta? Anota tus ideas.**

Si en mi casa o en la universidad se corta la conexión (ya sea el Wi-Fi o el cable de red), mi computador o celular no podría entrar a la “carretera” que es Internet. Eso significa que no tendría acceso a páginas web, plataformas, aplicaciones en línea ni comunicación por correo o mensajería. En otras palabras, mi vehículo (el navegador o la app) estaría listo, pero no tendría por dónde circular.

**¿Puedes identificar otros ejemplos de relaciones Cliente-Servidor en tu vida diaria (no necesariamente digitales)? Por ejemplo, al pedir comida en un restaurante. ¿Quién es el cliente y quién el servidor? ¿Qué se pide y qué se entrega?**

- Restaurante: El cliente es la persona que pide la comida. El mesero (servidor) toma la orden y entrega los platos preparados por la cocina.

- Biblioteca física: El lector (cliente) solicita un libro. El bibliotecario (servidor) busca y entrega el libro.

- Supermercado: El comprador (cliente) pide un producto en caja o mostrador, y el cajero/empleado (servidor) lo entrega.

- Transporte público: El pasajero (cliente) solicita un viaje. El conductor (servidor) ofrece el servicio de transporte.

En todos los casos, la lógica es la misma: alguien hace una petición (Cliente) y alguien más responde con el servicio o producto (Servidor).


**Toma la URL de tu sitio web favorito. Intenta identificar el protocolo, el nombre de dominio y la ruta (si la hay). ¿Qué crees que pasa si solo escribes el nombre de dominio (ej. www.google.com) sin una ruta específica? ¿Qué “página por defecto” crees que te envía el servidor?**

Ejemplo (usando YouTube):

URL: https://www.youtube.com/watch?v=dQw4w9WgXcQ

Protocolo: https://

Nombre de dominio: www.youtube.com

Ruta: /watch?v=dQw4w9WgXcQ

¿Qué pasa si escribo solo el dominio (www.youtube.com)?
El servidor me envía la página principal por defecto, normalmente un archivo llamado index.html o una vista inicial definida en el sitio. En este caso sería la página de inicio de YouTube con recomendaciones de videos.

**Compara HTTP con los protocolos seriales que usaste.
¿Qué similitudes encuentras?
¿Qué diferencias clave ves?
¿Por qué crees que HTTP necesita ser más complejo que un simple envío de bytes como hacías con el micro:bit?**

Similitudes:

- Ambos definen reglas de comunicación entre dos partes (Cliente ↔ Servidor o micro:bit ↔ p5.js).

- Necesitan un idioma común para que los mensajes tengan sentido.

- Siguen una estructura: se envía un mensaje, se espera una respuesta.

Diferencias:

- Los protocolos seriales son más simples, básicamente envían bytes o caracteres en un flujo directo.

- HTTP es más complejo, incluye cabeceras, métodos (GET, POST…), códigos de estado (200, 404…), y tipos de contenido (HTML, JSON, imágenes, etc.).

- En serial, la comunicación es más “cruda”, mientras que HTTP es estructurado y estandarizado a nivel global.
  
es complejo porque en la web se transmiten muchos tipos de recursos (texto, imágenes, videos, datos dinámicos) y es necesario un protocolo que pueda describir qué se pide, en qué formato se envía y cómo responder a diferentes situaciones. No bastaría con enviar solo bytes sin contexto.


**Piensa en una página web simple, como un formulario de login.
¿Qué parte crees que es HTML (ej. los campos de texto, el botón)?
¿Qué parte es CSS (ej. el color del botón, el tipo de letra)?
¿Qué parte es JavaScript (ej. la comprobación de si escribiste algo antes de enviar, el mensaje de “contraseña incorrecta” que aparece sin recargar la página)?**

- HTML: Los campos de texto para usuario y contraseña, y el botón de “Iniciar sesión”.

- CSS: El color del botón, la fuente de los textos, el tamaño y alineación de los campos.

- JavaScript: Validar que los campos no estén vacíos antes de enviar, mostrar el mensaje “Contraseña incorrecta” sin recargar la página.

**Compara el bucle draw() de p5.js con este modelo de “esperar a que algo pase y reaccionar”.
¿Qué ventajas crees que tiene el modelo basado en eventos para una interfaz de usuario web?
¿Sería eficiente tener un bucle draw() redibujando toda la página 60 veces por segundo si nada ha cambiado?**

Ventaja del modelo basado en eventos: Es más eficiente porque solo se ejecuta código cuando ocurre algo (clic, mensaje, cambio de tamaño).

Si redibujáramos 60 veces/seg sin cambios: Sería un gasto enorme de recursos y energía, y la página funcionaría más lenta innecesariamente.

**¿Por qué crees que podría ser útil usar JavaScript tanto en el cliente (navegador) como en el servidor? ¿Se te ocurre alguna ventaja para los desarrolladores?**

Por qué es útil usar JS en cliente y servidor: Porque los desarrolladores pueden usar un solo lenguaje para ambos lados, lo que simplifica el aprendizaje, evita tener que cambiar de lenguaje y permite compartir parte del código entre cliente y servidor.

**Resume con tus propias palabras la diferencia fundamental entre una comunicación HTTP tradicional y una comunicación usando WebSockets/Socket.IO. ¿En qué tipo de aplicaciones has visto o podrías imaginar que se usa esta comunicación en tiempo real?**

La diferencia principal entre la comunicación tradicional con HTTP y la que se hace con WebSockets es que HTTP funciona como un intercambio de cartas: el navegador pide algo y el servidor responde, y para cada nueva acción hay que repetir ese ciclo. En cambio, con WebSockets se abre una especie de “línea telefónica” que queda siempre activa entre el cliente y el servidor, lo que permite que ambos se envíen información en tiempo real sin necesidad de hacer nuevas peticiones. Socket.IO facilita mucho este proceso, ya que ofrece funciones sencillas para enviar y recibir mensajes. Este tipo de comunicación se utiliza en aplicaciones donde la rapidez es clave, como los chats en línea, los videojuegos multijugador o las herramientas colaborativas como Google Docs, donde necesitas ver de inmediato lo que hacen otras personas.

### Actividad 03

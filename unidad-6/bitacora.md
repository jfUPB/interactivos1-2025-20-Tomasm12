
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

**Detén el servidor si está corriendo.
Cambia la primera ruta de /page1 a /pagina_uno.
Inicia el servidor.**

<img width="586" height="239" alt="image" src="https://github.com/user-attachments/assets/395b5684-d793-463e-983d-8479f2a82f7d" />

**Intenta acceder a http://localhost:3000/page1. ¿Funciona?**

al intentar iniciar con http://localhost:3000/page1 no funciona


**Ahora intenta acceder a http://localhost:3000/pagina_uno. ¿Funciona?**

ahora con http://localhost:3000/pagina_uno si funciona 

<img width="2064" height="989" alt="image" src="https://github.com/user-attachments/assets/533f85e7-36d5-4462-8c05-8f40b39a5540" />

**¿Qué te dice esto sobre cómo el servidor asocia URLs con respuestas? Restaura el código.**

El servidor solo puede responder a las direcciones que han sido definidas en su código. Si en el navegador se escribe una URL distinta a la programada, como /page1 en lugar de /pagina_uno, no encuentra coincidencia y devuelve un error. Esto muestra que la relación entre las URLs y las respuestas no es automática, sino que depende de las rutas que el programador haya configurado explícitamente en el servidor.



**Abre http://localhost:3000/page1 en una pestaña. Observa la terminal del servidor. ¿Qué mensaje ves? Anota el ID.**

<img width="722" height="130" alt="image" src="https://github.com/user-attachments/assets/f9e14320-9fd1-4fa9-96fd-8aa1544aa93e" />

A user connected - ID: nZvG7JkxLh0X4n_8AAAB

En la terminal aparece un mensaje indicando que un usuario se conectó junto con un ID único. Ese ID sirve para identificar a cada cliente que entra al servidor.

**Abre http://localhost:3000/page2 en OTRA pestaña. Observa la terminal. ¿Qué mensaje ves? ¿El ID es diferente?**

<img width="689" height="93" alt="image" src="https://github.com/user-attachments/assets/a987b65d-9b00-4119-b5f7-d29f9cc34776" />

A user connected - ID: 0VgDVIOUbYXoRRQKAAAD
la terminal muestra que el servidor está activo y que un usuario se conectó con un ID único. También indica que la conexión proviene de la página 2 y registra los datos de esa ventana.

Si el ID  es diferente al que salio con page 1


**Cierra la pestaña de page1. Observa la terminal. ¿Qué mensaje ves? ¿Coincide el ID con el que anotaste?**

<img width="483" height="69" alt="image" src="https://github.com/user-attachments/assets/8ccca9d4-49fd-4a69-a67e-8e5498ebec6d" />

User disconnected - ID: nZvG7JkxLh0X4n_8AAAB
sale un mensaje que el usuario se desconceto y el ID concide con el del comienzo

**Cierra la pestaña de page2. Observa la terminal.**

<img width="387" height="32" alt="image" src="https://github.com/user-attachments/assets/a910cd26-a613-4aef-9a36-e6fb5701f76b" />
User disconnected - ID: 0VgDVIOUbYXoRRQKAAAD
sucede lo mismo el usuario se desconecta y el ID coincide



**Mueve la ventana de page1. Observa la terminal del servidor. ¿Qué evento se registra (win1update o win2update)? ¿Qué datos (Data:) ves?**

<img width="719" height="123" alt="image" src="https://github.com/user-attachments/assets/e5d2f2a2-f14c-497e-9914-fb8f10e07005" />

En la terminal aparece el evento Received win1updatecon, ademas sale los datos de la posición y tamaño de la ventana 
Received win1update from ID: EQHxQUDmTma4K9jAAAAD Data: { x: 1126, y: 211, width: 1146, height: 1260 }

**Mueve la ventana de page2. Observa la terminal. ¿Qué evento se registra ahora? ¿Qué datos ves?**

<img width="719" height="124" alt="image" src="https://github.com/user-attachments/assets/9b5e1c4b-7344-4fb3-bcb6-36a286d22af2" />

Ahora se registra en win2update y de nuevo muestra la posicion, lo ancho y la altura
Received win2update from ID: _MTnFI0ULRsLmp1KAAAB Data: { x: 1802, y: 380, width: 1146, height: 1260 }

**Experimento clave: cambia socket.broadcast.emit(‘getdata’, page1); por socket.emit(‘getdata’, page1); (quitando broadcast). Reinicia el servidor, abre ambas páginas. Mueve page1. ¿Se actualiza la visualización en page2? ¿Por qué sí o por qué no? (Pista: ¿A quién le envía el mensaje socket.emit?). Restaura el código a broadcast.emit.**

<img width="566" height="369" alt="image" src="https://github.com/user-attachments/assets/bd793c06-dfb1-46b7-939e-2661127e7221" />

Cuando moví page1, el servidor recibió el evento y lo mostró en consola, pero no se reflejó en page2 porque con socket.emit(...) solo responde al mismo cliente que envía. En cambio, usando socket.broadcast.emit(...) el servidor comparte la información con los demás y así ambas páginas se sincronizan.

**Cambia const port = 3000; a const port = 3001;.**

<img width="363" height="90" alt="image" src="https://github.com/user-attachments/assets/c583a092-990c-4fde-90b7-9931e4e08430" />

**Inicia el servidor. ¿Qué mensaje ves en la consola? ¿En qué puerto dice que está escuchando?**
Server is listening on http://localhost:3001


**Intenta abrir http://localhost:3000/page1. ¿Funciona?
Intenta abrir http://localhost:3001/page1. ¿Funciona?**
Ninguno de los 2 funciona 

<img width="1354" height="780" alt="image" src="https://github.com/user-attachments/assets/c28c8b8b-1d5b-4a52-85c8-077a77dbc688" />

**¿Qué aprendiste sobre la variable port y la función listen? Restaura el puerto a 3000.**

Aprendí que la variable port define el número de puerto en el que el servidor escucha las conexiones, y la función listen se encarga de iniciarlo en ese puerto. Si intento entrar con otro puerto diferente al configurado, la conexión falla porque no hay ningún servidor atendiendo ahí.

### Actividad 04

**Abre page2.html en tu navegador (con el servidor corriendo).**

**Abre la consola de desarrollador (F12).**

<img width="1254" height="366" alt="image" src="https://github.com/user-attachments/assets/e605b4a5-270b-441d-a2ab-5b55e051d795" />

**Detén el servidor Node.js (Ctrl+C).**

<img width="1242" height="541" alt="image" src="https://github.com/user-attachments/assets/80619a0f-d749-40ae-ab7c-6fc9065e6867" />

**Refresca la página page2.html. Observa la consola del navegador. ¿Ves algún error relacionado con la conexión? ¿Qué indica?**


<img width="1268" height="753" alt="image" src="https://github.com/user-attachments/assets/62a8f9d3-f60d-4c4d-9d16-506f06cd6ff2" />

me sale que no se puede acceder al sitio 

Vuelve a iniciar el servidor y refresca la página. ¿Desaparecen los errores?


<img width="1266" height="486" alt="image" src="https://github.com/user-attachments/assets/c03cb669-5691-44d3-a9cf-e132a6c26521" />

si el error desaparece y digue funcionando de forma normal 



**Comenta la línea socket.emit(‘win2update’, currentPageData, socket.id); dentro del listener connect.**

<img width="644" height="296" alt="image" src="https://github.com/user-attachments/assets/6eff0cdd-5078-472d-8454-ebb40971db54" />

**Reinicia el servidor y refresca page1.html y page2.html.**

<img width="731" height="145" alt="image" src="https://github.com/user-attachments/assets/03677058-d3dc-41a3-acef-1c8b9b44c4cd" />

**Mueve la ventana de page2 un poco para que envíe una actualización.**

<img width="2241" height="1071" alt="image" src="https://github.com/user-attachments/assets/f5c5f2ea-58de-437f-b53e-1996fcf2b4b9" />

<img width="1159" height="960" alt="image" src="https://github.com/user-attachments/assets/a84ae6eb-57c9-4d6e-bb4d-29cf39a50685" />

**¿Qué pasó? ¿Por qué?**

Al reiniciar el servidor, page1 y page2 se sincronizaron al inicio (se mostraban unidos por la línea). Pero al mover page2, sus cambios no llegaron a page1, así que dejaron de estar sincronizados. Al comentar la línea socket.emit(...) en checkWindowPosition(), page2 solo envió su posición inicial en setup, pero ya no pudo actualizar en tiempo real.


**Mueve la ventana de page1. Observa la consola del navegador de page2. ¿Qué datos muestra?**


<img width="1077" height="923" alt="image" src="https://github.com/user-attachments/assets/2fe71b47-7f08-404b-9339-c9d2f9ef8850" />

salen varios mensajes diciendo que recibio datos validos  y que esta "synced"

Mueve la ventana de page2. Observa la consola de page1. ¿Qué pasa? ¿Por qué?

<img width="1092" height="987" alt="image" src="https://github.com/user-attachments/assets/fa2ce9c5-bcd2-4396-832e-f9691a297c18" />

En la consola de page1 aparecen mensajes que corresponden a las coordenadas de page2. Esto sucede porque cada ventana, cuando detecta un cambio en su posición, genera un evento propio (win1update o win2update) que es enviado al servidor. El servidor, a su vez, redistribuye esa información a la otra ventana, que la recibe y la imprime en su consola.

De esta manera, ambas páginas permanecen en constante sincronización, ya que cada una conoce en tiempo real la ubicación de la otra gracias al intercambio de eventos a través del servidor.




**Observa checkWindowPosition() en page2.js y modifica el código del if para comprobar si el código dentreo de este se ejecuta.**

<img width="542" height="325" alt="image" src="https://github.com/user-attachments/assets/3ffc9cae-a546-4076-8a05-f2cd20affe18" />

**Mueve cada ventana y observa las consolas.**

<img width="1014" height="996" alt="image" src="https://github.com/user-attachments/assets/4185c106-44fc-4682-8383-fe6d551f862f" />

**¿Qué puedes concluir y por qué?**

Al modificar el if en checkWindowPosition() de page2.js y mover las ventanas, se comprobó que el código dentro del if se ejecuta cada vez que cambia la posición o tamaño de la ventana. Además, cada página recibe correctamente los datos enviados por la otra, lo que demuestra que la sincronización es bidireccional y funciona en tiempo real.


**Cambia el background(220) para que dependa de la distancia entre las ventanas. Puedes calcular la magnitud del resultingVector usando let distancia = resultingVector.mag(); y luego usa map() para convertir esa distancia a un valor de gris o color. background(map(distancia, 0, 1000, 255, 0)); (ajusta el rango 0-1000 según sea necesario).**

<img width="2223" height="1032" alt="image" src="https://github.com/user-attachments/assets/a79a3d90-8344-47dc-b41b-591b166dce1b" />

``` java
function draw() {
    // Crear los vectores de posición
    let vector2 = createVector(remotePageData.x, remotePageData.y);
    let vector1 = createVector(currentPageData.x, currentPageData.y);
    let resultingVector = createVector(vector2.x - vector1.x, vector2.y - vector1.y);

    // Calcular la distancia entre ventanas
    let distancia = resultingVector.mag();

    // Mapear la distancia a un rango de color (0-1000 px → gris 255-0)
    let bgColor = map(distancia, 0, 1000, 255, 0); 
    background(bgColor);

    if (!isConnected) {
        showStatus('Conectando al servidor...', color(255, 165, 0));
        return;
    }
    
    if (!hasRemoteData) {
        showStatus('Esperando conexión de la otra ventana...', color(255, 165, 0));
        return;
    }
    
    if (!isFullySynced) {
        showStatus('Sincronizando datos...', color(255, 165, 0));
        return;
    }

    // Solo dibujar cuando esté completamente sincronizado
    drawCircle(point2[0], point2[1]);
    checkWindowPosition();

    stroke(50);
    strokeWeight(20);
    drawCircle(resultingVector.x + remotePageData.width / 2, resultingVector.y + remotePageData.height / 2);
    line(point2[0], point2[1], resultingVector.x + remotePageData.width / 2, resultingVector.y + remotePageData.height / 2);
}

```
**Inventa otra modificación creativa.**

<img width="2199" height="810" alt="image" src="https://github.com/user-attachments/assets/30b3b5fe-3433-4b17-b6ef-e6f3fcc4561a" />
<img width="689" height="708" alt="image" src="https://github.com/user-attachments/assets/d48c9f40-469b-4180-a569-e206b0a88ded" />


``` java
function draw() {
    // Crear los vectores de posición
    let vector2 = createVector(remotePageData.x, remotePageData.y);
    let vector1 = createVector(currentPageData.x, currentPageData.y);
    let resultingVector = createVector(vector2.x - vector1.x, vector2.y - vector1.y);

    // Calcular la distancia entre ventanas
    let distancia = resultingVector.mag();

    // Mapear la distancia a un rango de gris para el fondo
    let bgColor = map(distancia, 0, 1000, 255, 0); 
    background(bgColor);

    // Mapear la distancia al tamaño de los círculos (mín 50px, máx 200px)
    let circleSize = map(distancia, 0, 1000, 200, 50);

    if (!isConnected) {
        showStatus('Conectando al servidor...', color(255, 165, 0));
        return;
    }
    
    if (!hasRemoteData) {
        showStatus('Esperando conexión de la otra ventana...', color(255, 165, 0));
        return;
    }
    
    if (!isFullySynced) {
        showStatus('Sincronizando datos...', color(255, 165, 0));
        return;
    }

    // Solo dibujar cuando esté completamente sincronizado
    drawCircle(point2[0], point2[1], circleSize);
    checkWindowPosition();

    stroke(50);
    strokeWeight(20);
    drawCircle(resultingVector.x + remotePageData.width / 2, resultingVector.y + remotePageData.height / 2, circleSize);
    line(point2[0], point2[1], resultingVector.x + remotePageData.width / 2, resultingVector.y + remotePageData.height / 2);
}

function drawCircle(x, y, size = 150) {
    fill(255, 0, 0);
    ellipse(x, y, size, size);
}

```

### Actividad 05
Explica tu idea y realiza algunos bocetos.

Idea: introvertido 
cunaod un amigo ser aserca uno inicia a usar su bateria peronal pero entre mas serca esta bateria mas se gasta 
- un circulo se asercara a otro y este cambiara de color, y entre mas serca cambiara a un color mas oscuro, ademas el ecenario cambiara tambien de tonalidad para mostrar el desgaste de la perona 
Implementa tu idea.

Incluye todos los códigos (servidor y clientes) en tu bitácora.
``` java
// Variables para animación del círculo remoto
let remoteSize = 150;
let remoteBrightness = 255;
let isRetreating = false;
```

``` java
if (distancia < 300) {
    background(0); // pantalla negra si se acercan
    remoteSize = map(distancia, 0, 300, 50, 150);
    ...
} else {
    background(map(distancia, 0, 1000, 255, 50)); 
}

```

``` java
if (!isRetreating && distancia < 100) {
    isRetreating = true;
    remoteBrightness = 150; // menos brillante
    setTimeout(() => {
        remoteBrightness = 255; // vuelve brillante
        remoteSize = 200;       // crece más
        setTimeout(() => {
            remoteSize = 150;   // regresa normal
            isRetreating = false;
        }, 1500);
    }, 1500);
}


```

``` java 
function drawCircle(x, y, c, s) {
    fill(c);
    noStroke();
    ellipse(x, y, s, s);
}

```
``` java 
let currentPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
}

let previousPageData = { ...currentPageData };
let remotePageData = { x: 0, y: 0, width: 100, height: 100 };
let point2 = [currentPageData.width / 2, currentPageData.height / 2];
let socket;
let isConnected = false;
let hasRemoteData = false;
let isFullySynced = false;

// Variables para animación del círculo remoto
let remoteSize = 150;
let remoteBrightness = 255;
let isRetreating = false;

function setup() {
    createCanvas(windowWidth, windowHeight);
    frameRate(60);
    socket = io();

    socket.on('connect', () => {
        console.log('Connected with ID:', socket.id);
        isConnected = true;
        socket.emit('win2update', currentPageData, socket.id);
        setTimeout(() => { socket.emit('requestSync'); }, 500);
    });

    socket.on('getdata', (response) => {
        if (response && response.data && isValidRemoteData(response.data)) {
            remotePageData = response.data;
            hasRemoteData = true;
            console.log('Received valid remote data:', remotePageData);
            socket.emit('confirmSync');
        }
    });

    socket.on('fullySynced', (synced) => {
        isFullySynced = synced;
        console.log('Sync status:', synced ? 'SYNCED' : 'NOT SYNCED');
    });

    socket.on('peerDisconnected', () => {
        hasRemoteData = false;
        isFullySynced = false;
        console.log('Peer disconnected');
    });

    socket.on('disconnect', () => {
        isConnected = false;
        hasRemoteData = false;
        isFullySynced = false;
        console.log('Disconnected from server');
    });
}

function isValidRemoteData(data) {
    return data && 
           typeof data.x === 'number' && 
           typeof data.y === 'number' && 
           typeof data.width === 'number' && data.width > 0 &&
           typeof data.height === 'number' && data.height > 0;
}

function checkWindowPosition() {
    currentPageData = {
        x: window.screenX,
        y: window.screenY,
        width: window.innerWidth,
        height: window.innerHeight
    };

    if (currentPageData.x !== previousPageData.x || currentPageData.y !== previousPageData.y || 
        currentPageData.width !== previousPageData.width || currentPageData.height !== previousPageData.height) {

        point2 = [currentPageData.width / 2, currentPageData.height / 2]
        socket.emit('win2update', currentPageData, socket.id);
        previousPageData = currentPageData; 
    }
}

function draw() {
    if (!isConnected) {
        background(50);
        showStatus('Conectando al servidor...', color(255, 165, 0));
        return;
    }
    
    if (!hasRemoteData) {
        background(50);
        showStatus('Esperando conexión...', color(255, 165, 0));
        return;
    }
    
    if (!isFullySynced) {
        background(50);
        showStatus('Sincronizando...', color(255, 165, 0));
        return;
    }

    checkWindowPosition();

    let vector2 = createVector(remotePageData.x, remotePageData.y);
    let vector1 = createVector(currentPageData.x, currentPageData.y);
    let resultingVector = createVector(vector2.x - vector1.x, vector2.y - vector1.y);
    let distancia = resultingVector.mag();

    // ----- REACCIONES -----
    if (distancia < 300) {
        // 1. Pantalla negra
        background(0);

        // 2. Reducir tamaño del círculo remoto al acercarse
        remoteSize = map(distancia, 0, 300, 50, 150);

        // 3. Si están muy cerca, activar "retirada y regreso brillante"
        if (!isRetreating && distancia < 100) {
            isRetreating = true;
            remoteBrightness = 150; // se vuelve menos brillante
            setTimeout(() => {
                remoteBrightness = 255; // vuelve brillante
                remoteSize = 200;       // crece más
                setTimeout(() => {
                    remoteSize = 150;   // regresa a tamaño normal
                    isRetreating = false;
                }, 1500);
            }, 1500);
        }
    } else {
        // Fondo normal con efecto de distancia
        background(map(distancia, 0, 1000, 255, 50));
        remoteSize = 150;
        remoteBrightness = 255;
    }

    // Dibujar Page 1 (círculo rojo fijo en el centro local)
    drawCircle(point2[0], point2[1], color(255, 0, 0), 150);

    // Dibujar Page 2 (círculo verde dinámico)
    drawCircle(resultingVector.x + remotePageData.width / 2,
               resultingVector.y + remotePageData.height / 2,
               color(0, remoteBrightness, 0),
               remoteSize);

    // Línea de conexión
    stroke(100);
    strokeWeight(4);
    line(point2[0], point2[1],
         resultingVector.x + remotePageData.width / 2,
         resultingVector.y + remotePageData.height / 2);
}

function showStatus(message, statusColor) {
    textSize(24);
    textAlign(CENTER, CENTER);
    noStroke();
    fill(0, 0, 0, 150);
    rectMode(CENTER);
    let textW = textWidth(message) + 40;
    let textH = 40;
    rect(width / 2, 1*height / 6, textW, textH, 10);
    fill(statusColor);
    text(message, width / 2, 1*height / 6);
}

function drawCircle(x, y, c, s) {
    fill(c);
    noStroke();
    ellipse(x, y, s, s);
}

function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
}

```

<img width="1060" height="683" alt="image" src="https://github.com/user-attachments/assets/92accc39-ed82-4b91-b85c-e137488118a1" />

<img width="1052" height="931" alt="image" src="https://github.com/user-attachments/assets/c99546b3-05ae-41a3-97d3-323153d6cd70" />





### Autoevaluación


| Competencia                                                                                           | Nota | Justificación                                                                                           |
|-------------------------------------------------------------------------------------------------------|------|---------------------------------------------------------------------------------------------------------|
| Configurarás y ejecutarás un servidor básico usando Node.js, Express y Socket.IO.                     | 5    | Lograste configurar y levantar el servidor sin errores, comprendiendo bien la estructura básica.        |
| Implementarás una comunicación en tiempo real entre dos sketches de p5.js utilizando Socket.IO.       | 5    | La comunicación en tiempo real funcionó correctamente y se integró de forma estable entre las ventanas. |
| Analizarás la arquitectura cliente-servidor y el flujo de datos en una aplicación web en tiempo real. | 5  | El análisis fue sólido, y logre entender el flujode datos.         |
| Crearás una nueva aplicación interactiva que utilice comunicación en red.                             | 4.5    | La aplicación tiene algunos problemas pero es funcional .     |

**Nota:** 4.8

# Changelog

Todas las novedades importantes de **WhatsApp Accesible**, versión por versión.
El formato sigue el estilo [Keep a Changelog](https://keepachangelog.com/es/) y las
versiones usan [Versionado Semántico](https://semver.org/lang/es/).

---

## [3.0.0] — 2026-07-25

La actualización más grande hasta ahora. Se revisó la aplicación entera —el motor que habla
con WhatsApp y toda la interfaz— y se corrigieron **unos setenta problemas**. Muchos no eran
fallas ruidosas sino algo peor: la app decía que había hecho algo **y no lo había hecho**.

Están todos acá abajo. Si no te interesa leerlos, no hace falta: se instala igual y no toca
tus chats. Pero preferimos que se pueda saber qué se arregló.

> **Se instala sola** desde cualquier versión 1.2.10 o posterior. Tus chats, tu historial y tu
> sesión quedan intactos.

### 🔐 Seguridad

- **Un archivo recibido ya no se ejecuta con un Enter.** La extensión de lo que te mandan la
  elige quien te lo manda. Si el archivo es un **programa** (`.exe`, `.bat`, `.ps1`, `.msi`,
  `.lnk` y compañía), ahora aparece un aviso que lo dice con todas las letras y hay que
  confirmar. Antes se abría directamente, y con un lector de pantalla no hay forma de notar que
  "informe.pdf.exe" no es un documento.
- **Se cerró un agujero por el que alguien podía dejarte archivos donde quisiera.** El
  identificador de un mensaje también lo elige quien lo envía, y se usaba tal cual como nombre
  de archivo: un identificador armado a propósito escribía **fuera de la carpeta de la
  aplicación** —incluida la carpeta de Inicio de Windows—. Ahora se sanean el nombre y la
  extensión.
- **La misma falla afectaba a los chats exportados** (los nombres dentro del `.zip`), y también
  quedó cerrada.
- **La pestaña Estados** abría archivos sin ese control. Ahora usa el mismo aviso que el chat.

### 🧯 Cosas que se perdían

- **Mensajes que desaparecían al ir hacia atrás en un chat.** La paginación avanzaba por hora, y
  las horas tienen precisión de un segundo: cuando varios mensajes caían en el mismo segundo —lo
  normal en un grupo activo— todos menos uno quedaban **salteados para siempre**. Ahora avanza
  por hora **y** por mensaje.
- **La media borrada no volvía nunca.** Después de usar "Vaciar TODA la media", "Liberar espacio"
  o de mover la carpeta, la nota de voz quedaba **inservible para siempre**: la app seguía
  apuntando a un archivo que ya no existía y no intentaba bajarlo de nuevo.
- **Una nota de voz se podía borrar antes de enviarse.** La limpieza de archivos temporales
  eliminaba el archivo que el mensaje todavía apuntaba, y a veces uno que aún no se había subido.
- **Las encuestas perdían sus votos al recargar el chat** (los datos estaban guardados; lo que
  fallaba era leerlos), y una encuesta reentregada por WhatsApp **borraba el conteo**.
- **La marca "editado" desaparecía al reiniciar**: un mensaje editado quedaba indistinguible del
  original.
- **Un corte de luz podía borrarte todos los ajustes.** El archivo de configuración se escribía
  encima del anterior; si el proceso moría a mitad, arrancabas con todo en cero, dispositivos de
  audio incluidos. Ahora se escribe de forma atómica.

### 🗣️ Cuando algo fallaba, la app no lo decía (o decía lo contrario)

- **Un mensaje enviado sin internet se perdía mientras la app decía "enviado".** El error se
  descartaba si mencionaba la conexión.
- **Reenviar algo que no estaba descargado** decía, de corrido: *"Descargá el archivo antes de
  reenviarlo. Mensaje reenviado."*
- **Una grabación que fallaba anunciaba "Audio enviado"** y dibujaba el mensaje como si hubiera
  salido.
- **Un audio que no se podía reproducir era silencio total** — imposible de distinguir de que la
  app se hubiera colgado.
- **"Guardar como" se colgaba para siempre** si salías del chat mientras se descargaba.
- **Un aviso de Windows rechazado no dejaba nada**: ni sonido, ni voz, ni notificación. El
  mensaje pasaba desapercibido.
- **Agregar a alguien a un grupo fallaba en silencio.** WhatsApp informa los fallos persona por
  persona; se descartaban. Ahora dice quién y por qué (privacidad, no está en WhatsApp, ya está
  en el grupo…).
- **"Eliminar para todos"** avisaba de un fallo con un texto genérico. Ahora dice lo que
  realmente pasó: el mensaje sigue en el chat de la otra persona.
- **Cambiar una configuración del grupo** dejaba la casilla marcada aunque el cambio se hubiera
  rechazado.
- **El diálogo de Privacidad podía mostrarte valores inventados.** Si la consulta fallaba, cada
  opción caía en "Todos" — te decía que tu última vez y tu foto las ve cualquiera cuando quizás
  estaban en "nadie".

### 🔊 Audio

- **Una nota de voz se podía ir al contacto equivocado.** Si salías del chat mientras grababas, la
  grabación seguía viva: el micrófono abierto, el otro recibiendo "grabando audio…" para siempre,
  y el próximo "Enviar audio" mandaba esa grabación **al chat que tuvieras abierto**.
- **Un fallo al abrir el dispositivo podía dejar la reproducción muda** hasta cambiar de
  dispositivo o cerrar el reproductor.
- **Cambiar la velocidad justo cuando arrancaba otro audio** mezclaba las muestras del anterior.
- **Los audios largos se comían toda la memoria**: se decodificaban enteros y sin tope. Ahora hay
  un límite y se avisa si el audio es más largo.
- **Un archivo de música se hacía pasar por nota de voz** ("mensaje de voz (0:00)", sin el
  nombre). Ahora muestra su nombre, y el filtro "Notas de voz" vuelve a funcionar —estaba siempre
  vacío—.
- **Alt+M (escuchar lo grabado)** dejaba armada la cadena de audios: al terminar reproducía sola
  la nota siguiente **y mandaba el recibo de "reproducido"** de algo que nunca escuchaste. Y lo
  reproducía a la velocidad pegada en vez de a 1x.
- **Un video reenviado llegaba como documento**, sin previsualización. También se agregó el envío
  de música como audio reproducible.

### 💬 Mensajes, orden y lectura

- **Un mensaje escrito en varias líneas se leía solo hasta la primera.** Si te mandaban un
  nombre, un documento, una dirección y un teléfono en cuatro renglones, veías **solo el nombre**,
  sin ninguna pista de que faltaba el resto. Afectaba a las cuatro listas (chat, Recientes,
  Destacados y Estados).
- **Los identificadores de tus mensajes se cruzaban** cuando mandabas dos seguidos rápido: a
  partir de ahí, cada cambio de estado, edición o borrado actuaba **sobre el mensaje equivocado**
  —incluido "eliminar para todos"—.
- **Borrar un mensaje eliminaba otro de la vista** si la lista se movía mientras el diálogo estaba
  abierto.
- **La línea "No leídos" desaparecía** al cargar mensajes viejos o al reordenarse, y quedaba mal
  ubicada si habías respondido en el medio.
- **Con la app minimizada, los mensajes no se agregaban al chat abierto** — y al volver se
  marcaban como leídos igual, así que el otro veía "Leído" de algo que no podías ver.
- **Responder con una nota de voz, una foto o un archivo perdía la cita**, y el banner de
  respuesta quedaba armado para el mensaje siguiente.
- **En los grupos, el autor de un mensaje citado era el nombre del grupo.**
- **"Editar" se ofrecía siempre**, incluso pasados los 15 minutos que permite WhatsApp: la edición
  se descartaba pero la app igual reescribía el texto, así que vos veías tu corrección y el otro
  nunca.
- **Dos secciones "Hoy"** si dejabas la app abierta pasada la medianoche.
- **El estado de un mensaje podía ir para atrás** (de "Leído" a "Enviado") cuando WhatsApp lo
  reentregaba.
- **Al responder a un contacto nuevo**, el chat podía quedar con tu propio nombre.
- **El número de una tarjeta de contacto no se mostraba en ningún lado**: recibías un contacto y
  solo veías el nombre.

### 👥 Grupos

- **"Eliminar chat" se quitó de los grupos.** No borraba solo en esta app: hacía desaparecer el
  chat y todos sus mensajes **también del teléfono** y de cualquier dispositivo vinculado, sin
  vuelta atrás, mientras seguías siendo miembro. Quedan "Salir del grupo" y "Vaciar chat", que es
  lo que hace WhatsApp mismo.
- **Podías quedar bloqueado de administrar tu propio grupo.** En los grupos que usan el
  direccionamiento nuevo de WhatsApp, la app no te reconocía como administrador.
- **Un grupo renombrado por otra persona conservaba el nombre viejo para siempre**, y que te
  agregaran, te sacaran o te hicieran administrador pasaba en silencio. Ahora se avisa (y un grupo
  silenciado sigue silencioso: solo se anuncia lo que te afecta a vos).
- **Un grupo recién creado, o al que te acababas de unir, tardaba hasta un minuto en aparecer.**
- **El chat de un grupo eliminado volvía en el siguiente arranque.**
- **Se ofrecía agregar a gente que ya estaba en el grupo.**
- **Un grupo archivado seguía apareciendo** en la pestaña Grupos.
- **Destacar un mensaje recibido no se sincronizaba** con el teléfono.

### 🔌 Conexión, arranque y actualizaciones

- **La actualización automática no se habría instalado.** Al aceptar, el proceso no terminaba de
  cerrarse y el instalador —que espera a que termine— se quedaba esperando para siempre.
- **Si el motor moría, la app seguía como si nada**, sin poder mandar ni recibir, sin decir nada.
  Ahora lo detecta, lo avisa y lo reinicia.
- **Abrir la app sin internet mataba el motor** para toda la sesión. Ahora reintenta.
- **Si desvinculabas el dispositivo desde el teléfono**, la app no se enteraba.
- **Si faltaba un componente** (por ejemplo si el antivirus se lo llevó), hacías doble clic y **no
  pasaba absolutamente nada**: ni ventana, ni error, ni sonido.
- **La pantalla de vinculación era un callejón sin salida**: los códigos vencen al minuto y no
  había forma de pedir otro sin cerrar la aplicación.
- **"Iniciar con Windows" decía "activado" apuntando a una carpeta vieja** después de mover la
  aplicación de lugar.

### 🧭 Navegación y detalles

- **El diálogo "Reenviar a…" no se podía cerrar con Escape** — era el único sin salida por
  teclado.
- **El mini reproductor escondía el control que tenía el foco** sin devolverlo a la lista.
- **El administrador de grupos se abría solo** en un momento cualquiera, después de un pedido
  fallido.
- **Destacados abría los grupos como si fueran chats privados.**
- **Un chat con el silencio ya vencido seguía figurando como silenciado.**
- **Los archivados nunca mostraban su línea de "No leídos".**
- **Las encuestas de varias respuestas** hechas en otro cliente se mostraban como de una sola
  opción.
- **El chat exportado de un grupo se titulaba con su identificador interno** en vez del nombre.
- **Copiar en un audio recibido vaciaba el portapapeles** y anunciaba "Copiado".

### 🛠️ Por dentro

- Se corrigió un fallo que **mataba el motor** (acceso concurrente a datos compartidos) cuando
  alguien renombraba un grupo en el momento justo.
- Las búsquedas de encuestas recorrían la tabla entera de mensajes en cada voto: ahora hay índice.
- La confirmación de envío viaja con una marca propia, para que el estado de un mensaje no pueda
  caer en otro.
- El motor y la interfaz se auditaron en tres rondas independientes, y cada hallazgo se verificó
  releyendo el código antes de darlo por bueno. Se sumaron pruebas automáticas para los arreglos
  que se podían cubrir así.

---

## [2.0.14] — 2026-07-18

### ✨ Nuevo
- **Menú contextual en los chats archivados**: la lista de "Chats archivados" ahora responde a
  la tecla Aplicaciones / clic derecho con el mismo menú que la lista principal —Abrir,
  Desarchivar, Silenciar, Marcar como no leído, Exportar chat, Vaciar chat, Eliminar chat y Salir
  del grupo—. Antes ahí solo se podía Abrir o Desarchivar.

---

## [2.0.13] — 2026-07-18

### ✨ Nuevo
- **Vaciar TODA la media** (Ajustes): un botón que borra todos los audios, notas de voz, fotos,
  videos y documentos descargados, dejando la carpeta solo con lo necesario para funcionar (los
  chats y el historial NO se tocan). A diferencia de "Liberar espacio", este **también** borra las
  notas de voz.

### 🔧 Mejorado
- **Chats y grupos archivados en silencio**: un chat o grupo archivado ya no suena ni avisa cuando
  llega un mensaje (queda como un silenciado). Los mensajes igual llegan y los ves al entrar, pero
  sin interrumpir.

---

## [2.0.12] — 2026-07-17

### 🐛 Corregido
- **Tu mensaje se ubicaba arriba del que te mandaron**: al responder justo después de recibir
  un mensaje, el tuyo a veces aparecía **arriba** en vez de abajo. Pasaba cuando el reloj de tu
  PC estaba un poco atrasado respecto a WhatsApp (tu mensaje quedaba con una hora menor). Ahora
  un mensaje que enviás nunca queda con hora anterior al último del chat, así siempre va **abajo**.

---

## [2.0.11] — 2026-07-16

### 🐛 Corregido
- **Chat de un contacto nuevo tomaba tu nombre**: al responderle a alguien que te escribió
  por primera vez (y no tenés agendado), el chat se **renombraba con tu propio nombre de
  perfil** en vez del de la persona. Ahora el chat conserva el nombre del contacto; si ya
  te quedó mal, se corrige solo con el próximo mensaje que esa persona te mande.

---

## [2.0.10] — 2026-07-16

### 🐛 Corregido
- **"No leídos fantasma"**: a veces un chat avisaba mensajes no leídos (1, o hasta muchísimos
  de golpe), pero al entrar no había nada nuevo —los mismos mensajes de siempre. Pasaba porque
  WhatsApp a veces **re-entrega** mensajes que ya tenías (mismo mensaje, reintentado); el motor
  los volvía a contar como no leídos y a avisar. Ahora un mensaje ya conocido **no vuelve a
  contar ni a avisar**; solo cuentan los realmente nuevos.

---

## [2.0.9] — 2026-07-15

### ✨ Nuevo
- **En grupos, "Enviar mensaje al privado" y "Responder en privado"** desde el menú
  contextual de un mensaje. La primera abre el chat 1 a 1 con quien escribió ese mensaje;
  la segunda abre ese privado **citando** el mensaje del grupo —como el "responder en
  privado" de WhatsApp—, así la otra persona lo ve como una respuesta a su mensaje del
  grupo.

---

## [2.0.8] — 2026-07-15

### 🐛 Corregido
- **Mensajes desordenados al reconectar**: al reabrir la app después de estar un tiempo
  desconectado, en un grupo con muchos no leídos (30-60) WhatsApp los entrega todos juntos
  y, con el chat abierto, algunos caían al fondo fuera de orden (mensajes viejos después de
  los nuevos). Ahora, cuando llega una tanda fuera de orden, la lista **se reacomoda sola por
  horario** apenas termina la ráfaga, dejándote en el mismo mensaje en el que estabas.

---

## [2.0.7] — 2026-07-14

### 🐛 Corregido
- **Cambio de dispositivo de reproducción (Ctrl+P) inestable**: si tenías dos salidas que
  empiezan con la misma palabra (por ejemplo dos "Altavoces …" o dos "Auriculares …"), al
  elegir una se cambiaba a la otra —o no cambiaba—. El código las comparaba solo por la
  primera palabra y agarraba siempre la primera. Ahora selecciona **exactamente** el
  dispositivo que elegís.

---

## [2.0.6] — 2026-07-14

### 🐛 Corregido
- **Error al alternar audios mono/estéreo**: al reproducir un audio con distinta cantidad
  de canales que el anterior (una nota de voz mono y después un audio estéreo, o al revés),
  saltaba un error interno y podía cortar el sonido un instante. Era una condición de
  carrera al reconstruir el reproductor; ya no ocurre.

---

## [2.0.5] — 2026-07-14

### 🐛 Corregido
- **Grupos: salir/eliminar ahora refresca la lista al instante.** Al salir de un grupo,
  quedaba en la lista hasta que hacías otra cosa (salir de otro grupo hacía desaparecer el
  primero). Era un desfasaje: la lista re-agregaba el grupo desde el registro interno de
  WhatsApp, que tarda un instante en enterarse de que saliste. Ahora el grupo **se va al
  toque**.

### 🔧 Mejorado
- Al **"Eliminar chat"** de un grupo, el mensaje de confirmación aclara que eso **solo borra
  el chat de tu lista** y que **seguís siendo miembro** del grupo (para irte de verdad, usá
  **"Salir del grupo"**).

---

## [2.0.4] — 2026-07-13

### 🐛 Corregido
- **Ruido fuerte ("trrr"/"tac", interferencias) al reproducir notas de voz recibidas —
  solucionado de raíz.** La causa real no estaba en cómo se reproducía, sino en cómo se
  **decodificaba**: nuestro decodificador de Opus interpretaba mal ciertos frames (los de
  las partes más fuertes) de algunas notas y generaba esa distorsión. El archivo siempre
  estuvo perfecto (VLC lo tocaba bien). Ahora el audio se decodifica con **libopus** (el
  mismo motor que usa VLC) y las notas suenan limpias, a su calidad nativa.
- **Guardar audios WAV o MP3**: al guardar un audio que te mandan en WAV o MP3, ahora se
  guarda en su **formato original** (antes lo forzaba a opus). Las notas de voz siguen en
  opus.

### 🔧 Mejorado
- La reproducción usa el motor **DirectSound** de Windows (más limpio, como VLC) y toca
  cada audio a su **frecuencia nativa** —una nota de 16 kHz suena como 16 kHz, sin
  inflarla.

---

## [2.0.1] — 2026-07-10

### 🐛 Corregido
- **Ruido fuerte al reproducir notas de voz recibidas** ("trrr"/"tac", como
  interferencias que molestan al oído). La 2.0 forzaba la reproducción a 48000 Hz en
  estéreo; en placas de audio nativas a 44100 Hz (vía el driver MME de Windows) esa
  reconversión metía el ruido. Ahora la reproducción usa el **formato nativo de tu
  placa** y respeta **mono/estéreo del origen** —una nota de voz mono suena como
  mono—, igual que antes de la 2.0. Todo el procesamiento interno del audio ya era
  correcto: el problema estaba solo en cómo se le entregaba al driver.

---

## [2.0.0] — 2026-07-09

**Versión 2.0** — app mucho más liviana y un buen pulido de audio y escritura.

### 🪶 Mucho más liviana
- La descarga pasó de **~63 MB a ~26 MB**: reemplazamos los componentes pesados de audio
  (numpy + libsndfile + PyAV) por un **ffmpeg propio de ~2 MB** (con libopus). Funciona
  igual o mejor.

### ✨ Nuevo
- **Liberar espacio** (Ajustes): borra videos, música, fotos y documentos descargados y
  **conserva las notas de voz**.
- **Filtrar**: "Notas de voz" y "Audios" (música y archivos) quedaron separados.
- **Dispositivos de audio en vivo**: con **Ctrl+P**, cambiar micrófono o auriculares se
  aplica al instante, sin dar Aceptar.
- **Ctrl+Enter / Shift+Enter** hace una nueva línea al escribir (Enter sigue enviando).

### 🔧 Mejorado
- **Notas de voz a 64k** — más nítidas que las típicas de WhatsApp.
- **Pegar texto multilínea** entra completo (antes se cortaba en el primer salto).
- **Reproductor**: al terminar, el audio se desmonta (la flecha izquierda ya no lo
  revive), y Espacio/flechas solo actúan cuando hay un audio cargado.

---

## [1.2.11] — 2026-07-09

### 🔧 Mejorado
- **App más liviana**: reemplazamos un componente de audio pesado (~30 MB) por una
  herramienta propia de ~1 MB. La descarga y las actualizaciones pesan **~25 MB menos**,
  y se elimina de raíz un error que a veces rompía el armado de versiones nuevas. El
  **control de velocidad** de los audios funciona exactamente igual.

### 🗑️ Quitado
- La opción **"estado con foto y música"** (era lo único que usaba ese componente
  pesado). Los estados de **texto, imagen, video y audio** siguen igual.

---

## [1.2.10] — 2026-07-07

### 🐛 Corregido
- **Actualización automática que rompía la app en algunas PCs**: después de actualizar,
  la app no abría (error de "argumento inesperado") porque el instalador dejaba un
  archivo de una versión anterior. Ahora la actualización **limpia lo viejo**
  correctamente, sin tocar tus datos.

---

## [1.2.9] — 2026-07-07

### 🐛 Corregido
- **Confirmación de lectura en vivo**: con un chat abierto, un mensaje nuevo que llega
  ahora se marca como **leído al instante** —antes, a quien te escribió le quedaba en
  "entregado" aunque lo estuvieras viendo.

### ✨ Nuevo
- **"Escribiendo…" y "grabando audio…" salientes**: la otra persona ahora ve tu estado
  cuando escribís o grabás una nota de voz (tu cliente lo mostraba pero no lo enviaba).
  Respeta el modo fantasma.

---

## [1.2.8] — 2026-07-07

### ✨ Nuevo
- **Filtrar el historial**: desde el menú contextual del chat, **"Filtrar"** muestra solo
  los **Enlaces**, las **Fotos y videos**, los **Audios** o los **Documentos** de todo el
  chat. **"Todo"** (o **Escape**) vuelve al chat completo.

### 🔧 Mejorado
- **Escape** ahora sale del chat desde **cualquier lugar** (la lista de mensajes, la caja
  de texto, los botones, la vista de conexión), no solo desde algunos. Mientras grabás,
  Escape cancela la grabación.
- **Búsqueda (Ctrl+F)**: ahora busca en **todo** el historial (lo carga completo antes de
  buscar), así encuentra la palabra esté donde esté —antes solo miraba lo ya cargado.

### 🐛 Corregido
- **Minimizado**: con un chat abierto, al minimizar con Alt+F4, los mensajes que llegan a
  ese chat ahora se anuncian como **"mensaje nuevo"** y quedan como **no leídos** (antes
  leía el contenido y no avisaba). Y ya **no dice "Leído"** mientras está minimizado.

---

## [1.2.7] — 2026-07-06

### 🐛 Corregido
- **Reproducción en estéreo con velocidad alterada**: en audios estéreo (música que te
  mandan, o tus propias grabaciones en estéreo —incluido el monitoreo mientras grabás—),
  poner **1.5x o 2x** en lugar de acelerar **bajaba el tono una octava** y sonaba lento y
  raro (el estéreo quedaba mezclado en un solo canal, al doble de largo). Ahora acelera
  bien, **manteniendo el tono**.

---

## [1.2.6] — 2026-07-06

### 🐛 Corregido
- **Actualizaciones automáticas (crítico)**: por fin se instalan solas. Hasta ahora la
  actualización se descargaba pero **no llegaba a instalarse** —la app se cerraba y
  volvía a abrir en la versión anterior, pidiéndola de nuevo—. Quedó resuelto de raíz
  (el instalador se quedaba sin consola y se cortaba antes de copiar). **Esta es la
  última actualización que hay que instalar a mano; a partir de acá, se actualiza sola.**

> Incluye también lo de la 1.2.5 (avisos de leído/reproducido y el fix del audio
> reenviado), que hasta ahora no había llegado a instalarse por este mismo problema.

---

## [1.2.5] — 2026-07-06

### ✨ Nuevo
- **Aviso por voz de "Leído" / "Reproducido"**: cuando la otra persona lee o reproduce
  tu mensaje en el chat que tenés abierto, ahora te lo dice por voz (además del sonido),
  así te enterás al instante sin tener que ir hasta el mensaje.
- **Confirmación de "reproducido" al escuchar notas de voz**: cuando reproducís una nota
  de voz que te enviaron, ahora le avisamos a quien te la mandó (le aparece el
  "reproducido"), igual que en WhatsApp.

### 🐛 Corregido
- **Reenvío de notas de voz**: al reenviar un audio ya no aparece con duración
  **0 segundos** — conserva su duración real.

---

## [1.2.4] — 2026-07-05

### 🐛 Corregido
- **Instalación de actualizaciones**: en PCs cuya ruta de usuario tiene tildes o eñes
  (por ejemplo `C:\Users\José\…`), la actualización se descargaba pero no llegaba a
  instalarse y volvía a pedirla en cada arranque. Ahora se instala correctamente.
  (Además, el instalador cierra el motor y deja un registro en `data/update.log`.)

---

## [1.2.3] — 2026-07-05

### 🐛 Corregido
- Cambio de dispositivos de audio corregido a fondo: ahora podés cambiar el micrófono
  o el altavoz **las veces que quieras** —y volver a "Predeterminado del sistema"— y
  se aplica al instante. Antes solo tomaba bien el primer cambio y después quedaba
  pegado al anterior.

---

## [1.2.2] — 2026-07-05

### 🐛 Corregido
- Al cambiar el **micrófono** o el **dispositivo de reproducción** en Ajustes, el
  cambio ahora se aplica **al instante**. Antes había que reiniciar la app para que
  la grabación y la reproducción usaran el dispositivo nuevo.
- Cuando la app **no puede verificar** si hay actualizaciones (sin internet o límite
  temporal de GitHub), ahora lo avisa, en vez de decir por error que ya tenés la
  última versión.

---

## [1.2.1] — 2026-07-05

### 🐛 Corregido
- Los dispositivos de audio se aplican al instante (incluido luego en la 1.2.2 junto
  con el aviso de verificación de actualizaciones).

---

## [1.2.0] — 2026-07-05

### ✨ Nuevo
- **Búsqueda rápida por teclado** en la lista de chats: escribí las primeras letras
  de un nombre y salta directo (como en el Explorador de Windows). Repetir la misma
  letra recorre los que empiezan igual.
- **Elegir micrófono y dispositivo de reproducción** — desde Ajustes o con **Ctrl+P**
  en cualquier pantalla. Se muestran solo los dispositivos activos.
- **Grabar audios en estéreo** (opcional, en Ajustes).
- Mientras grabás un audio: **Alt+P** pausa y reanuda, y **Alt+M** reproduce lo que
  llevás grabado para escucharte antes de enviarlo.
- Botón **"¿Qué hay de nuevo?"** en Ajustes (y se muestra solo después de actualizar).

### 🐛 Corregido
- Al volver de un grupo con Escape, ahora vuelve a la pestaña **Grupos** (antes iba
  siempre a Recientes).

---

## [1.1.0] — 2026-07-05

### ✨ Nuevo
- **Encuestas** — crear, votar y ver los resultados en vivo. Siguen funcionando aunque
  reinicies la app o vuelvas a entrar al chat.
- **Ajustes de privacidad** — última vez, en línea, foto de perfil, estados,
  confirmaciones de lectura y quién puede agregarte a grupos.
- **Compartir contacto** — desde el menú contextual de cualquier mensaje.
- **Mensajes temporales por defecto** para los chats nuevos.
- **Cambiar tu nombre visible** (el que ven los demás).
- **Administración de grupos avanzada** — "solo administradores pueden enviar",
  "solo administradores editan la info", **aprobación de nuevos miembros** (con lista de
  solicitudes para aprobar o rechazar), quién puede agregar participantes, y **vista previa**
  del grupo antes de unirte por enlace.
- **Menú por participante en grupos** — enviar mensaje privado, mencionar en el grupo,
  ver información del contacto y copiar número.
- **Enviar archivos pegándolos** en el cuadro de escribir (**Ctrl+V**), con confirmación.
- **Ctrl+G** para guardar el archivo seleccionado.
- **Modo "sin voz en segundo plano"** — cuando la app no está adelante, te guiás solo
  por los sonidos.

### 🔧 Mejorado
- La casilla **"Audio de una sola vez"** ahora aparece únicamente mientras grabás.
- El botón **"Encuesta"** se muestra solo en grupos.
- Navegación más limpia: se quitaron los textos instructivos repetitivos que se leían en
  cada mensaje ("pulsá Enter para abrir", etc.).
- **"Eliminar chat"** ahora se sincroniza también con tu teléfono.

### 🐛 Corregido
- **Administrador de grupos**: el botón no abría el panel, y al abrirlo el foco del teclado
  quedaba trabado (no respondían Tab, las flechas ni Escape). Ya funciona con normalidad.

### 🗑️ Quitado
- **Bloquear / desbloquear contactos**: WhatsApp rechaza esta operación con la librería
  actual, así que se quitó para no dejar una función que no funciona. La app **sigue
  mostrando** si un contacto está bloqueado (desde tu teléfono).

---

## [1.0.0] — Primera versión pública

- Mensajería de texto con estados (enviado, entregado, leído).
- Notas de voz: grabar, enviar y reproducir, con control de velocidad manteniendo el tono
  y reproducción encadenada.
- Historial completo con scroll infinito y almacenamiento local portable.
- Grupos, estados, reacciones, responder/citar, reenviar, editar y destacar.
- Fijar, silenciar, archivar, marcar como no leído, favoritos, buscar dentro del chat y
  exportar un chat a `.zip`.
- Notificaciones de Windows opcionales, inicio con Windows y bandeja del sistema.
- Separadores de día y de mensajes no leídos.
- Actualizaciones automáticas.

[3.0.0]: ../../releases/tag/v3.0.0
[2.0.14]: ../../releases/tag/v2.0.14
[2.0.13]: ../../releases/tag/v2.0.13
[2.0.12]: ../../releases/tag/v2.0.12
[2.0.11]: ../../releases/tag/v2.0.11
[2.0.10]: ../../releases/tag/v2.0.10
[2.0.9]: ../../releases/tag/v2.0.9
[2.0.8]: ../../releases/tag/v2.0.8
[2.0.7]: ../../releases/tag/v2.0.7
[2.0.6]: ../../releases/tag/v2.0.6
[2.0.5]: ../../releases/tag/v2.0.5
[2.0.4]: ../../releases/tag/v2.0.4
[2.0.1]: ../../releases/tag/v2.0.1
[2.0.0]: ../../releases/tag/v2.0.0
[1.2.11]: ../../releases/tag/v1.2.11
[1.2.10]: ../../releases/tag/v1.2.10
[1.2.9]: ../../releases/tag/v1.2.9
[1.2.8]: ../../releases/tag/v1.2.8
[1.2.7]: ../../releases/tag/v1.2.7
[1.2.6]: ../../releases/tag/v1.2.6
[1.2.5]: ../../releases/tag/v1.2.5
[1.2.4]: ../../releases/tag/v1.2.4
[1.2.3]: ../../releases/tag/v1.2.3
[1.2.2]: ../../releases/tag/v1.2.2
[1.2.1]: ../../releases/tag/v1.2.1
[1.2.0]: ../../releases/tag/v1.2.0
[1.1.0]: ../../releases/tag/v1.1.0
[1.0.0]: ../../releases/tag/v1.0.0

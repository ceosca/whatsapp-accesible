# Changelog

Todas las novedades importantes de **WhatsApp Accesible**, versión por versión.
El formato sigue el estilo [Keep a Changelog](https://keepachangelog.com/es/) y las
versiones usan [Versionado Semántico](https://semver.org/lang/es/).

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

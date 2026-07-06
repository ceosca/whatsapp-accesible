# Changelog

Todas las novedades importantes de **WhatsApp Accesible**, versión por versión.
El formato sigue el estilo [Keep a Changelog](https://keepachangelog.com/es/) y las
versiones usan [Versionado Semántico](https://semver.org/lang/es/).

---

## [1.2.1] — 2026-07-05

### 🐛 Corregido
- Al cambiar el **micrófono** o el **dispositivo de reproducción** en Ajustes, el
  cambio ahora se aplica **al instante**. Antes había que reiniciar la app para que
  la grabación y la reproducción usaran el dispositivo nuevo.

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

[1.2.1]: ../../releases/tag/v1.2.1
[1.2.0]: ../../releases/tag/v1.2.0
[1.1.0]: ../../releases/tag/v1.1.0
[1.0.0]: ../../releases/tag/v1.0.0

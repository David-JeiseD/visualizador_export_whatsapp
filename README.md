# 💬 Visualizador de exports de WhatsApp

Visor web que convierte un export de chat de WhatsApp (`.txt` o `.md`) en una conversación con aspecto de app: burbujas, colores por persona, respuestas citadas y búsqueda. Sin instalación, sin servidor y **sin subir nada**: todo se procesa en el navegador.

## ¿Por qué existe?

Leer un export en crudo es incómodo: cuesta seguir quién dijo qué y a quién. Este visor hace evidente el hilo de la conversación.

## Características

- **Dos formatos de entrada:** `.txt` (export nativo de WhatsApp) y `.md`. El formato se detecta por el contenido, no por la extensión.
- **Claridad de remitentes:** tu lado a la derecha en verde; cada otra persona con su propio color. Funciona con chats de grupo.
- **Respuestas citadas** con el nombre de quien dijo lo citado.
- **Adjuntos reconocidos:** imagen, sticker, video, audio y álbum se muestran como etiquetas; también mensajes reenviados y eliminados.
- **Búsqueda** con resaltado y navegación entre coincidencias (`Enter` / `Shift+Enter`).
- **Separadores de fecha fijos** al hacer scroll, tema claro/oscuro según el sistema y diseño adaptable a móvil.
- **Privacidad por diseño:** el archivo se lee localmente con la API `File`; no hay peticiones de red.

## Uso

1. Abre `index.html` en tu navegador (doble clic).
2. Arrastra tu archivo de chat o pulsa **Elegir archivo**.

Para obtener el export en WhatsApp: *Chat → ⋮ → Más → Exportar chat*.

## Detalles técnicos

- Un único archivo HTML con CSS y JavaScript vanilla, sin dependencias ni paso de build.
- El parser (`parse()`) es una función pura que normaliza ambos formatos a un mismo modelo de mensaje (fecha, hora, remitente, texto, cita, adjunto), separada de la capa de interfaz.
- Soporta mensajes multilínea, horas en formato 12/24 h y marcas invisibles que WhatsApp inserta en el texto.

## Limitaciones conocidas

- Carga un archivo a la vez.
- En el `.txt`, el orden de fecha se asume mes/día salvo que algún valor supere 12 (entonces se interpreta día/mes); un export día/mes con todos los días ≤ 12 podría mostrar fechas cambiadas.
- Renderiza el chat completo de una vez; con decenas de miles de mensajes podría ir lento. La virtualización de la lista sería la mejora natural.
- Las citas de respuesta solo están presentes en el formato `.md`; el `.txt` nativo no las incluye.

## Ideas a futuro

- Virtualización del scroll para chats muy grandes.
- Salto por fecha y estadísticas de actividad.
- Carga y unión de varios archivos.

## Licencia

MIT

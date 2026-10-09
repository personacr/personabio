# CLAUDE.md — personα · Link in Bio (bio.persona.cr)

Este archivo es la memoria del proyecto. Leelo completo antes de hacer cualquier cambio.

## Quién es el dueño

- **José Pablo García** — cineasta, fotógrafo y director escénico costarricense. Marca: **PERSONA** (se escribe `personα`).
- Está aprendiendo a usar GitHub y Claude Code. **Explicale todo en español sencillo (voseo costarricense), sin jerga técnica.**
- Antes de un cambio grande, resumí qué vas a hacer y pedí confirmación. Al terminar, decí en 2–3 líneas qué cambió y cómo verlo en vivo.

## Qué es este proyecto

- Página "Link in Bio" de una sola página: `index.html` + carpeta `img/`.
- Se publica en **https://bio.persona.cr** (Hostinger). Hostinger está conectado a este repo: cada cambio en la rama `main` se publica solo en 1–2 minutos.
- Todo el CSS y JS vive dentro de `index.html`. **No crear archivos externos ni agregar librerías.**

## Sistema de diseño (NO cambiar sin permiso explícito)

| Token CSS | Valor | Uso |
|---|---|---|
| `--black` | `#000000` | Fondo |
| `--bone` | `#F4F2ED` | Texto principal |
| `--fog` / `--mist` | `#7A7875` / `#A8A5A0` | Texto secundario |
| `--copper` | `#4FB3E8` | **Acento azul.** El nombre de la variable es heredado (antes era cobre). No renombrar. |
| `--copper-d` | `#2E8FC0` | Hover del acento |

- **Tipografía:** Fraunces (serif: wordmark, manifiesto, títulos de banners, footer) + Plus Jakarta Sans (todo lo demás).
- **Wordmark:** `person<span class="alpha">α</span>` — la α en itálica azul.
- **Banners de sección:** palabra en Fraunces peso 200, minúsculas, última letra en itálica azul: `stag<span class="last">e</span>`.
- **Íconos por disciplina:** Motion `▭` · Photo `◎` · Stage `⌒` · Music = SVG de diapasón.
- El favicon es un SVG en base64 con la α en `#4FB3E8`. Si cambia el color de acento, regeneralo.

## Arquitectura de secciones

1. **Hero:** perfil, wordmark, nombre, rol, bio corta, manifiesto.
2. **MOTION** (banner `motion-banner.jpg`): Reels Cinematográficos → Cortos & Videoclips → Dele Viaje → A Ojos Cerrados (solo info).
3. **PHOTO** (banner `photo-banner.jpg`): Espectáculos (6 fotos) → Personas (6) → Conceptual (4, grid de 2 columnas) → Photography Reels (al final).
4. **STAGE** (banner `stage-banner.jpg`): Lights Will Guide You (videos + 4 fotos + mini-íconos de sitio e Instagram) → Matilda Jr. (4 fotos).
5. **MUSIC** (banner `music-banner.jpg`): Soundtracks & Singles (embeds de Spotify).
6. **CONTACTO:** formulario Formspree + redes sociales.
7. **Footer:** wordmark + www.persona.cr.

## Cómo agregar un proyecto nuevo (patrón de tarjeta)

Copiá la estructura de una tarjeta existente (`#c-matilda` o `#c-lwgy`):

- `<div class="card" id="c-NOMBRE">` con `card-head` (botón que llama `toggle('c-NOMBRE')`), `card-icon` de la sección, título, subtítulo y flecha `›`.
- Dentro de `card-body > card-inner`: videos (`vid-list` / `vid-wrap ratio-16`), galería (`gallery g2` o `g3`) y opcionalmente `card-mini-icons`.
- **Cada foto de galería** lleva `onclick="openLightbox('NOMBRE', índice)"`.
- **Registrá la galería** en el objeto `lbGalleries` del JavaScript, con las rutas en el mismo orden.
- **Bilingüe siempre:** todo texto visible va duplicado con `<span data-es>…</span><span data-en>…</span>`. Si José Pablo no da la versión en inglés, traducila vos y avisale.
- Agregá `alt` descriptivo a cada imagen.

## Procesamiento de fotos

José Pablo sube las fotos originales a la carpeta **`nuevas/`**. Vos:

1. Procesalas con Python + Pillow (`pip install Pillow`):
   - **Galerías:** recorte cuadrado centrado, **800×800 px**, JPEG calidad 82, optimizado. En retratos verticales subí el recorte un poco (~8%) para favorecer rostros.
   - **Banners de sección:** proporción 16:4, **1400×350 px**, JPEG calidad 87. Ajustá la posición vertical para que el sujeto quede centrado.
   - **Imagen para compartir (og-image):** 1200×630 px.
2. Nombralas en minúsculas, sin espacios ni tildes: `stillstanding-01.jpg`, `stillstanding-02.jpg`…
3. Movelas a `img/` y **borrá los originales de `nuevas/`** (no subir archivos pesados al sitio).
4. Revisá visualmente al menos una foto procesada antes de terminar.

## Integraciones activas (no romper)

- **Google Analytics 4:** `G-TY6Y414RXR`. Eventos: `section_open` (al abrir una tarjeta), `outbound_click` (links externos), `contact_form_open`, `contact_form_submit`. Las tarjetas nuevas quedan registradas solas si usan `toggle()`.
- **Formspree:** `https://formspree.io/f/mojoqqqn`.
- **WhatsApp:** `https://wa.me/50688433789` · **Vimeo:** vimeo.com/personacr · **Email:** josepablo@persona.cr
- **Open Graph:** `og:image` apunta a `https://bio.persona.cr/img/og-image.jpg` (1200×630).

## Reglas de oro

- ❌ Nunca subir contraseñas, datos de clientes, cotizaciones ni galerías privadas a este repo (es público).
- ❌ No cambiar paleta, tipografías ni arquitectura sin permiso.
- ✅ Mantener el sitio rápido: fotos comprimidas, sin librerías.
- ✅ Antes de terminar: revisá que el HTML no tenga etiquetas sin cerrar, que el toggle ES/EN funcione y que cada galería nueva esté en `lbGalleries`.
- ✅ Mensajes de commit en español y claros: `Agrega proyecto Still Standing en Stage`.
- ✅ **Vista previa antes del Merge:** después de cada cambio, y antes de que José Pablo haga el Merge, siempre darle un link de vista previa con raw.githack.com usando el SHA del último commit, con este formato: `https://raw.githack.com/personacr/personabio/SHA/index.html` (reemplazar `SHA` por el código completo del último commit ya subido). Si después se hace otro commit, dar el link nuevo con el SHA nuevo.

## Pendientes conocidos

- Agregar el proyecto **Still Standing** en STAGE (preguntar a José Pablo: rol, año, posición en la lista, videos, links).
- Decisión pendiente sobre un nuevo isotipo para la α (exploraciones "Umbral" / "Testigo"). No aplicar hasta que José Pablo lo apruebe.

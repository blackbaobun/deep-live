# Firmas Email · Deep Estate Agency

4 firmas HTML (table-based, inline CSS) compatibles con Gmail, Outlook (desktop + web + iOS), Apple Mail (macOS + iOS) y Spark. Diseño 600×240 desktop, stack vertical en mobile vía `@media (max-width:480px)`.

## Archivos

| Archivo | Persona | Cargo | Teléfono |
|---|---|---|---|
| `david-founder.html` | David Soriano | Founder · CEO | +34 600 29 12 77 |
| `david-ceo.html` | David Soriano | CEO | +34 600 29 12 77 |
| `pedro-real-estate.html` | Pedro Soriano | Real Estate Agent | +34 664 21 29 69 |
| `pedro-coordinacion.html` | Pedro Soriano | Coordinación Internacional | +34 664 21 29 69 |

Email: `david@deepestateagency.com` / `pedro@deepestateagency.com` · Dirección: Plaza España, 1 · Alicante.

## Assets (`assets/`)

| Archivo | Tamaño display | Tamaño real (retina 2×) |
|---|---|---|
| `david.png` | 180×240 | 360×480 |
| `pedro.png` | 180×240 | 360×480 (recortado 140% + offset -20% según Figma) |
| `logo-icon.png` | 50×36 | 100×72 |
| `logo-text.png` | 122×34 | 244×68 |

Servidos en producción desde `https://deepestateagency.com/email-signature/assets/...` tras `bun run build && make deploy-live`. URLs absolutas en cada HTML.

## Instalación

### Gmail (web)

1. Abre el archivo `.html` en el navegador.
2. Click derecho dentro de la firma → "Seleccionar todo" o pinta con el ratón desde la esquina superior izquierda hasta abajo derecha.
3. Copia (⌘C / Ctrl+C).
4. Gmail → ⚙ → Ver todos los ajustes → General → Firma → Crear nueva → pega (⌘V / Ctrl+V).
5. Guardar cambios al final.

Nota: Gmail elimina el bloque `<style>` por lo que las media queries no aplican en Gmail. En mobile la firma se escala al ancho de pantalla (no apila). Estilos inline se preservan.

### Outlook Web (outlook.com / Microsoft 365)

1. Configuración → Correo → Redactar y responder → Firma de correo.
2. Crear nueva firma.
3. Pega la firma copiada del navegador (igual que Gmail).
4. Guardar.

Outlook Web preserva estilos inline. Outlook iOS aplica media queries → apila bien en mobile.

### Outlook Desktop (Windows / Mac)

Outlook Windows usa el motor de renderizado de Word, sin soporte de gradientes CSS ni media queries.

1. Archivo → Opciones → Correo → Firmas.
2. Nueva firma. Outlook abre el editor.
3. Cerrar Outlook.
4. Navega a `%APPDATA%\Microsoft\Signatures\` (Windows) o `~/Library/Group Containers/UBF8T346G9.Office/Outlook/Outlook 15 Profiles/Main Profile/Data/Signatures` (Mac).
5. Reemplaza el `.htm` generado con el contenido del archivo `.html` de la firma. Mantén el nombre de fichero `.htm` (no `.html`).
6. Reabre Outlook → la firma aparece. Verás fondo sólido `#341214` (sin gradiente) y layout fijo 600 wide; eso es correcto en Outlook desktop.

### Apple Mail (macOS)

1. Mail → Configuración → Firmas → "+" (crear nueva).
2. Escribe cualquier cosa de relleno y guarda.
3. Cierra Mail.
4. Navega a `~/Library/Mail/V10/MailData/Signatures/` (versión Vx depende del macOS).
5. Encuentra el `.mailsignature` recién creado (timestamp reciente). Ábrelo con un editor de texto.
6. Conserva las cabeceras MIME (las primeras líneas hasta la línea en blanco). Reemplaza el HTML siguiente con el contenido entre `<body>...</body>` de tu archivo `.html`.
7. En Finder: click derecho sobre el `.mailsignature` → Obtener información → marca "Bloqueado" (impide que Mail lo sobrescriba).
8. Reabre Mail. Selecciona la firma al redactar.

Apple Mail respeta `<style>` y media queries → mobile (iOS Mail) apila perfecto.

### Spark

1. Configuración → Firmas → Crear firma → HTML mode.
2. Pega el contenido completo del archivo `.html` (incluye `<style>` y media queries).
3. Guarda.

Spark renderiza media queries → apila en mobile.

### Zimbra (Webmail)

Zimbra sanitiza HTML pegado: elimina `<head>`, `<style>`, `<!doctype>`, condicionales Outlook, atributos no reconocidos. Las firmas están preparadas (solo inline CSS, tabla fixed 600px), pero **NO pegues el HTML como texto** — pega el contenido **renderizado** del navegador.

Workflow:

1. Abre el archivo `.html` en un navegador (Chrome/Safari/Firefox).
2. Pinta con el ratón desde la esquina superior izquierda de la firma hasta la inferior derecha. Selecciona la firma renderizada, NO el código fuente.
3. Copia (⌘C / Ctrl+C).
4. Zimbra → Preferencias → Firmas → Crear nueva → asegúrate de estar en modo HTML (no texto plano).
5. Pega (⌘V / Ctrl+V).
6. Guardar.

Notas Zimbra:

- Sin gradient: algunas versiones no aplican `background-image: linear-gradient(...)`. Fallback `bgcolor="#341214"` (color sólido) ya garantizado.
- VML Outlook (`<v:roundrect>`): Zimbra ignora los comentarios condicionales `<!--[if mso]>...<![endif]-->`. La foto se carga vía `<img>` con `border-radius:12px` (rendering rounded en Zimbra moderno).
- Si copias el `.html` como texto, Zimbra lo mete escapado. **Siempre copia desde el renderizado del navegador.**

## Comportamiento por cliente

| Cliente | Gradiente | Media query | Resultado mobile |
|---|---|---|---|
| Apple Mail macOS | ✅ | ✅ | apila |
| Apple Mail iOS | ✅ | ✅ | apila |
| Spark (todas las plataformas) | ✅ | ✅ | apila |
| Gmail web | ✅ | ❌ (strip `<style>`) | escala a viewport |
| Gmail iOS/Android app | ✅ | parcial | escala a viewport |
| Outlook 365 web | ✅ | ✅ | apila |
| Outlook iOS/Android | ✅ | ✅ | apila |
| Outlook desktop (Windows) | ❌ (solid `#341214`) | ❌ | layout 600 fijo |
| Outlook desktop (Mac) | ✅ | ❌ | layout 600 fijo |

Todos los clientes muestran texto seleccionable, links clicables (`tel:`, `mailto:`, web) y fotos.

## Modificaciones rápidas

Cambiar teléfono / email: edita el archivo y reemplaza en los dos sitios (texto visible + atributo `href`). Mismo patrón para nombre, cargo, tagline.

Cambiar fondo: localiza `background-color:#341214` y `linear-gradient(to right,#1f0709 0%,#341214 50%,#512022 100%)`.

Cambiar fuente: la elegante (nombre) usa `'Cormorant Garamond',Georgia,serif`; resto usa `-apple-system,BlinkMacSystemFont,'Segoe UI',Roboto,Arial,sans-serif`. Cormorant Garamond no carga en Gmail/Outlook → fallback a Georgia (similar elegancia, fiable).

## Re-export desde Figma

Diseño origen: `https://www.figma.com/design/bcbSigMiNAKndYSYif5T9m/Deep-pruebas?node-id=115-694`. Si rediseñas:

1. Exporta `david-soriano` y `pedro-soriano` como PNG @2x (360×480).
2. Exporta `logo-icon` y `logo-text` como SVG, luego convierte a PNG @2x (100×72 y 244×68). En macOS:
   ```bash
   /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome \
     --headless=new --disable-gpu --default-background-color=00000000 \
     --window-size=100,72 --screenshot=logo-icon.png file://$PWD/logo-icon.svg
   ```
3. Reemplaza en `assets/`. URLs en HTML no cambian.

Foto de Pedro lleva crop `size:140%` `left:-20%` aplicado en exportación (ver `pedro.png` reglas en repo). Si exportas raw photo, replícalo con Chrome headless + HTML wrapper de overflow:hidden (ver historial git).

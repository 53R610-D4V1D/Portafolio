# Cómo actualizar

[← Volver al índice](README.md)

Recetas para los cambios habituales y los comandos que los verifican.

---

## Ver el sitio sin tocar XAMPP

```bash
cd /c/xampp/htdocs/Portafolio
python -m http.server 8899 --bind 127.0.0.1
# abrir http://127.0.0.1:8899/index.html
```

Para cerrarlo después:

```bash
python -c "
import subprocess, re
out = subprocess.run(['netstat','-ano','-p','TCP'], capture_output=True, text=True).stdout
for m in re.finditer(r'127\.0\.0\.1:8899\s+\S+\s+LISTENING\s+(\d+)', out):
    subprocess.run(['taskkill','/F','/PID', m.group(1)])
"
```

---

## Agregar capturas a un proyecto

1. Copiá las imágenes a `asset/<proyecto>/`.
2. Optimizalas y renombralas con el script de abajo. **Sin espacios en los nombres.**
3. Agregá un `<img>` por captura dentro de `<div id="carousel-<proyecto>">`:

   | Orientación | Clases |
   | --- | --- |
   | Horizontal | `h-full w-full object-cover flex-shrink-0` |
   | **Vertical** (captura de celular) | `h-full w-full object-contain flex-shrink-0 bg-slate-950` |

   Con `object-cover`, una captura vertical de 540×1200 se recorta casi por completo:
   solo se ve una franja del medio.

4. Agregá un `<span class="carousel-dot ...">` más, con el índice siguiente.
5. Poné `loading="lazy"` en todas menos la primera.

### Script de optimización

```python
from PIL import Image
import os, glob

d = 'asset/<proyecto>'
for p in sorted(glob.glob(d + '/*.png')):
    im = Image.open(p).convert('RGB')
    target = 1280 if im.width > im.height else 540   # 540 para capturas de celular
    if im.width > target:
        im = im.resize((target, int(im.height * target / im.width)), Image.LANCZOS)
    im.save(os.path.splitext(p)[0] + '.jpg', 'JPEG', quality=84, optimize=True, progressive=True)
    os.remove(p)
```

Referencia de lo ya logrado: Reporte Municipal 2663 → 638 KB (77 % menos),
Activisport 1775 → 382 KB (79 %), Invector 1629 → 155 KB (91 %).

Si renombrás archivos, actualizá las referencias:

```bash
rg -n "asset/<proyecto>/" index.html
```

---

## Agregar un proyecto entero

1. Cloná la estructura de una tarjeta existente:
   `<div class="project-card" data-category="...">`.
2. El contenedor de imagen lleva
   `class="carousel-media relative aspect-video w-full bg-slate-900/40 overflow-hidden cursor-pointer"`
   con `onclick="openModalGallery(this)"`.
3. Adentro, el carrusel:
   `<div id="carousel-<proyecto>" class="carousel-container absolute inset-0 flex transition-transform duration-300">`.
4. Registralo: `initCarousel('carousel-<proyecto>')` junto a los otros.
5. Agregá la **línea de datos duros** debajo de las etiquetas, con el mismo formato que
   las demás. Es lo que permite compararlas de un vistazo:

   ```html
   <p class="mt-3 text-xs text-slate-200/70">
     Dato &middot; Dato &middot; Dato
   </p>
   ```

   Las actuales:

   | Proyecto | Línea |
   | --- | --- |
   | Invector | Julio 2025 – agosto 2026 · Permisos granulares · Workflow de aprobación con historial |
   | Reporte Municipal | 88 endpoints REST · 438 pruebas automatizadas · 23 migraciones Flyway |
   | Activisport | Abril 2026 – presente · En producción con cliente de pago · 7.561 pruebas automatizadas |

6. Si usa una tecnología sin filtro, agregá el filtro (`<input>` + `<label>`) y asignale el
   `data-category`. **Si un filtro se queda sin proyectos, eliminalo** — junto con su CSS.
7. Agregá el nodo al JSON-LD del `<head>`.

---

## Agregar contenido al JSON-LD

El bloque vive al final del `<head>`. Hoy tiene 4 nodos en su `@graph`:
`ProfilePage`, `Person`, `WebApplication` (Activisport) y `SoftwareApplication`
(Reporte Municipal).

> **El JSON-LD debe espejar contenido visible.** Declarar una credencial, un proyecto o
> una habilidad que no aparece en la página se penaliza como datos inconsistentes.
> Si lo agregás al JSON-LD, tiene que verse en la página. Y al revés.

Un proyecto sin sitio en vivo **no lleva `url`**.

---

## Actualizar un dato

```bash
rg -n "<el dato>" index.html cv.html
```

Y acordate del documento de Claude, que no sale en esa búsqueda.
Ver la regla de oro en [README.md](README.md).

---

## Verificaciones

### JSON-LD válido

Si tiene un error de sintaxis, Google descarta el bloque entero y en silencio.

```bash
python -c "
import re, json, io
h = io.open('index.html', encoding='utf-8').read()
d = json.loads(re.findall(r'<script type=\"application/ld\+json\">(.*?)</script>', h, re.S)[0])
print('VALIDO |', len(d['@graph']), 'nodos:', [n['@type'] for n in d['@graph']])
"
```

### HTML balanceado e imágenes existentes

```bash
python -c "
import io, re, os
from html.parser import HTMLParser
VOID = {'area','base','br','col','embed','hr','img','input','link','meta','param','source','track','wbr'}
class B(HTMLParser):
    def __init__(s):
        super().__init__(convert_charrefs=True); s.st=[]; s.er=[]
    def handle_starttag(s,t,a):
        if t not in VOID: s.st.append(t)
    def handle_endtag(s,t):
        if t in VOID: return
        if s.st and s.st[-1]==t: s.st.pop()
        else: s.er.append(t)
h = io.open('index.html', encoding='utf-8').read()
b = B(); b.feed(h)
print('errores:', b.er or 'ninguno', '| sin cerrar:', b.st or 'ninguno')
faltan = [s for s in re.findall(r'src=\"(asset/[^\"]+)\"', h) if not os.path.exists(s)]
print('imagenes faltantes:', faltan or 'ninguna')
"
```

### Medir el layout de verdad

Las capturas de pantalla de este sitio salen en blanco por AOS y el timing de pintado.
**Medir el DOM es más confiable.** Con el servidor local levantado y las herramientas de
navegador, o desde la consola del navegador:

```javascript
document.querySelectorAll('[data-aos]').forEach(e => { e.style.opacity = 1; e.style.transform = 'none'; });
[...document.querySelectorAll('.project-card')].map(c => {
  const m = c.querySelector('.carousel-media').getBoundingClientRect();
  return { nombre: c.querySelector('h3').textContent.trim(),
           alto: Math.round(c.getBoundingClientRect().height),
           media: `${Math.round(m.width)}x${Math.round(m.height)}`,
           ratio: +(m.width / m.height).toFixed(2) };
});
```

Las tres tarjetas deben dar **el mismo alto** y **ratio 1.78**.

### El test del ATS

Este es **el que reprobaba el CV hecho en Canva**: no exponía ni la empresa ni el cargo.

```bash
pdftotext -layout cv.pdf - | sed -n '/EXPERIENCIA/,/EDUCACI/p'
```

Si ahí no aparecen el nombre de la empresa y el cargo, un ATS tampoco los ve.

---

## Exportar el CV a PDF

Abrí `cv.html` → `Ctrl+P` → Destino "Guardar como PDF" → márgenes predeterminados →
desactivá "Encabezados y pies de página".

El propio archivo muestra esas instrucciones en un aviso que no se imprime.

Está configurado en tamaño **Letter**. Para A4, cambiá `@page { size: Letter }`.
Sale en dos páginas, que es lo correcto para este volumen de experiencia.

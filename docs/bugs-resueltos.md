# Bugs resueltos

[← Volver al índice](README.md)

Errores ya corregidos. Están acá para que no se reintroduzcan.

---

## El patrón que causó dos de ellos

> **`height: 100%` o `max-height: 100%` contra un padre sin altura definida no resuelve en CSS.**
> El navegador lo trata como si no existiera y el elemento cae a altura automática.

Es de los errores más silenciosos que hay, porque **funciona por accidente** mientras el
contenido tenga el tamaño "correcto". Los dos carruseles de este portafolio vivieron años
rotos sin que se notara, hasta que entró una imagen vertical.

**La regla:** si necesitás limitar el tamaño de algo y no controlás la altura del padre,
anclalo a unidades de viewport (`vh` / `vw`), no a porcentajes. Por construcción no puede fallar.

---

## 1. `aspect-video` no generaba nada

### Síntoma

La tarjeta de Reporte Municipal se estiraba a ~500 px de alto mientras las otras medían
~110 px, rompiendo la grilla de proyectos.

### Causa

El `<script>` de Tailwind cargaba `?plugins=aspect-ratio`. Ese plugin **legacy desactiva
las utilidades `aspect-*` del core**.

Medido con `getComputedStyle` sobre un elemento de prueba recién creado:

```
aspect-ratio: auto     ← debería ser 16/9
height: 0px            ← el contenedor no tenía altura propia
```

Como el contenedor medía 0, su altura real la dictaba el hijo en flujo. Con imágenes
horizontales el desfase era invisible; con las verticales de 540×1200 se disparaba.

### Arreglo

1. Se quitó `?plugins=aspect-ratio` del CDN. El sitio usa `aspect-video` y `aspect-[16/9]`,
   ambas del core, y **cero** clases `aspect-w-*` / `aspect-h-*` del plugin.
2. Respaldo en CSS propio, para no depender del CDN:
   ```css
   .carousel-media { aspect-ratio: 16 / 9; }
   ```
3. Los carruseles pasaron de `flex h-full` a `absolute inset-0 flex`, para que la altura sea
   definida y el `h-full` de las imágenes resuelva.

### ⚠ No volver a agregar `?plugins=aspect-ratio` al script de Tailwind.

---

## 2. El modal recortaba las capturas verticales

### Síntoma

Al abrir una captura de celular en el modal de galería, se veía solo una franja del medio.

### Causa

```css
.modal-image-container img { max-height: 100%; }
```

El contenedor tiene `height: auto` con solo `max-height: 80vh`, así que el porcentaje del
hijo no resuelve. La imagen se dibujaba a su alto natural de 1200 px y el `overflow: hidden`
la recortaba.

### Arreglo

```css
.modal-image-container img {
  display: block;
  max-width: calc(90vw - 8px);
  max-height: calc(80vh - 8px);
  width: auto; height: auto; object-fit: contain;
}
```

Los `- 8px` descuentan el borde del contenedor: con `box-sizing: border-box` el borde entra
en el `max-height` y la imagen lo desbordaría.

En móvil el modal pasó de 60vh a **70vh**, porque en pantalla angosta una captura de celular
a 60vh quedaba innecesariamente chica.

### Verificación

Las 7 diapositivas de Reporte Municipal, con proporción natural idéntica a la renderizada:
verticales 540×1200 → 284×631 (ratio 0.45 exacto), horizontales sin escalar. Cero recortes.

---

## 3. `fab fa-nextjs` no existe

En Font Awesome 6.4 free **no hay icono de marca para Next.js**. El icono del filtro
Next.js nunca renderizó. Se reemplazó por `fab fa-react`, que es lo que la sección de
habilidades ya usaba para "React / Next.js".

---

## 4. El CV exportado de Canva era invisible para un ATS

Al extraer el texto del PDF con `pdftotext -layout`, la sección de experiencia salía así:

```
EXPERIENCIA LABORAL
                                      Febrero 2021- diciembre 2024
Optimización SQL: Reduje tiempos de reportes de 20 a 5 min...
```

**Sin nombre de empresa y sin cargo.** Se perdían porque en Canva viven dentro de cajas de
texto que el extractor no lee en orden. Un ATS llena campos: empresa, cargo, fechas. Los dos
primeros le salían vacíos.

### Arreglo

Se creó `cv.html`: una sola columna, texto real en HTML semántico, sin cajas flotantes ni
tablas de maquetación. Verificado con el mismo método: empresa y cargo aparecen en orden.

**El test está en [como-actualizar.md](como-actualizar.md).** Corrélo sobre cualquier CV
antes de mandarlo.

---

## 5. Datos estructurados inconsistentes

El JSON-LD debe espejar contenido **visible**. Declarar una credencial que no aparece en la
página hace que Google lo marque como datos inconsistentes y descarte el bloque.

Por eso, cuando se agregó el bootcamp de IA al `hasCredential`, hubo que agregar también su
tarjeta a la sección Educación. No era opcional.

---

## Verificar que siguen arreglados

Ver la sección de verificaciones en [como-actualizar.md](como-actualizar.md).
Las tres tarjetas de proyecto deben dar el **mismo alto** y **ratio 1.78**.

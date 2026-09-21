# Estructura del proyecto

[← Volver al índice](README.md)

---

## Archivos del portafolio

| Archivo | Para qué sirve |
| --- | --- |
| `index.html` | El portafolio completo. Un solo archivo: estilos, contenido, JSON-LD y JavaScript. |
| `cv.html` | La hoja de vida imprimible. Se abre y se exporta a PDF con `Ctrl+P`. |
| `asset/favicon.svg` | Favicon propio, monograma SD. |
| `asset/activisport/` | 7 capturas de Activisport. |
| `asset/reportemunicipal/` | 15 capturas de Reporte Municipal. |
| `asset/invector/` | 3 capturas de Invector. |
| `asset/titulos/` | Certificados en PDF. |
| `docs/` | Esta documentación. |

---

## Anatomía de `index.html`

Es un archivo único. Las zonas que vas a tocar, en orden de aparición:

| Zona | Qué contiene |
| --- | --- |
| `<head>` — meta | `description`, Open Graph, Twitter Card, canonical, robots, favicon |
| `<head>` — JSON-LD | `<script type="application/ld+json">` con 4 nodos: `ProfilePage`, `Person`, `WebApplication` (Activisport) y `SoftwareApplication` (Reporte Municipal) |
| `<head>` — `<style>` | CSS propio: `.typing`, `.carousel-media`, `.modal-gallery`, `.surface` |
| `#inicio` | Hero: nombre, titular con efecto de tipeo, botones |
| `#sobre-mi` | Perfil y el bloque "Lo que me define" |
| `#experiencia` | Activisport y Serviunix |
| `#proyectos` | Filtros + 3 tarjetas con carrusel |
| `#habilidades` | Grilla de habilidades e idiomas |
| `#educacion` | Títulos y formación complementaria |
| `#contacto` | Datos de contacto |
| `<script>` final | Carruseles, filtros, modal de galería |

### Cómo funcionan los filtros de proyectos

No son CSS puro. El mecanismo real es:

1. Cada filtro es un `<input type="radio" id="filter-X">`.
2. Un listener de `change` extrae la `X` del `id` y llama a `filterProjects('X')`.
3. Esa función muestra u oculta cada `.project-card` comparando contra su `data-category`.

Las clases `peer-checked/X:` **solo estilan la etiqueta activa**, no filtran nada.

Filtros actuales: `all`, `laravel`, `spring`, `nextjs`.

### Cómo funcionan los carruseles

- El contenedor de imagen lleva `class="carousel-media relative aspect-video w-full ..."`.
- Adentro, `<div id="carousel-<proyecto>" class="carousel-container absolute inset-0 flex ...">`.
- `moveCarousel()` aplica `transform: translateX(-N * 100%)`.
- Cada carrusel nuevo debe registrarse con `initCarousel('carousel-<proyecto>')`.

Carruseles actuales: `carousel-invector`, `carousel-reportemunicipal`, `carousel-activisport`.

---

## La hoja de vida editable

Existe una tercera versión, editable y comentable, en Claude Docs:

```
https://claude.ai/code/artifact/bd19a2f0-adec-46cb-81be-edcf223a1b7a
```

No aparece en ninguna búsqueda local. Cuando actualices un dato, acordate de este.

---

## Dónde viven los proyectos

Los tres repositorios están fuera de este portafolio. En esta máquina:

| Proyecto | Ubicación | Repositorio |
| --- | --- | --- |
| Activisport | `~/Documents/Proyectos/activisport` | privado |
| Reporte Municipal | `~/Documents/Proyectos/reportemunicipal` | privado (404) |
| Invector | `htdocs/invector` | privado (404) |

Que los tres sean privados es el motivo por el que las tarjetas de Reporte Municipal e
Invector **no llevan enlaces externos**: las capturas las sostienen solas.

---

## Assets: peso actual

| Carpeta | Peso |
| --- | --- |
| `asset/activisport/` | 382 KB |
| `asset/reportemunicipal/` | 638 KB |
| `asset/invector/` | 155 KB |

Todas las capturas están en JPEG progresivo, a 1280 px de ancho las horizontales y
540 px las verticales. Ver [como-actualizar.md](como-actualizar.md) para el script.

> **Nunca dejes espacios en los nombres de archivo.** Rompen en servidores estrictos
> y se ven mal en la URL. Ya pasó una vez con las capturas de Activisport y con el PDF
> de la carta de recomendación, que todavía lo tiene.

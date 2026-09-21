# Pendientes

[← Volver al índice](README.md)

---

## Decisiones que requieren tu criterio

### El nombre de Invector

Las capturas muestran la marca **KRINCHAKAU** en el logo del landing, en el logo del panel
y en el correo `admin@krinchakau.com`. La tarjeta del portafolio dice **Invector**, que es
el nombre del repositorio y de la documentación interna.

Un reclutador va a ver la discordancia en dos segundos. Hay que unificar: o el producto se
llama Invector y las capturas están viejas, o se llama KRINCHAKAU y el portafolio debería
decir eso.

### Captura con datos de prueba

`asset/invector/gestion-inventos.jpg` muestra:

- Un invento titulado **"asd"** con descripción **"asdas"**
- La URL `127.0.0.1:8000` en la barra de estado
- El dashboard con "Total Inventos: 1, Usuarios Registrados: 2" y porcentajes de variación
  que parecen quemados en el código

Cargá tres o cuatro inventos con títulos y descripciones creíbles y volvé a capturar.
Una captura con "asd" tira abajo el trabajo de las otras dos.

### Enero de 2027 — releer la línea del cliente

Hoy el CV dice *"un club en suscripción mensual desde julio de 2026"*.

A partir de enero de 2027 serán **seis meses de pagos continuos**. Ahí deja de ser "tiene un
cliente" y pasa a ser **evidencia de retención**, que se redacta distinto y pesa mucho más.

Poné un recordatorio. La fecha ya está publicada; solo hay que cambiar cómo se enmarca.

---

## Verificación visual pendiente

Nunca se pudo confirmar con los ojos, porque las capturas de pantalla automáticas de este
sitio salen en blanco (por AOS y el timing de pintado). Todo se verificó **midiendo el DOM**,
que es más confiable, pero conviene mirarlo igual:

1. Que el tipeo del hero corra parejo y no se corte en móvil.
2. Que los tres carruseles pasen bien, incluidas las capturas verticales de Reporte Municipal.
3. Que `cv.html` salga limpio con `Ctrl+P`, en dos páginas.

---

## Deuda técnica del portafolio

Ordenada por impacto real.

| Problema | Detalle |
| --- | --- |
| `asset/perfil_1.png` pesa **1.5 MB** | Está arriba de todo. Es el peor golpe al LCP en móvil. Convertir a WebP o JPEG y bajar a ~150 KB. |
| `cdn.tailwindcss.com` | Imprime en consola un aviso de que no es para producción. Lo ve cualquier técnico que abra DevTools. |
| CSS inválido | `.modal-gallery .carousel-btn { z-10; }` debería ser `z-index: 10;`. |
| Código huérfano de video | `onVideoLoad`, `.video-loading` y el `IntersectionObserver` de `data-src` quedaron sin uso al quitar el último `<iframe>`. Inofensivo, pero sobra. |
| Nombre de archivo con espacios | `asset/carta_recomedacion/13-01-2025CARTA DAVID .pdf` — con espacios **y un espacio antes del `.pdf`**. Rompe en servidores estrictos. |
| `README.md` vacío | 0 bytes. Tu CV enlaza a ese GitHub; es lo primero que ve quien entre. |

---

## Del lado de los proyectos

### Reporte Municipal

- **7 hallazgos HIGH de seguridad abiertos** al cierre: `citizenUserId` confiado desde el
  cliente, uploads sin validación de MIME, rate limiter vulnerable a spoofing de
  `X-Forwarded-For`.
- El panel admin tiene **un solo archivo de tests** (7 casos).
- Sin cobertura instrumentada: no hay plugin JaCoCo.
- Sin actividad desde el 11 de abril de 2026.
- El `README.md` del proyecto dice Expo 51 cuando es Expo 54, y `CLAUDE.md` dice
  "no source code exists yet", completamente obsoleto.

### Invector

- Módulos P0 pendientes según su propio roadmap: verificación de inversores y de identidad,
  y contratos.
- Detenido desde el 5 de agosto de 2026.

---

## Y lo más importante, que no es técnico

Tres veces en una sola sesión el repositorio tenía algo **mejor** de lo que decía el
portafolio: las 7.561 pruebas, los 26 módulos, la entrada por voz del agente.

No es descuido. Es un sesgo consistente a la baja sobre el propio trabajo, y es más caro que
inflar, porque el que infla al menos llega a la entrevista.

**Cuando termines algo, anotá el número el mismo día.** Una línea en un archivo de texto
alcanza. En dos meses no te vas a acordar de que el agente acepta voz.

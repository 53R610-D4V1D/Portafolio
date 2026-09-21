# Documentación del portafolio

Guía operativa para actualizar el portafolio y la hoja de vida sin romper nada
ni perder datos ya verificados.

**Última actualización: 21 de septiembre de 2026.**

---

## Índice

| Documento | Para qué |
| --- | --- |
| [estructura.md](estructura.md) | Qué es cada archivo y dónde vive cada cosa |
| [cronologia.md](cronologia.md) | Las fechas congeladas, con su evidencia |
| [datos-verificados.md](datos-verificados.md) | Los números publicados y cómo reverificarlos |
| [como-actualizar.md](como-actualizar.md) | Recetas y comandos para los cambios habituales |
| [bugs-resueltos.md](bugs-resueltos.md) | Errores ya arreglados que no hay que reintroducir |
| [pendientes.md](pendientes.md) | Deuda técnica y decisiones abiertas |
| [reglas-de-redaccion.md](reglas-de-redaccion.md) | Cómo se escribe el contenido y por qué |

---

## La regla de oro

Todo dato que cambie hay que tocarlo en **los tres lados**:

1. `index.html` — el portafolio
2. `cv.html` — la hoja de vida imprimible
3. El documento editable en Claude Docs

Si los tres no dicen lo mismo, un reclutador que abra dos de ellos va a dudar del
tercero. La coherencia entre documentos vale más que cualquier frase bien escrita.

Antes de dar por hecho un cambio:

```bash
rg -n "<el dato que cambiaste>" index.html cv.html
```

Y acordate del documento de Claude, que no aparece en esa búsqueda.

---

## Antes de publicar cualquier número

Los datos de este portafolio están verificados uno por uno contra los repositorios.
Si vas a agregar una cifra nueva, verificala primero y anotá **con qué comando** la
sacaste, en [datos-verificados.md](datos-verificados.md).

Un número que no podés reproducir es un número que no deberías publicar.

---

## Mantené esto vivo

Cada vez que cambies algo, actualizá la fecha del encabezado de este archivo.

Un documento de mantenimiento desactualizado es peor que no tener ninguno, porque
te hace confiar en datos viejos.

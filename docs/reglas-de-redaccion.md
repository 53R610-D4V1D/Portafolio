# Reglas de redacción

[← Volver al índice](README.md)

Cómo se escribe el contenido del portafolio y la hoja de vida, y por qué.
Cada una de estas reglas costó encontrarla. No las rompas sin una razón mejor.

---

## 1. El cargo debe contener el keyword del puesto que buscás

**No** la palabra que mejor te describe. La palabra por la que te van a buscar.

Los ATS y los buscadores de reclutadores filtran por keyword en el cargo.
"Responsable Técnico", "Líder de Sistemas" o "Encargado de TI" describen lo mismo y
**pierden el filtro** contra "Desarrollador".

Por eso el rol en Activisport es **Fundador y Desarrollador Principal**, y no
"Fundador y Responsable Técnico". "Principal" aporta seniority sin mentir: es el único
desarrollador.

---

## 2. Nunca escribir "clientes" en plural

Activisport tiene **un** club pagando. Uno.

En la entrevista van a preguntar cuántos clientes tenés. Si el CV insinuaba varios y la
respuesta es "uno", **toda la hoja de vida pasa a ser sospechosa**: los 20 a 5 minutos,
el multi-tenant, las 7.561 pruebas. Todo.

Un dato honesto y chico sostiene la credibilidad de los grandes. Uno inflado se los lleva
puestos.

La respuesta correcta, sin vergüenza: *"Uno pagando, y lo estoy operando solo mientras
construyo el siguiente."* Eso suena a fundador.

---

## 3. "IA en producción", no "IA aplicada"

En 2026, **usar IA para programar no es un diferenciador**. Lo hace todo el mundo. Ponerlo
al frente no destaca, iguala.

Peor: hay managers que filtran **en contra** de perfiles que suenan dependientes de la IA.
"IA aplicada" sin contexto se lee como *"no resuelve sin que le escriban el código"*.

**El diferenciador real es haber metido IA adentro de un producto que factura**: un asistente
con function calling que modifica la base de datos en producción. Eso casi nadie lo tiene.

De ahí el titular **Backend Developer · IA en producción**: dice que la despachaste, no que
la consumís. Y mantiene la lectura correcta — sos un backend sólido **que además** entrega IA.

---

## 4. Experiencia y Proyectos no son lo mismo

| Va en **Experiencia** | Va en **Proyectos** |
| --- | --- |
| Activisport: hay alguien pagando | Reporte Municipal: sin desplegar, sin cliente |
| Serviunix: empleo formal | Invector: sin pago, detenido |

Ese contraste **es lo que hace creíble a Activisport**. Si metés los tres como experiencia,
el entrevistador que pregunta descubre que dos no tienen cliente y empieza a dudar del
tercero.

Un proyecto con fechas de inicio y fin cerradas es completamente normal en una hoja de vida.
Lo que se ve mal es un proyecto sin fechas, o uno que se presenta como vivo y no lo está.

---

## 5. No inferir el nivel de idioma a partir del stack

El inglés es **básico** y **no incluye lectura de documentación técnica**.

Que el stack sea Next.js, Prisma y Railway —documentación solo en inglés— no implica lo
contrario: la IA hace de intermediario del idioma.

En el CV se escribe **"básico"**, no "muy básico": es el término estándar y honesto.
"Muy básico" suena a autocastigo sin aportar precisión.

Y no se le agrega "lectura técnica de documentación", que es una habilidad distinta.

---

## 6. Las capturas van con datos de demostración

La captura del agente de IA usa "Club demo", no el club que paga. Mantené eso en cualquier
captura futura.

Y con datos **creíbles**: una pantalla con "asd" y "asdas" tira abajo el trabajo de las
demás. Ver [pendientes.md](pendientes.md).

---

## 7. Formato de las tarjetas de proyecto

Las tres llevan la misma estructura para que el ojo las compare solo:

1. Carrusel de capturas
2. Título
3. Descripción de dos a cuatro líneas
4. Etiquetas de tecnología
5. **Una línea de datos duros**, con el mismo formato

La línea de datos duros es lo que las hace comparables de un vistazo. Y Activisport gana
sin discusión, que es exactamente lo que tiene que pasar.

---

## 8. Lo que nunca se escribe sobre Reporte Municipal

Está prohibido: **"en producción"**, **"desplegado"**, **"en uso"**, **"clientes"**.

No está desplegado y ninguna alcaldía lo usa. Su propio `DEPLOY_CHECKLIST.md` dice `NO-GO`.
Ver [datos-verificados.md](datos-verificados.md).

---

## 9. Los números van con su fuente

Todo dato publicado tiene que ser reproducible con un comando, anotado en
[datos-verificados.md](datos-verificados.md).

Y para tests: **nunca contar con grep** si el proyecto usa tests parametrizados.
El número que vale es el que reporta el runner, porque es el que cualquiera verifica
corriendo `npm test`.

---

## 10. Coherencia antes que elocuencia

Tres documentos cuentan la misma historia: el portafolio, `cv.html` y el documento de Claude.

Si dos no coinciden, gana la duda. Una frase mediocre repetida igual en los tres lados vale
más que una frase brillante que contradice a las otras dos.

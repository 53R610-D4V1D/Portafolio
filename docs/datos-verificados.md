# Datos verificados

[← Volver al índice](README.md)

Todos los números publicados en el portafolio y la hoja de vida salieron de los comandos
de esta página. Si actualizás una cifra, volvé a correr el comando y anotá el resultado acá.

**Un número que no podés reproducir es un número que no deberías publicar.**

---

## Activisport

| Dato | Valor | Cómo verificar |
| --- | --- | --- |
| Pruebas automatizadas | **7.561** | `npm test` (script `vitest run`) — ver aviso abajo |
| Archivos de test | 776 | `git ls-files \| rg "\.(test\|spec)\.(ts\|tsx)$" \| wc -l` |
| Modelos Prisma | 77 | `rg -c "^model " prisma/schema.prisma` |
| Migraciones | 102 | `ls prisma/migrations \| wc -l` |
| Módulos funcionales | 26 | `git ls-files \| rg -o "src/app/.*/([a-z-]+)/page\.tsx" -r '$1' \| sort -u` |
| Rutas API | 16 | `git ls-files \| rg "app/api/.*route\.ts$" \| wc -l` |
| Commits | 1663 | `git rev-list --count HEAD` |

### ⚠ Aviso sobre el conteo de pruebas

El proyecto tiene **52 bloques `it.each`**. `grep` cuenta esa línea **una sola vez**, pero
al ejecutar expande a todos sus casos parametrizados.

| Método | Resultado |
| --- | --- |
| `rg -c "^\s*(it\|test)\("` | 7.061 |
| Ampliado con `.each .only .skip` | 7.174 |
| **`vitest run` (real)** | **7.561** |

**Publicar siempre el número del runner.** Es el que cualquiera verifica corriendo
`npm test`. Si el portafolio dice menos, quedás corto sin razón.

Esta regla aplica a cualquier proyecto con tests parametrizados (`it.each`, `test.each`,
`describe.each`).

### Arquitectura

Hexagonal, confirmada en disco por la estructura de carpetas:

```
src/domain/  src/application/  src/infrastructure/  src/interface/
```

### Módulos del panel

41 páginas `page.tsx`, de las cuales **26 son módulos funcionales**:

> academias · agente-ia · alumnos · asistencia · audit · calendario · cargos-excedente ·
> clases · comprobantes-whatsapp · configuracion · contabilidad · cotizador · crm · crons ·
> dashboard · docentes · pagos · perfil · planes · reportes · roles · seguridad · soporte ·
> suscripciones · torneos · usuarios

El resto son páginas de autenticación, legales y placeholders `-no-disponible`.

### El asistente de IA

Acepta **entrada por texto y por voz**. Confirmado por la existencia de
`docs/agente-ia/entrada-audio-plan-produccion.md` y los OpenSpec
`agente-ia-audio-infraestructura` y `agente-ia-guardar-audios`.

Ejecuta herramientas que **leen y modifican la base de datos** (function calling en
producción). La captura `asset/activisport/agente-ia.jpg` lo muestra consolidando deuda
vencida de toda la academia.

### Estado comercial

**Un club** en suscripción mensual desde el **22 de julio de 2026**. Nunca escribir
"clientes" en plural — ver [reglas-de-redaccion.md](reglas-de-redaccion.md).

Equipo de tres: Sergio cubre el 100% del desarrollo como único perfil técnico; los otros
dos llevan operaciones y el frente comercial.

---

## Reporte Municipal

| Dato | Valor |
| --- | --- |
| Endpoints REST | 88 |
| Controladores | 19 |
| Dominios (monolito modular) | 9 |
| Pruebas automatizadas | **438** (276 backend + 162 móvil) |
| Casos E2E ejecutados | 68 |
| Migraciones Flyway | 23 |
| Tablas | 21 |
| Commits | 73 |

### ⚠ No está desplegado y ninguna alcaldía lo usa

El `DEPLOY_CHECKLIST.md` del proyecto dice literalmente `Status: NOT READY` y
`Deploy decision: NO-GO`. No hay CI/CD, ni Dockerfile, ni configuración de hosting.
El `eas.json` tiene `"production": {}` vacío.

El documento de Dabeiba es una **presentación comercial de venta** con precios, no un
contrato. Dabeiba es un piloto propuesto.

**Por eso va en Proyectos y nunca en Experiencia**, y por eso está prohibido escribir
"en producción", "desplegado" o "en uso" en su tarjeta. El contraste con Activisport es
justamente lo que hace creíble a Activisport.

### Dos correcciones de stack

| Lo que decía | La realidad verificada |
| --- | --- |
| Expo 51 | **Expo 54**, React Native 0.81.5, React 19 (el README del proyecto está viejo) |
| Arquitectura hexagonal | **Por capas dentro de cada dominio.** El ADR del proyecto rechaza las interfaces por servicio como YAGNI. La hexagonal es la de Activisport. |

Confirmado correcto: Spring Boot 3.2.5, Java 21, Next.js 14.2.21, PostgreSQL,
JWT con refresh rotativos, Flyway, Tailwind.

### Contrapeso honesto

Al cierre quedaron **7 hallazgos HIGH de seguridad abiertos**, el panel admin tiene un solo
archivo de tests y no hay cobertura instrumentada. Sin actividad desde el 11 de abril de 2026.

Conviene saberlo antes de que lo pregunte un entrevistador técnico.

---

## Invector

Marketplace de invenciones: los inventores publican proyectos con metas de inversión, los
inversores expresan interés, y un administrador aprueba antes de publicar. Fases de proyecto:
idea → prototipo → validado → escalado.

| Dato | Valor |
| --- | --- |
| Stack | Laravel 12 (PHP 8.2), React + Inertia.js 2.0, TypeScript, Vite, Tailwind |
| Librerías clave | `spatie/laravel-permission`, `nnjeim/world`, Ziggy, Radix UI |
| Commits | 67 |

Implementado: autenticación completa con verificación de correo, perfil con documento y
país/departamento/ciudad, perfil público de creador, CRUD de invenciones con asistente de
tres pasos y media, explorar con filtros, guardados e intereses de inversión, flujo de
aprobación con historial, módulos admin CRUD, dashboard con métricas, taxonomía de dos
niveles y permisos granulares.

**No es trabajo pagado.** Iba a ser un proyecto futuro con un interlocutor externo y quedó
detenido hasta nuevo aviso. Por eso va en Proyectos.

> La marca visible en las capturas es **KRINCHAKAU**, no Invector.
> Ver [pendientes.md](pendientes.md).

---

## Formación y datos personales

| Dato | Valor |
| --- | --- |
| Ingeniero de Software | Politécnico Grancolombiano, 2021 – 2024 |
| Tecnólogo en Análisis y Desarrollo | SENA, 2019 – 2021 |
| Bootcamp IA (33 h) | Udemy, finalizado 16 sep 2026 — [verificable](https://ude.my/UC-27739c3e-339c-433a-8e9e-00fd1cb595dc) |
| Habilidades comunicativas | Universidad Pontificia Bolivariana, 2025 |
| Ventas y atención al cliente | Universidad Católica de Oriente, 2025 |
| Curso Angular y Spring Boot | Udemy, 2025 |
| Ubicación | Dabeiba, Antioquia (Colombia) · disponibilidad remota |
| Idiomas | Español nativo · **inglés básico**, sin lectura de documentación técnica |
| Correo | `sergiose534@gmail.com` (confirmado) |
| Teléfono | +57 314 589 9773 |
| Métrica destacada de Serviunix | Informes críticos de **20 a 5 minutos** refactorizando Eloquent a SQL nativo |

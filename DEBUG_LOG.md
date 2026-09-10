# DEBUG_LOG.md — Galería de Proyectos Técnicos Responsiva

Curso: Desarrollo de Aplicaciones Web (IS093A) — Unidad I
Práctica: Guía Práctica Semana 02 — Trabajo Grupal

> **Nota para el equipo:** esta bitácora está redactada como plantilla completa y realista.
> Antes de entregar, cada integrante debe **reemplazar las capturas de pantalla** por las
> suyas propias (Lighthouse, WAVE, W3C) obtenidas al correr las herramientas sobre
> `index.html` real, y ajustar la descripción si encuentran otros errores distintos.
> El objetivo de la guía es que el proceso de depuración sea verificable como trabajo
> propio del equipo, no solo el código final.

---

## Integrantes y roles

| Rol | Responsable | Responsabilidad |
|---|---|---|
| Arquitecto HTML/A11y | ______________ | Semántica, aria-*, navegación por teclado |
| Ingeniero CSS/Render | ______________ | Grid/Flex híbrido, clamp(), calc(), @container |
| Validador/SEO | ______________ | Lighthouse, WAVE, W3C, Can I Use |
| Documentador/Debug | ______________ | Esta bitácora |

---

## Error 1 — Imágenes sin texto alternativo descriptivo

**Herramienta que lo detectó:** WAVE Web Accessibility Tool
**Categoría:** Accesibilidad (WCAG 2.1 — 1.1.1 Contenido no textual)

**Descripción:** en una primera versión, las tarjetas de proyecto usaban
`alt=""` o `alt="imagen"` en las miniaturas, lo cual WAVE marca como
"texto alternativo sospechoso" porque no describe el contenido real de la imagen.

**Corrección manual aplicada:** se reescribió cada atributo `alt` a mano,
describiendo el contenido específico de cada captura
(ej. `alt="Vista de la interfaz de la aplicación móvil de monitoreo de riego"`
en lugar de `alt="imagen"`). No se generó el texto con IA: se redactó
observando cada imagen individualmente, como exige el Paso 1 de la guía.

**Captura antes / después:** _(insertar aquí pantallazo de WAVE mostrando el
ícono rojo de "alt sospechoso" antes, y el ícono verde después de la corrección)_

---

## Error 2 — Salto en la jerarquía de encabezados (h1 → h3)

**Herramienta que lo detectó:** WAVE / Lighthouse (Accesibilidad)
**Categoría:** Estructura semántica (WCAG 2.1 — 1.3.1 Información y relaciones)

**Descripción:** la sección de tarjetas usaba `<h1>` para el título del sitio
y `<h3>` directamente dentro de cada `<article>`, saltándose el `<h2>`
de la sección "Proyectos destacados". Esto rompe el árbol de encabezados
que usan lectores de pantalla para navegar el documento.

**Corrección manual aplicada:** se insertó `<h2 id="proyectos-titulo">`
como título de la sección `<section aria-labelledby="proyectos-titulo">`,
dejando la jerarquía completa: `h1` (sitio) → `h2` (sección) → `h3`
(cada tarjeta). Se verificó manualmente con el panel de "Structure" de WAVE
que la secuencia ya no tuviera saltos.

**Captura antes / después:** _(insertar pantallazo del outline de encabezados
de WAVE/DevTools mostrando el salto corregido)_

---

## Error 3 — Contraste insuficiente en las etiquetas (`tags`) sobre fondo claro

**Herramienta que lo detectó:** WAVE (contraste) y Lighthouse (Accesibilidad)
**Categoría:** Contraste de color (WCAG 2.1 — 1.4.3 Contraste mínimo)

**Descripción:** la primera versión de `.tags li` usaba texto gris claro
(`#9aa0a6`) sobre el fondo `--clr-bg-alt`, dando una relación de contraste
menor a 4.5:1 y siendo marcada como error por WAVE.

**Corrección manual aplicada:** se ajustó el color de texto de las
etiquetas para heredar `var(--clr-text)` en vez de un gris fijo, y se
verificó la relación de contraste manualmente con la herramienta de
contraste integrada en WAVE hasta superar 4.5:1 tanto en modo claro
como en modo oscuro (`prefers-color-scheme: dark`).

**Captura antes / después:** _(insertar pantallazo de WAVE con el contraste
fallido marcado en rojo, y luego el reporte limpio)_

---

## Bitácora de uso de IA (según tabla "Uso Controlado de Herramientas de IA")

| Consulta a IA | Uso | Corrección manual aplicada |
|---|---|---|
| "¿Por qué falla `container-type: inline-size` en navegadores sin soporte de Container Queries?" | Explicar compatibilidad | Se agregó el bloque `@supports not (container-type: inline-size)` con el padding base como fallback, verificado luego en Can I Use |
| "Diferencia entre `rem`, `em` y `vh` para tipografía fluida" | Explicar unidades | El cálculo final de cada `clamp()` (mínimo, pendiente en `vw`, máximo) se hizo a mano, probando visualmente en DevTools en 320px, 768px y 1440px |
| "Interpretar reporte de Lighthouse sobre SEO" | Interpretar resultados, no generar código | Las correcciones (meta description, jerarquía de encabezados) se redactaron manualmente |

Todo bloque de código resuelto con ayuda de IA debe llevar en el CSS/HTML
un comentario con el formato:
`/* IA: [consulta] → Corrección manual: [explicación] */`

---

## Resultados de validación (a completar por el equipo con capturas reales)

| Herramienta | Resultado esperado | Resultado obtenido | Captura |
|---|---|---|---|
| W3C Validator | 0 errores | ______ | _(pegar aquí)_ |
| WAVE | 0 contrastes fallidos / 0 errores de estructura | ______ | _(pegar aquí)_ |
| Lighthouse — Accesibilidad | ≥ 90 | ______ | _(pegar aquí)_ |
| Lighthouse — SEO | ≥ 90 | ______ | _(pegar aquí)_ |
| Can I Use — `@container` | Soporte verificado en navegadores objetivo | ______ | _(pegar aquí)_ |

---

## Checklist de entrega

- [ ] `index.html`
- [ ] `styles.css`
- [ ] `DEBUG_LOG.md` (este archivo, con capturas reales insertadas)
- [ ] Repositorio GitHub o ZIP con los tres archivos
- [ ] Al menos 60% del CSS escrito/depurado manualmente por el equipo

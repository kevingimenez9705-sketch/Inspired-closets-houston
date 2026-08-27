# Revisión de alcance — Feedback del cliente sobre Preview V1.1

Fuente: `Inspired_Closet_Presentation_Comments.pdf` (10 páginas, comentarios del
cliente sobre la V1.1), recibido 2026-08-27.

Estado: **documento de trabajo para confirmar alcance con el cliente.**
Nada de lo listado abajo fue implementado todavía — es un mapeo de cada
pedido contra el estado actual del sitio (`index.html`, rama
`claude/v1-1-design-feedback-9kmzis`) más una estimación de esfuerzo y las
preguntas que conviene cerrar con el cliente antes de tocar código.

---

## 1. Portada — agregar elemento gráfico

**Pedido:** sumar un elemento gráfico/de diseño similar al de la
presentación original (círculos concéntricos superpuestos, ver captura de
la página 01 del PDF), manteniendo la adaptación visual para Houston.

**Estado actual:** la sección `Welcome` (index.html:474-489) es solo texto
— kicker, título, subtítulo y línea de contacto. No hay ningún elemento
gráfico/decorativo.

**Esfuerzo:** bajo. Es agregar un bloque visual (SVG/CSS, círculos
concéntricos con gradiente en los colores de marca vino/arena que ya usa
el sitio) en el layout del hero, sin tocar la estructura de navegación.

**Abierto:** ¿el cliente quiere el mismo motivo (círculos concéntricos) o
solo "algo gráfico" en ese lugar? La nota original dice "similar", así que
probablemente alcanza con esa forma reinterpretada en la paleta Houston.

---

## 2. Our Spaces — imágenes más grandes

**Pedido:**
- Mantener el concepto interactivo actual.
- Agrandar lo más posible las imágenes de las categorías (Closets, Pantry,
  Home Office, etc.) en la grilla.
- Al abrir una categoría, agrandar considerablemente las fotos internas
  también.
- La sección se va a usar fuerte para mostrar muchas fotos de
  productos/proyectos.

**Estado actual:**
- Grilla de categorías: `.spaces-grid` a 4 columnas, thumbnails de solo
  **84px de alto** (`.space-card .ph`, index.html:246).
- Modal de categoría: galería a `aspect-ratio: 1/1` dentro de un panel
  centrado (`.space-panel`, `.space-gallery`, index.html:272-317).

**Esfuerzo:** bajo-medio. Es ajuste de CSS (alturas de card, proporción de
imagen, anchos máximos del panel) más, si se quiere que la sección
"aguante" muchas más fotos por categoría, revisar cómo se cargan/pasan las
imágenes al array de cada espacio en el JS. No requiere rehacer el
concepto interactivo, que el cliente pidió mantener.

**Abierto:** ¿cuántas fotos por categoría hay que soportar realmente? Si
van a ser "muchas" (más de las ~3-5 actuales por espacio), conviene
pensar la galería como carrusel/grid con miniaturas en vez de solo
flechas prev/next, para que no se sienta lenta con más contenido.

---

## 3. Finishes / Materials / Hardware

**Pedido:** recuperar de la presentación original la posibilidad de
mostrar colores de acabado (finishes), opciones de hardware, accesorios y
detalles de materiales — como en el template original (Maxwell's
Austin/San Antonio), páginas "Hinges & drawer glides, side by side" y
"How it works".

**Estado actual:** no existe. El sitio Houston no tiene ninguna sección de
finishes/hardware/materiales. `Our Process` (index.html:529) es lo más
cercano y solo cubre las 4 etapas (Consult/Design/Prepare/Install), sin
detalle de materiales.

**Esfuerzo:** medio-alto. Es una **sección nueva completa**: necesita
contenido propio (nombres/fotos de acabados, hardware — bisagras, guías
de cajón — y accesorios) adaptado a lo que Inspired Closets Houston
realmente ofrece. No hay assets de esto en `inspired-closets-houston-content-pack/`
todavía.

**Abierto:** esto depende 100% de qué materiales/hardware/acabados
específicos ofrece Inspired Closets Houston (puede no ser el mismo
catálogo que Maxwell's Austin/San Antonio). Hace falta que el cliente
provea: lista de acabados con foto, marca/modelo de hardware, y rango de
accesorios a mostrar.

---

## 4. Panel vs. Hardwood (comparativa de materiales)

**Pedido:** página que explica la diferencia entre panel (TFL) y madera
maciza — "The right material for the job" (página 05/13 del original).

**Estado actual:** no existe ninguna sección comparativa de materiales.

**Esfuerzo:** medio. Es principalmente contenido + layout de dos columnas
(ya hay precedente de layouts en dos columnas en el sitio). El texto del
original es específico de Maxwell's ("TFL panel", "19 decorative
finishes") y habría que confirmar si Houston usa el mismo material/
argumento de venta o uno propio.

**Abierto:** ¿Inspired Closets Houston vende el mismo tipo de panel
(TFL) que Maxwell's, o es una marca/proveedor distinto? El copy de venta
no se puede copiar tal cual si el material real es otro.

---

## 5. Envision (video AR)

**Pedido:** página que muestra el video "Envision" — visualización 3D/AR
del clóset antes de construirlo.

**Estado actual:** no existe. No hay video ni sección de este tipo en el
sitio Houston.

**Esfuerzo:** depende de si Inspired Closets Houston tiene la misma
tecnología "Envision" que Maxwell's, o si esto es específico de la otra
marca/franquicia. Si Houston no tiene esa herramienta, la sección no
aplica tal cual y habría que decidir si se omite, se reemplaza por
renders 3D propios, o se confirma que sí existe el servicio.

**Abierto — bloqueante:** ¿Inspired Closets Houston ofrece la
funcionalidad Envision? Si no, este punto necesita una decisión de
producto antes de diseñar nada (no es solo un tema de layout).

---

## 6. Guarantee (Four guarantees, in writing)

**Pedido:** página de las 4 garantías (Price Match, Satisfaction, Lifetime
Warranty, Transferrable Warranty) tal como en el original.

**Estado actual:** no existe una sección de garantías. `Our Process`
tiene un ítem "05 · Love YOUR CLOSET / Lifetime guarantee" mencionado de
paso, pero no hay una página dedicada a las 4 garantías con detalle.

**Esfuerzo:** medio. Layout de 4 tarjetas ya tiene precedente visual en el
sitio (parecido a `spaces-grid` u `Our Process`). Lo que falta es
contenido: texto exacto de cada garantía para Houston (precios,
condiciones, si transfieren la garantía al nuevo dueño, etc.), que hay
que confirmar que sea igual a Maxwell's o propio de Houston.

**Abierto:** ¿las 4 garantías (price match, satisfaction/refund, lifetime
warranty, transferrable warranty) aplican igual para Houston, o hay
condiciones distintas (ej. el "83% of resale cost" es un dato de mercado
de Austin/San Antonio, no necesariamente válido para Houston)?

---

## 7. "Working with us is easy" — 5 pasos con detalle al click

**Pedido:** la página de proceso debe mostrar contenido expandido al
hacer click en cada una de las 5 opciones (Consult, Design, Prepare,
Install, Love your closet).

**Estado actual:** `Our Process` (index.html:529-551) ya existe con 4
pasos (Consult/Design/Prepare/Install) como texto estático, sin
interacción de click/expandir, y sin el 5º paso "Love your closet".

**Esfuerzo:** bajo-medio. Agregar el 5º paso es contenido; agregar el
comportamiento de click-to-expand por paso es interacción nueva pero el
sitio ya tiene el patrón de overlay/panel usado en Our Spaces, reutilizable
acá.

**Abierto:** ¿qué contenido extra debería aparecer al expandir cada paso?
El PDF no lo especifica, solo marca que "debe mostrar algo" al hacer
click — hay que pedirle al cliente el copy ampliado de cada etapa.

---

## 8. Financing (Custom storage, on your terms)

**Pedido:** página de financiamiento con oferta 0% APR, y página interna
con tabla de pagos estimados por mes (Wells Fargo Financing).

**Estado actual:** no existe ninguna sección de financiamiento en el
sitio Houston.

**Esfuerzo:** medio. Layout de oferta + tabla de pagos tiene precedente
(tablas simples, tarjetas). El bloqueante real es de negocio, no de
diseño.

**Abierto — bloqueante:** ¿Inspired Closets Houston ofrece financiamiento
con Wells Fargo (mismo programa que Maxwell's) o con otro proveedor? Los
montos/tasas/plazos de la tabla son específicos y no se pueden inventar —
hace falta que el cliente confirme el programa de financiamiento real
antes de construir esta sección.

---

## 9. Before & After (con antes/después por categoría)

**Pedido:** página "Real transformations, from your Texas neighbors" con
grilla de categorías, cada una abriendo una galería antes/después.

**Estado actual:** no existe. El sitio Houston no tiene sección de
before/after; sí tiene fotos de proyectos dentro de Our Spaces, pero sin
el formato comparativo antes/después.

**Esfuerzo:** medio-alto. Reutiliza el patrón interactivo de Our Spaces
(grilla → modal), pero necesita **fotos "antes" reales de proyectos de
Houston**, que hoy no están en el content pack (`images/services/` solo
tiene fotos finales, no "antes").

**Abierto — bloqueante de contenido:** ¿existen fotos "antes" de
proyectos reales de Houston? Sin eso la sección no se puede construir
con contenido genuino (y usar fotos antes/después de Austin/San Antonio
bajo la marca Houston sería engañoso).

---

## 10. Choose your adventure — cierre con 2 opciones

**Pedido:** página final con dos caminos: "Design in your home, today"
(diseño en vivo con fotos recientes) o "Meet in our showroom" (reservar
visita a showroom), con datos de contacto.

**Estado actual:** `Next Steps` (index.html:597) ya es la sección de
cierre/CTA, pero es más simple — no tiene las dos tarjetas "opción A /
opción B" ni el flujo de "swipe through recent projects".

**Esfuerzo:** bajo-medio. Es una reestructuración de la sección de cierre
existente a 2 tarjetas, reusando datos de contacto que el sitio ya tiene
(dirección, teléfono).

**Abierto:** el original ofrece "swipe through recent projects" en vivo
durante la reunión — ¿eso aplica al formato de preview web, o es algo que
hacía el diseñador en persona con su propio dispositivo? Si es lo
segundo, la versión web solo necesita el link/CTA, no la funcionalidad de
swipe.

---

## Resumen de prioridad y bloqueos

| # | Punto | Esfuerzo | ¿Bloqueado por contenido/negocio? |
|---|-------|----------|-----------------------------------|
| 1 | Elemento gráfico portada | Bajo | No |
| 2 | Imágenes más grandes en Our Spaces | Bajo-medio | No |
| 7 | 5 pasos con click en Our Process | Bajo-medio | Sí — falta copy ampliado |
| 10 | Choose your adventure (cierre) | Bajo-medio | Parcial — aclarar el "swipe" |
| 6 | Guarantee (4 garantías) | Medio | Sí — confirmar condiciones Houston |
| 4 | Panel vs Hardwood | Medio | Sí — confirmar material real |
| 3 | Finishes/Materials/Hardware | Medio-alto | Sí — falta catálogo Houston |
| 8 | Financing | Medio | **Sí, bloqueante** — confirmar proveedor/tasas |
| 5 | Envision (video AR) | Depende | **Sí, bloqueante** — confirmar si el servicio existe en Houston |
| 9 | Before & After | Medio-alto | **Sí, bloqueante** — faltan fotos "antes" |

**Los puntos 1, 2, 7 y 10 se pueden implementar ya** sin depender de
información nueva del cliente (7 y 10 con una vuelta rápida de copy).

**Los puntos 3, 4, 6, 8, 9 y especialmente 5** son secciones nuevas de
contenido de negocio: antes de tocar código hace falta que el cliente
confirme qué de todo eso realmente aplica a Inspired Closets Houston (que
puede no compartir programa de financiamiento, tecnología Envision, ni
catálogo de materiales con la franquicia Maxwell's Austin/San Antonio de
donde sale la presentación original), y provea el contenido real
(fotos, precios, condiciones).

## Próximo paso sugerido

Confirmar con el cliente, punto por punto, los "abiertos" marcados arriba
(especialmente los 3 bloqueantes: Envision, Financing, Before&After) antes
de iniciar la implementación. Con eso confirmado se puede planificar en
fases: Fase 1 (bajo esfuerzo, sin bloqueos) → Fase 2 (secciones nuevas con
contenido ya confirmado).

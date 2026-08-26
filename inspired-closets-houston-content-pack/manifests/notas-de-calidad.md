# Notas de calidad y validación

## Corrección 2026-08-26

La primera versión de este paquete tenía un error de integridad: 21 de las 36
imágenes eran copias byte-idénticas de otra imagen del paquete, mal etiquetadas
como fotos distintas (ej. el mismo retrato aparecía como Cassandra Perez, Juan
Juarez, Merary Torres y Pati Juarez a la vez; la misma foto de consulta
aparecía en closets, garage, pantry y laundry). El CSV afirmaba una
trazabilidad "alta" que el archivo real no respaldaba.

Se volvieron a descargar las 36 imágenes directamente desde las URLs listadas
en `source_asset` de `asset-map.csv`. Verificación por hash SHA-256: **36
archivos, 36 hashes únicos** — ya no hay duplicados. Las dimensiones en el CSV
también se corrigieron para reflejar el tamaño real del archivo descargado
(varias estaban mal registradas). Cada imagen fue revisada visualmente contra
su etiqueta (persona, servicio o paso del proceso) y coincide correctamente.

## Cobertura

- 36 imágenes descargadas desde los archivos originales expuestos por el sitio.
- 8 categorías de servicio.
- 4 imágenes del proceso.
- 6 retratos del equipo.
- 2 imágenes generales: showroom y appointment.

## Calidad de imagen

- Con las imágenes correctas ya verificadas, solo **showroom (1200x800)**, **appointment (1080x720)** e **install (1080x720)** superan los 1000 px. Son aptas para portada o pantalla completa.
- **Consult (600x400)**, **design (600x400)** y **prepare (600x398)** están en resolución media — sirven para tarjetas medianas, no para full-bleed.
- Los 6 retratos del equipo son 480x480 — correctos para tarjetas circulares/cuadradas de tamaño moderado.
- **Todo el resto (closet, garage, pantry, laundry, home office, murphy bed, entryway, entertainment)** son en realidad thumbnails de 196–300 px de lado. Son las imágenes reales que expone el sitio en esas secciones (no hay una versión de mayor resolución pública) — sirven para grillas de servicios en tamaño chico/mediano, pero **no alcanzan para full-bleed o portada**. Si el diseño final necesita esas categorías a pantalla completa, hay que pedir los originales de mayor resolución al cliente.
- Los nombres de archivo fueron normalizados sin alterar el contenido visual.

## Corrección 2026-08-26 (b) — realce de las 24 fotos de servicio

Se probaron sistemáticamente variantes de tamaño típicas de WordPress (300/600/768/
1024/1536/1920/2048px) para cada una de las 24 fotos de servicio contra el bucket S3
del cliente: ninguna devolvió una versión más grande. Confirmado — 196–300px es la
única resolución que el sitio expone públicamente para estas categorías.

Con eso confirmado, se aplicó un realce de calidad a las 24 (no inventa contenido,
solo reescala y afina lo que ya existe): upscale Lanczos a ~900–1000px de lado +
unsharp mask suave + leve ajuste de contraste/saturación. De paso se corrigió un bug
real: las 3 fotos de garage tienen canal alfa (fondo transparente, no negro); al
escalarlas antes sin componer el alfa sobre un fondo sólido, el borde circular
quedaba con un artefacto dentado negro muy visible al agrandar. Ahora se componen
sobre el mismo blanco cálido (#FBF7F0) del diseño antes de escalar.

## Alertas editoriales

- La página principal de Houston contiene un bloque titulado “Custom Closets in Holland, MI” junto a información de Houston. Parece contenido residual de una plantilla y no se incorporó como mensaje de la presentación.
- Los precios y tiempos de instalación son ejemplos del sitio, no presupuestos. Deben validarse antes de publicar.
- La página de Entryway procede de una copia más antigua que las demás y merece una comprobación final si se utilizará información comercial sensible.

## Confianza de asociaciones

- `alta`: la imagen está vinculada directamente a un nombre, paso, tipo de espacio o encabezado en la estructura del sitio.
- No se incluyeron asociaciones de baja confianza.

## Derechos

Los recursos pertenecen a Inspired Closets y/o sus titulares. Confirmar autorización antes de publicar, distribuir o reutilizar el material fuera del proyecto encargado.


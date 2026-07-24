# Auditoría técnica de la plantilla

## Hallazgos iniciales

- Los cinco notebooks eran ejemplos genéricos de descarga, películas, scraping,
  bases de datos y modelado, sin relación verificable con criminalidad en Cali.
- El README describía fechas y rutas distintas al proyecto actual.
- `requirements.txt` solo contenía herramientas de pruebas y no las librerías
  importadas por los notebooks.
- `api/`, `reportes/` y `webapp/` eran marcadores mínimos.
- La plantilla versionaba archivos `.DS_Store`, un temporal `~$...xlsx` y
  ejemplos binarios dentro de `data/raw/`.
- No existían controles para el grano agregado, el código oficial de Cali, el
  solapamiento entre fuentes o el denominador poblacional.

## Cambios técnicos

- Los notebooks 00–04 se reescribieron como pipeline Colab + Drive.
- El filtro por Cali ocurre por fuente antes de cualquier unión.
- Se incorporó trazabilidad con SHA-256, archivo y fila de origen.
- Hurto por Modalidades se conserva como complemento y se controla su
  solapamiento con Hurto a Personas.
- Se agregaron controles de fechas, cantidades, duplicados y cobertura DANE.
- El EDA se limitó a las preguntas 1–5, sin resultados inventados.
- El modelado quedó bloqueado detrás de puertas de calidad y no entrena nada.
- Los datos binarios de la plantilla se retiraron del seguimiento y las carpetas
  se conservan mediante archivos `.gitkeep`.

## Validación pendiente

La ejecución integral requiere Google Colab, autorización de Drive y los archivos
reales del proyecto. En desarrollo local se validan JSON, sintaxis de celdas,
codificación UTF-8, alcance del diff y ausencia de salidas ejecutadas.

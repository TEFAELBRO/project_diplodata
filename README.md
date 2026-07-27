# Vigía Cali

**Sistema auditable de vigilancia temporal de la criminalidad reportada para la
planeación institucional**

**Autores:** completar manualmente antes de la entrega.

Proyecto académico de ciencia de datos para auditar, preparar y explorar fuentes
agregadas de SIEDCO y población municipal del DANE. La implementación actual
llega únicamente hasta las preguntas 1–5 del EDA criminal-temporal.

## Propuesta de valor

El producto se plantea como un **sistema reproducible de vigilancia temporal de
la criminalidad reportada en Cali**. Su aporte diferencial es convertir fuentes
agregadas en evidencia trazable para:

- reconocer qué categorías concentran más reportes;
- comparar tasas anuales con denominadores poblacionales consistentes;
- detectar cambios temporales que requieren revisión;
- documentar las limitaciones antes de apoyar una decisión;
- habilitar, solo después de superar controles de calidad, un pronóstico mensual
  de homicidios para planeación y seguimiento.

El alcance no estima riesgo individual ni riesgo por comuna o barrio. Tampoco
recomienda despliegues operativos automáticos. Esta delimitación distingue el
producto de propuestas de mapas de riesgo territorial y reduce el riesgo de
estigmatizar zonas o comunidades.

## Estado

- Ingesta y trazabilidad por fuente: implementada para ejecución en Google Colab.
- Consolidación y calidad: implementadas con validaciones que bloquean resultados
  no confiables.
- EDA: limitado deliberadamente a las preguntas 1–5.
- Modelado: implementado para ejecución condicionada en Colab. El notebook 04
  compara una regresión de Poisson regularizada y un bosque aleatorio contra un
  baseline estacional, con validación temporal y prueba final separada.
- API y aplicación web: no implementadas.

No se incluyen resultados numéricos en Git porque los datos de Drive no están
disponibles en este entorno de desarrollo.

## Fuentes y grano

Entradas esperadas:

- Ocho CSV SIEDCO en
  `MyDrive/datav3/A1 - SIEDCO/datos_criminalidad_cali`.
- Uno o más Excel de población DANE bajo `MyDrive/datav3`.

Las filas SIEDCO son agregados. Por tanto:

- una fila no equivale a un delito individual;
- los totales se calculan con `sum(cantidad)`;
- Cali se filtra fuente por fuente mediante `cod_muni = 76001` o
  `codigo_dane = 76001000`;
- el nombre del municipio es solo una validación secundaria.

`Hurto por Modalidades` se trata como fuente complementaria. Sus registros de
Hurto a Personas se excluyen de la tabla canónica para evitar doble conteo. Solo
se incorporan las categorías de residencias, comercio, motocicletas y
automotores cuando la etiqueta de origen permite identificarlas.

## Ejecución en Google Colab

1. Abra Colab con la misma cuenta que tiene acceso a Drive.
2. Clone o abra este repositorio en Colab.
3. Ejecute los notebooks completos, en orden:

   1. `src/00_descargas.ipynb`
   2. `src/01_consolidar.ipynb`
   3. `src/02_limpieza.ipynb`
   4. `src/03_EDA.ipynb`
   5. `src/04_modelo.ipynb`

4. Autorice `drive.mount("/content/drive")`.
5. Confirme que cada notebook termina sin una excepción de control.
6. Revise primero los archivos de `audit/` antes de interpretar el EDA.

Las salidas reproducibles se escriben exclusivamente en:

```text
MyDrive/datav3/project_diplodata_outputs/eda_01_05_v1/
├── landing/
├── trusted/
├── surface/
├── audit/
└── reportes/
```

Las fuentes originales no se sobrescriben. Cambiar el identificador
`eda_01_05_v1` en todos los notebooks permite conservar una ejecución separada.

## Preguntas EDA implementadas

El notebook 03 conserva el texto y la intención de las primeras cinco preguntas
del documento de requisitos:

1. distribución total por tipo de delito;
2. tasas por 100.000 habitantes;
3. evolución y tendencia 2018–2025;
4. número de categorías crecientes, estables/no concluyentes o decrecientes;
5. extremos de homicidios y hurto a personas y patrones temporales comunes.

Las tasas se calculan por año usando población del mismo año. El resumen del
período usa personas-año y solo compara categorías con cobertura completa.
Cada pregunta conserva la secuencia solicitada para la socialización:
**Pregunta → Código → Respuesta → Guía de interpretación → Interpretación o
conclusión → Decisión que apoya**.

La diferenciación frente al proyecto de seguridad de Bucaramanga y las notas
extraídas de la socialización se documentan en
`reportes/DIFERENCIACION_PRODUCTO.md`.

## Reproducibilidad y controles

- Los inventarios guardan ruta, tamaño y SHA-256 de cada fuente.
- Las fechas se convierten fuente por fuente y los fallos quedan cuantificados.
- Los duplicados exactos y repeticiones agregadas ambiguas se reportan, pero no
  se eliminan automáticamente.
- Los archivos DANE se validan por código municipal, año y población positiva.
- Valores DANE conflictivos para un mismo año bloquean el cálculo de tasas.
- No se rellenan meses o años ausentes con cero sin evidencia de cobertura.
- El notebook 04 entrena modelos solo si todas las puertas de calidad se
  cumplen. No usa particiones aleatorias ni acepta machine learning si no supera
  el baseline estacional en la prueba final.

## Validación en este repositorio

Sin acceso al Drive del proyecto solo se puede validar estructura y sintaxis:

```bash
python -m pip install -r requirements.txt
python -m compileall src
```

Los notebooks deben validarse finalmente en Colab con **Entorno de ejecución →
Ejecutar todas**. Una ejecución completa debe producir los inventarios, tablas y
figuras en la carpeta de salida de Drive sin editar las entradas.

## Estructura

```text
src/       notebooks 00–04
data/      estructura local vacía; los datos no se versionan
reportes/  documentación técnica, no resultados generados
api/       alcance futuro
webapp/    alcance futuro
```

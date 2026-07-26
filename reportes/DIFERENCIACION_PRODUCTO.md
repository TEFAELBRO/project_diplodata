# Diferenciación del producto de datos

## Orientaciones obtenidas de la socialización

Las notas compartidas por el docente y los compañeros dejan cuatro requisitos
útiles para este proyecto:

1. actualizar en los cuadernos el nombre del proyecto, autores, fechas y demás
   datos de presentación antes de la entrega;
2. explicar qué decisiones permite apoyar el producto, no limitarse a mostrar
   resultados o predicciones;
3. indicar las unidades en tablas y gráficas;
4. conectar los resultados con planificación, prevención, evaluación y
   asignación responsable de recursos.

El primer punto requiere confirmación final de los autores y del título
académico. Los otros tres se incorporan en la estructura actual.

## Comparación con el proyecto de Bucaramanga

La única evidencia disponible es el texto de la socialización. Allí el proyecto
de Bucaramanga se describe como:

> Desarrollo de un producto de datos para la estimación del riesgo de delito
> por comuna y la predicción de su cantidad.

| Dimensión | Bucaramanga, según el chat | Producto de Cali |
|---|---|---|
| Unidad espacial | Comuna | Ciudad, sin estimar riesgo por comuna o barrio |
| Problema principal | Riesgo territorial y cantidad | Vigilancia temporal de reportes y calidad de la evidencia |
| Alcance delictivo del modelo | No especificado en el chat | Un único objetivo candidato: homicidios mensuales |
| Valor distintivo | Priorización territorial | Trazabilidad, tasas comparables, señales temporales y validación reproducible |
| Uso previsto | Planificación y prevención por territorio | Seguimiento periódico, planeación temporal y evaluación analítica |
| Salvaguarda | No verificable con el chat | No inferir riesgo individual, no estigmatizar zonas y no automatizar despliegues |

No se encontró una publicación pública del repositorio o documento de
Bucaramanga con la cual verificar su implementación. Por eso, esta comparación
valida la **diferencia de alcance declarada**, no una diferencia línea por línea
entre ambos códigos.

## Identidad recomendada

**Sistema reproducible de vigilancia temporal de la criminalidad reportada en
Santiago de Cali para apoyar la planeación y el seguimiento institucional.**

La palabra “reportada” es importante: SIEDCO no representa necesariamente toda
la criminalidad ocurrida. El sistema describe reportes agregados y hace visibles
la cobertura, el denominador, el período y las limitaciones de cada resultado.

## Decisiones que puede apoyar

- priorizar qué categorías requieren una revisión descriptiva más profunda;
- identificar años o tendencias que ameritan análisis contextual;
- comparar tasas anuales con una base poblacional consistente;
- definir si existe evidencia suficiente para diseñar un experimento predictivo;
- planear revisiones mensuales de homicidios cuando el modelo futuro supere un
  baseline y reporte incertidumbre.

## Decisiones que no debe automatizar

- clasificar personas o comunidades como peligrosas;
- afirmar causalidad a partir de correlaciones o tendencias;
- asignar patrullaje o presupuesto únicamente a partir del modelo;
- interpretar ausencia de registros como ausencia de delito;
- comparar categorías con coberturas temporales diferentes.

## Mensaje breve para la sustentación

> Nuestro producto no intenta replicar un mapa de riesgo por comuna. Se
> diferencia porque construye una cadena auditable para vigilar la evolución
> temporal de la criminalidad reportada en Cali. Antes de predecir, valida
> fuentes, códigos territoriales, cantidades, fechas, solapamientos y población.
> El resultado busca apoyar seguimiento y planeación con evidencia reproducible,
> sin convertir una predicción en una decisión automática.

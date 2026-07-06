# Clinical Deterioration Intelligence

Detección temprana de deterioro clínico en las primeras 72 horas de internación.
Proyecto de portfolio — Patricia Ruiz.

## Objetivo
Identificar qué pacientes tienen mayor riesgo de deteriorar clínicamente en las
primeras 72 horas, y construir un primer modelo de alerta temprana.

## Estado
- [x] Fase 0 — Organización del repo
- [x] Fase 1 — Diseccionar el encargo
- [x] Fase 2 — Aprender el dominio
- [x] Fase 3 — Modelar el dataset (ER)
- [x] Fase 3b — Glosario de métricas de negocio
- [x] Fase 4 — Setup técnico y reproducibilidad
- [x] Fase 5 — Primer contacto con los datos
- [x] Fase 6 — Auditoría de calidad de datos
- [x] Fase 7 — Limpieza y preparación (ETL)
- [ ] Fase 8 en adelante — pendiente

## Datos
Los archivos de datos (crudos y procesados) no se versionan en este repositorio
por su tamaño. El dataset original está disponible en:
kaggle.com/datasets/tarekmasryo/hospital-deterioration-dataset

El pipeline de limpieza (Fase 7, notebook 01_exploracion_limpieza.ipynb) documenta
paso a paso cómo se genera la versión procesada a partir de los datos crudos.

## Documentación
- `docs/contexto_dominio.md` — glosario clínico (signos vitales, labs, dispositivos de O₂)
- `docs/diccionario_datos.md` — definición de cada columna del dataset
- `docs/diagrama_er.md` — modelo entidad-relación e hipótesis de claves
- `docs/auditoria_calidad.md` — hallazgos de calidad de datos (Fase 6)
- `docs/log_limpieza.md` — decisiones de limpieza aplicadas y su justificación (Fase 7)

## Stack
Python (Google Colab) · SQL (BigQuery) · Power BI · GitHub

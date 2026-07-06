# Log de limpieza — Fase 7

## Decisiones aplicadas

### 1. Presión arterial inconsistente (vitals_timeseries)
- **Problema:** 1231 filas (0.295%) con systolic_bp < diastolic_bp,
  fisiológicamente imposible.
- **Decisión:** exclusión de esas filas del dataset limpio.
- **Justificación:** no es un caso clínico extremo válido (a diferencia de SpO2 bajo
  o FC alta, que sí son plausibles en pacientes graves) — es un error de carga o
  de sensor, sin forma de corregirlo sin inventar el dato real.
- **Impacto:** 1231 filas excluidas de vitals; se alinearon las mismas
  (patient_id, hour_from_admission) en labs para mantener consistencia entre tablas.

### 2. Valor centinela deterioration_hour = -1 (patients)
- **Naturaleza:** valor intencional del dataset, no un dato faltante.
- **Decisión:** se mantiene sin modificar. Representa "sin evento de deterioro"
  para 8062 de 10.000 pacientes (80.6%).
- **NO se imputa ni se trata como nulo.**

### 3. Nulos
- 0% de nulos en las tres tablas originales — no se requirió imputación.

### 4. Duplicados
- 0 duplicados de fila completa y de PK compuesta — no se requirió deduplicación.

## Resumen de volumen

| Tabla | Filas originales | Filas limpias | % excluido |
|---|---|---|---|
| patients | 10.000 | 10.000 | 0% |
| vitals | 417.866 | 416635 | 0.295% |
| labs | 417.866 | [completar con tu resultado real] | [completar] |

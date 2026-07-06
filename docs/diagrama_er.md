# Diagrama ER e hipótesis de claves — Fase 3 / validación Fase 5

## Granularidad
- patients.csv: 1 fila = 1 paciente (10.000 filas)
- vitals_timeseries.csv: 1 fila = 1 paciente en 1 hora
- labs_timeseries.csv: 1 fila = 1 paciente en 1 hora

## Claves primarias
- patients: PK simple (patient_id)
- vitals / labs: PK compuesta (patient_id, hour_from_admission)

## Diagrama
patients (PK: patient_id)
   |-- 1:N --> vitals_timeseries (FK: patient_id)
   |-- 1:N --> labs_timeseries (FK: patient_id)
vitals_timeseries <-- (patient_id + hour coinciden) --> labs_timeseries : relación 1:1 confirmada

## Tabla de hechos vs. dimensión
- Fact table: panel unido (vitals + labs + patients) a nivel paciente-hora.
- Dimensión: patients.csv.

## Hipótesis planteadas en la Fase 3 y su validación real (Fase 5)

1. HIPÓTESIS: labs tendría menos filas por paciente que vitals (los laboratorios no
   se miden tan seguido como los vitales).
   RESULTADO REAL: ambas tablas tienen EXACTAMENTE la misma cantidad de filas por
   paciente (promedio 41.79 cada una) - hipótesis NO confirmada tal como se planteó,
   pero el motivo real es otro: ningún paciente llega a las 72h completas (los_hours
   varía por paciente), así que ambas tablas están recortadas por igual según el
   alta real del paciente, no porque los labs se midan con menor frecuencia horaria.

2. HIPÓTESIS: patient_id es único y consistente entre las 3 tablas.
   RESULTADO REAL: confirmado. 0 pacientes de más o de menos entre patients, vitals y labs.

3. HIPÓTESIS: el nombre de la columna de tiempo seria "hour".
   RESULTADO REAL: corregido - la columna real se llama "hour_from_admission" en
   vitals y labs.

4. HIPÓTESIS: relación 1:1 entre vitals y labs por cada (patient_id, hour).
   RESULTADO REAL: confirmado en la muestra de prueba (join no multiplicó filas).

## Hallazgo adicional post-limpieza (Fase 7)
Se excluyeron 1231 filas de vitals por presión sistólica < diastólica (imposible
fisiológicamente). Se alineó labs_clean con las mismas (patient_id, hour_from_admission)
para mantener ambas tablas en el mismo universo de observaciones válidas.
Panel final unido: 416.635 filas, 27 columnas.

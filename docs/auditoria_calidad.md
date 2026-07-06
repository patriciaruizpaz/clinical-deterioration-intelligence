# Auditoría de calidad de datos — Fase 6

## Nulos
0% de nulos en las tres tablas (patients, vitals, labs) - sin excepciones.

## Duplicados
- Filas 100% duplicadas: 0 en las tres tablas.
- PK compuesta (patient_id + hour_from_admission): 0 duplicados en vitals y labs.

## Consistencia lógica
- Sistólica < diastólica (imposible fisiológicamente): 1231 filas encontradas en vitals.
- oxygen_device = "none" con oxygen_flow > 0: 0 filas (consistente).
- deterioration_hour posterior al propio los_hours del paciente: 0 pacientes (consistente).

## Categóricas
- gender: M, F (limpio, sin variantes).
- admission_type: Elective, Transfer, ED (limpio). Distribución real: ED 64.3%,
  Elective 25.9%, Transfer 9.8%.
- oxygen_device: none, nasal, mask, hfnc, niv (limpio, 5 categorías esperadas).

## Valores centinela identificados
- deterioration_hour = -1: valor intencional, "sin evento de deterioro" (8062 pacientes,
  80.6%). NO se trata como nulo ni se imputa.

## Clipping detectado en el EDA (Fase 8, hallazgo adicional)
Se observan picos anómalos en los extremos de varias variables continuas
(systolic_bp, diastolic_bp, lactate, crp_level, sepsis_risk_score, heart_rate,
respiratory_rate, spo2_pct, wbc_count) - consistente con límites de generación
del dataset sintético (censura/clipping), no con datos reales de pacientes.
Se interpreta con cautela cualquier análisis de percentiles extremos en estas variables.

## Multicolinealidad detectada (Fase 8, hallazgo adicional)
Los marcadores de laboratorio (lactate, creatinine, crp_level, wbc_count) están
correlacionados fuertemente entre sí (r > 0.80 en varios pares), no solo con el
sepsis_risk_score que los combina. Sugiere que el dataset sintético los generó a
partir de una variable oculta de "gravedad general". Implica que no se pueden meter
todos juntos en la regresión logística (Fase 11) sin evaluar VIF o seleccionar un
subconjunto representativo.

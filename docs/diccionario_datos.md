# Diccionario de datos — Clinical Deterioration Intelligence

## patients.csv (1 fila = 1 paciente, 10.000 filas)

| Columna | Significado | Tipo / unidad |
|---|---|---|
| patient_id | Identificador único del paciente | entero |
| age | Edad del paciente | años |
| gender | Sexo del paciente | M / F |
| comorbidity_index | Índice de comorbilidad | entero, mayor = más frágil |
| admission_type | Tipo de admisión | Elective / Transfer / ED |
| baseline_risk_score | Score de riesgo basal al ingreso | decimal 0-1 |
| los_hours | Duración de la internación (Length of Stay) | horas |
| deterioration_event | Si tuvo algún evento de deterioro en toda la internación | 0/1 |
| deterioration_within_12h_from_admission | Si deterioró dentro de las primeras 12h desde el ingreso | 0/1 |
| deterioration_hour | Hora (desde ingreso) del evento de deterioro | entero, -1 = no aplica (valor centinela intencional) |

## vitals_timeseries.csv (1 fila = paciente + hora, PK compuesta: patient_id + hour_from_admission)

| Columna | Significado | Tipo / unidad |
|---|---|---|
| patient_id | Identificador del paciente | entero |
| hour_from_admission | Horas desde el ingreso (reloj propio de cada paciente) | entero |
| heart_rate | Frecuencia cardíaca | latidos/min |
| respiratory_rate | Frecuencia respiratoria | respiraciones/min |
| spo2_pct | Saturación de oxígeno | % |
| temperature_c | Temperatura corporal | °C |
| systolic_bp | Presión arterial sistólica | mmHg |
| diastolic_bp | Presión arterial diastólica | mmHg |
| oxygen_device | Dispositivo de oxígeno (none/nasal/mask/hfnc/niv) | categórica |
| oxygen_flow | Flujo de oxígeno administrado | litros/min |
| mobility_score | Score de movilidad | escala numérica |
| nurse_alert | Alerta de enfermería en esa hora | 0/1 |

## labs_timeseries.csv (1 fila = paciente + hora, PK compuesta: patient_id + hour_from_admission)

| Columna | Significado | Tipo / unidad |
|---|---|---|
| patient_id | Identificador del paciente | entero |
| hour_from_admission | Horas desde el ingreso | entero |
| wbc_count | Glóbulos blancos | x10³/µL |
| lactate | Lactato | mmol/L |
| creatinine | Creatinina | mg/dL |
| crp_level | Proteína C reactiva | mg/L |
| hemoglobin | Hemoglobina | g/dL |
| sepsis_risk_score | Score compuesto de riesgo de sepsis | decimal 0-1 |

## Archivos adicionales confirmados en Drive (pendiente de inspeccionar en detalle)
- hospital_deterioration_hourly_panel.csv — panel horario ya unido, provisto por el dataset original.
- hospital_deterioration_ml_ready.csv — features listas para modelado con variable objetivo.

# Contexto de dominio — Clinical Deterioration Intelligence

## Signos vitales (medidos con sensores, en tiempo real)
- Frecuencia cardíaca (heart_rate): normal 60-100 bpm. Taquicardia >100, bradicardia <60.
- Frecuencia respiratoria (respiratory_rate): normal 12-20/min. Taquipnea >24, <8 preocupante.
- SpO2 (spo2_pct): saturación de oxígeno. Normal 95-100%, preocupante <92%, grave <88%.
- Temperatura (temperature_c): normal 36-37.5°C. Alarma en ambos extremos: fiebre >38°C
  o hipotermia <36°C (en sepsis, la hipotermia es tan grave como la fiebre).
- Presión arterial (systolic_bp / diastolic_bp): normal ~90-140 / 60-90.
  Hipotensión (sistólica <90): señal clásica de shock o sepsis avanzada.

## Variables de laboratorio (medidas con muestra de sangre, no en tiempo real)
- Lactato (lactate): marcador de falta de oxígeno en tejidos. Normal <2 mmol/L, grave >4.
- WBC (wbc_count): glóbulos blancos, respuesta inmune a infección.
- PCR / CRP (crp_level): marcador de inflamación general.
- Creatinina (creatinine): función renal. Sube con daño renal agudo.
- Score de riesgo de sepsis (sepsis_risk_score): score compuesto de vitales+labs, no es
  una medición directa. Mayor = más riesgo.

## Intervenciones (acciones del equipo médico, no mediciones del cuerpo)
- Dispositivo de oxígeno (oxygen_device): escalera de soporte, cada escalón implica más
  gravedad que el anterior: ninguno -> nasal -> mascara -> hfnc -> niv.
  El CAMBIO de escalón es tan informativo como el valor puntual de SpO2.

## Variables del paciente (una sola vez, no cambian hora a hora)
- Índice de comorbilidad (comorbidity_index): resume enfermedades crónicas de base.
  Mayor = paciente más frágil (similar en concepto al Índice de Charlson).
- LOS (los_hours): duración total de la internación, en horas.
- Tipo de admisión (admission_type): Elective, Transfer, ED (guardia/emergencia).

## Reglas de negocio implícitas
- Datos anidados por paciente: cada paciente tiene múltiples filas horarias (hasta 72),
  que NO son independientes entre sí (pseudo-replicación si se tratan como si lo fueran).
- Autocorrelación temporal: el valor de una hora está correlacionado con el de la hora anterior
  del mismo paciente.
- Ningún paciente llega a las 72h completas de monitoreo (los_hours varía, promedio ~42h) -
  el monitoreo dura hasta el alta o desenlace real del paciente, no un máximo fijo.

## Benchmarks de referencia
- Sistemas de alerta temprana tipo NEWS2: revisión clínica con score >=5, urgencia con >=7.
- Tasa de deterioro/eventos adversos en sala general: ~4-10% (benchmark genérico).
  En este dataset: deterioration_event = 19.4% (cohorte de alto riesgo por diseño, no un error).

## Traducción número -> frase clínica (para reportar hallazgos)
- Odds ratio de 2.3 en comorbilidad alta -> "un paciente con comorbilidad alta tiene poco
  más del doble de probabilidad de deteriorar que uno de comorbilidad baja."
- Lactato p90 de 5.2 -> "1 de cada 10 pacientes de este grupo tiene un lactato compatible
  con sepsis grave."

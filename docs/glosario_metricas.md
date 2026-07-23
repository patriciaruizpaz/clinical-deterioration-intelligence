# Glosario de métricas de negocio — Fase 3b / corrección Fase 8

## Tasa de deterioro dentro de las 12h desde el ingreso (CORREGIDA - a nivel PACIENTE)
Definición de negocio: de cada 100 pacientes, cuántos deterioran dentro de las
primeras 12 horas desde su ingreso.
Formula: (pacientes con deterioration_within_12h_from_admission = 1) / (total pacientes) x 100
Resultado real: 3.1% de los pacientes.
Nota: la definición original (Fase 3b) asumía una columna a nivel HORA
(deterioration_next_12h) que no existe en el dataset real. Se corrigió a nivel paciente.
Dónde se calcula: Python (Fase 8).

## Tasa de deterioro global (en toda la internación)
Definición de negocio: de cada 100 pacientes, cuántos tuvieron algún evento de
deterioro en cualquier momento de su internación.
Fórmula: (pacientes con deterioration_event = 1) / (total pacientes) x 100
Resultado real: 19.4%.
Nota: distinta de la métrica anterior - esta cuenta TODA la internación, no solo
las primeras 12h. No confundir ambas al reportar resultados.

## Score de riesgo de sepsis (promedio y p90)
Definición de negocio: qué tan alto es, en promedio, el riesgo de sepsis de la
cohorte, y qué tan grave es el 10% de casos más severos.
Fórmula: promedio(sepsis_risk_score) y percentil 90, agrupado por comorbilidad.
Filas incluidas: todas (0% nulos confirmado en Fase 6).
Dónde se calcula: Python (EDA) + SQL (pregunta 6).

## Distribución de dispositivo de oxígeno
Definición de negocio: % de horas monitoreadas sin soporte, con soporte bajo o alto.
Fórmula: (filas con esa categoría) / (total de filas) x 100
Dónde se calcula: Python (EDA) + Power BI.

## Advertencia de escala (hora vs. paciente)
Varias métricas de este proyecto existen en dos escalas distintas y NO deben
confundirse entre sí: "a nivel hora" (cada fila = una observación horaria) vs.
"a nivel paciente" (cada fila = un paciente). Ejemplo: la tasa de deterioro dentro
de 12h y el score de sepsis promedio deben reportarse siempre aclarando en qué
nivel se calcularon.

## Validación — Tasa de deterioro a 12h (confirmado en Fase 9)
Resultado real sobre panel_con_target.csv (416.635 filas horarias):
- No deteriora en las próximas 12h: 94.61%
- Deteriora en las próximas 12h: 5.39%

Fuente: columna deterioration_next_12h de hospital_deterioration_hourly_panel.csv,
unida al panel limpio por (patient_id, hour_from_admission).

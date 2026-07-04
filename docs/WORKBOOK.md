# Workbook Documentation / Documentacion del Workbook

## Espanol

## Archivo

- `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx`

## Objetivo

El workbook registra asistencia, calcula campos auxiliares, clasifica entradas con un semaforo y resume resultados por supervisor.

## Hojas

| Hoja | Descripcion |
| --- | --- |
| `REGISTRO` | Base de asistencia con fecha, empleado, entrada, salida, calculos y novedad. |
| `PERSONAL` | Catalogo de colaboradores, supervisores, activo y reglas de horario. |
| `NORMALIDAD` | Calendario auxiliar 2026. |
| Hojas de supervisor | Tableros mensuales con conteos y grafica. |

## Estados del semaforo

| Estado | Significado |
| --- | --- |
| `VERDE` | Entrada dentro del rango esperado. |
| `AMARILLO` | Alerta leve por entrada posterior al umbral amarillo. |
| `ROJO` | Alerta por entrada posterior al umbral rojo. |
| `ROJO FUERTE` | Alerta severa por entrada posterior al umbral mas alto. |
| `FALTA` | No hay entrada registrada y no existe novedad. |
| `REVISAR` | El empleado o sus reglas no se encontraron correctamente. |
| `VACACIONES` | Novedad autorizada. |
| `FESTIVO` | Novedad autorizada. |
| `INCAPACIDAD` | Novedad autorizada. |
| `PERMISO` | Novedad autorizada. |

## Reglas

- Si existe `NOVEDAD`, esa novedad tiene prioridad sobre el calculo del semaforo.
- Si no hay `ENTRADA`, el resultado es `FALTA`.
- Si hay `ENTRADA`, se compara con los umbrales definidos en `PERSONAL`.
- `TIPO DIA` define si se usan reglas `L-V` o `S-D`.

## Tableros

Cada tablero de supervisor usa `COUNTIFS` para contar estados por colaborador y mes. Tambien calcula totales, porcentaje verde, registros y promedio de horas.

---

## English

## File

- `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx`

## Purpose

The workbook records attendance, calculates helper fields, classifies check-ins with a traffic-light status, and summarizes results by supervisor.

## Sheets

| Sheet | Description |
| --- | --- |
| `REGISTRO` | Attendance database with date, employee, check-in, check-out, calculations, and exception. |
| `PERSONAL` | Employee catalog, supervisors, active status, and schedule rules. |
| `NORMALIDAD` | 2026 helper calendar. |
| Supervisor sheets | Monthly dashboards with counts and chart. |

## Traffic-light states

| State | Meaning |
| --- | --- |
| `VERDE` | Check-in within the expected range. |
| `AMARILLO` | Mild alert for check-in after the yellow threshold. |
| `ROJO` | Alert for check-in after the red threshold. |
| `ROJO FUERTE` | Severe alert for check-in after the highest threshold. |
| `FALTA` | No check-in registered and no exception exists. |
| `REVISAR` | Employee or rules were not found correctly. |
| `VACACIONES` | Authorized exception. |
| `FESTIVO` | Authorized exception. |
| `INCAPACIDAD` | Authorized exception. |
| `PERMISO` | Authorized exception. |

## Rules

- If `NOVEDAD` exists, that exception has priority over traffic-light calculation.
- If there is no `ENTRADA`, the result is `FALTA`.
- If `ENTRADA` exists, it is compared against thresholds defined in `PERSONAL`.
- `TIPO DIA` defines whether `L-V` or `S-D` rules are used.

## Dashboards

Each supervisor dashboard uses `COUNTIFS` to count states by employee and month. It also calculates totals, green percentage, records, and average hours.

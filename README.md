# Sistema de Asistencia con Semaforo en Excel

Herramienta en Microsoft Excel para revisar asistencia, retardos, faltas y cumplimiento de horarios mediante una clasificacion visual tipo semaforo.

Este proyecto usa una version demo anonimizada. Todos los nombres, numeros de empleado y registros incluidos son ficticios y se usan solo como ejemplo de funcionamiento.

## Archivo publico

- `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx`

## Que problema resuelve

El archivo ayuda a convertir registros de entrada y salida en metricas faciles de revisar. En lugar de contar manualmente retardos o faltas, el sistema clasifica cada registro y resume los resultados por supervisor y colaborador.

## Como se usa

1. Abrir el archivo `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx`.
2. Revisar la hoja `PERSONAL` para ver el catalogo demo de colaboradores.
3. Revisar la hoja `REGISTRO`, donde estan las fechas, entradas, salidas y clasificacion del semaforo.
4. Abrir las hojas de supervisor para consultar el resumen por equipo.
5. Cambiar el periodo en el resumen si se desea revisar otro mes disponible en los registros.

## Hojas principales

### `PERSONAL`

Contiene el catalogo de colaboradores demo.

Ejemplo ficticio:

| No. EMP | NOMBRE | SUPERVISOR | ACTIVO |
| --- | --- | --- | --- |
| 7001 | SOFIA MORALES VEGA | CAMILA RIVERA NAVA | SI |
| 7002 | DIEGO RAMIREZ PENA | CAMILA RIVERA NAVA | SI |

### `REGISTRO`

Contiene los registros de asistencia. La columna `NOVEDAD` permite marcar un dia como excepcion (vacaciones, incapacidad, permiso o festivo) mediante una lista desplegable; cuando se llena, sobrescribe la clasificacion automatica del semaforo para ese dia.

Ejemplo ficticio:

| FECHA | No. EMP | ENTRADA | SALIDA | SEMAFORO | NOVEDAD |
| --- | --- | --- | --- | --- | --- |
| 01/06/2026 | 7001 | 08:00 | 17:00 | VERDE | |
| 01/06/2026 | 7002 | 08:12 | 17:00 | AMARILLO | |
| 02/06/2026 | 7003 | - | - | FALTA | |
| 03/06/2026 | 7004 | - | - | VACACIONES | VACACIONES |

### Hojas de supervisor

Muestran el resumen del equipo asignado:

- Total de registros verdes.
- Total de registros amarillos.
- Total de registros rojos.
- Total de faltas.
- Total de dias de vacaciones, festivos, incapacidades y permisos.
- Porcentaje de cumplimiento.
- Promedio o conteo de horas segun el registro disponible.
- Grafica de distribucion mensual por colaborador.

## Clasificacion del semaforo

- `VERDE`: asistencia dentro del rango esperado.
- `AMARILLO`: retardo leve o alerta inicial.
- `ROJO`: retardo mayor.
- `ROJO FUERTE`: incumplimiento mas severo.
- `FALTA`: ausencia o registro incompleto segun la regla configurada.
- `VACACIONES`: dia marcado como vacaciones en la columna NOVEDAD.
- `FESTIVO`: dia marcado como festivo en la columna NOVEDAD.
- `INCAPACIDAD`: dia marcado como incapacidad en la columna NOVEDAD.
- `PERMISO`: dia marcado como permiso en la columna NOVEDAD.

## Tecnologias usadas

- Microsoft Excel
- Formulas condicionales
- `IF`
- `COUNTIFS`
- Catalogos auxiliares
- Resumen por periodo
- Clasificacion por reglas de negocio

## Privacidad

Esta version no contiene datos reales. Antes de publicarse:

- Los nombres fueron reemplazados por nombres inventados.
- Los numeros de empleado fueron reemplazados por identificadores ficticios.
- Los registros se dejaron como datos de demostracion.
- El archivo original no debe publicarse.

## Valor del proyecto

Este proyecto demuestra capacidad para:

- Automatizar reportes operativos en Excel.
- Transformar registros crudos en indicadores.
- Crear tableros simples para seguimiento de equipos.
- Reducir conteos manuales.
- Presentar informacion clara para toma de decisiones.

---

# Excel Attendance Traffic Light System

Microsoft Excel tool for reviewing attendance, lateness, absences, and schedule compliance through a visual traffic light classification system.

This project uses an anonymized demo version. All names, employee numbers, and records included in the file are fictional and are used only to demonstrate how the system works.

## Public File

- `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx`

## Problem Solved

The workbook helps turn clock-in and clock-out records into easy-to-review metrics. Instead of manually counting late arrivals or absences, the system classifies each record and summarizes results by supervisor and employee.

## How To Use

1. Open `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx`.
2. Review the `PERSONAL` sheet to see the demo employee catalog.
3. Review the `REGISTRO` sheet, where dates, check-in times, check-out times, and traffic light classifications are stored.
4. Open the supervisor sheets to review team summaries.
5. Change the period in the summary if you want to review another available month.

## Main Sheets

### `PERSONAL`

Contains the demo employee catalog.

Fictional example:

| EMP No. | NAME | SUPERVISOR | ACTIVE |
| --- | --- | --- | --- |
| 7001 | SOFIA MORALES VEGA | CAMILA RIVERA NAVA | YES |
| 7002 | DIEGO RAMIREZ PENA | CAMILA RIVERA NAVA | YES |

### `REGISTRO`

Contains attendance records. The `NOVEDAD` (exception) column lets you flag a day as vacation, sick leave, personal leave, or holiday through a dropdown list; when filled in, it overrides the automatic traffic-light classification for that day.

Fictional example:

| DATE | EMP No. | CHECK-IN | CHECK-OUT | STATUS | EXCEPTION |
| --- | --- | --- | --- | --- | --- |
| 06/01/2026 | 7001 | 08:00 | 17:00 | GREEN | |
| 06/01/2026 | 7002 | 08:12 | 17:00 | YELLOW | |
| 06/02/2026 | 7003 | - | - | ABSENCE | |
| 06/03/2026 | 7004 | - | - | VACATION | VACATION |

### Supervisor Sheets

Show each team's summary:

- Total green records.
- Total yellow records.
- Total red records.
- Total absences.
- Total vacation, holiday, sick leave, and personal leave days.
- Compliance percentage.
- Average or total hours depending on the available record.
- Monthly distribution chart per team member.

## Traffic Light Classification

- `GREEN`: attendance within the expected range.
- `YELLOW`: minor lateness or first alert.
- `RED`: greater lateness.
- `STRONG RED`: more severe non-compliance.
- `ABSENCE`: absence or incomplete record according to the configured rule.
- `VACATION`: day flagged as vacation in the exception column.
- `HOLIDAY`: day flagged as a holiday in the exception column.
- `SICK LEAVE`: day flagged as sick leave in the exception column.
- `PERSONAL LEAVE`: day flagged as personal leave in the exception column.

## Technologies Used

- Microsoft Excel
- Conditional formulas
- `IF`
- `COUNTIFS`
- Helper catalogs
- Period summaries
- Business rule classification

## Privacy

This version does not contain real data. Before publication:

- Names were replaced with fictional names.
- Employee numbers were replaced with fictional identifiers.
- Records were kept as demonstration data.
- The original file should not be published.

## Project Value

This project demonstrates the ability to:

- Automate operational reports in Excel.
- Transform raw records into indicators.
- Create simple dashboards for team tracking.
- Reduce manual counting.
- Present clear information for decision-making.


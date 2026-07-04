# Sistema de Asistencia con Semáforo en Excel / Excel Attendance Traffic-Light System

Sistema de control de asistencia construido 100% en Microsoft Excel (sin macros) que convierte registros de entrada y salida en un semáforo operativo automático, con tableros mensuales por supervisor.

A 100% Microsoft Excel system (no macros) that turns check-in/check-out records into an automatic operational traffic light, with monthly dashboards per supervisor.

---

## Índice

- [Español](#español)
  - [Resumen del proyecto](#resumen-del-proyecto)
  - [Archivo incluido](#archivo-incluido)
  - [Qué problema resuelve](#qué-problema-resuelve)
  - [Estructura del libro](#estructura-del-libro)
  - [Flujo de trabajo](#flujo-de-trabajo)
  - [Lógica del semáforo](#lógica-del-semáforo)
  - [Catálogo de personal](#catálogo-de-personal)
  - [Tableros por supervisor](#tableros-por-supervisor)
  - [Características principales](#características-principales)
  - [Ejemplo de uso](#ejemplo-de-uso)
  - [Control de calidad](#control-de-calidad)
  - [Cómo adaptarlo](#cómo-adaptarlo)
  - [Requisitos](#requisitos)
  - [Descargar o clonar](#descargar-o-clonar)
  - [Privacidad](#privacidad)
  - [Tecnologías y fórmulas usadas](#tecnologías-y-fórmulas-usadas)
  - [Valor del proyecto](#valor-del-proyecto)
  - [Posibles mejoras futuras](#posibles-mejoras-futuras)
- [English](#english)
  - [Project summary](#project-summary)
  - [Included file](#included-file)
  - [What problem it solves](#what-problem-it-solves)
  - [Workbook structure](#workbook-structure)
  - [Workflow](#workflow)
  - [Traffic-light logic](#traffic-light-logic)
  - [Employee catalog](#employee-catalog)
  - [Supervisor dashboards](#supervisor-dashboards)
  - [Main features](#main-features)
  - [Usage example](#usage-example)
  - [Quality assurance](#quality-assurance)
  - [How to adapt it](#how-to-adapt-it)
  - [Requirements](#requirements)
  - [Download or clone](#download-or-clone)
  - [Privacy](#privacy)
  - [Technologies and formulas used](#technologies-and-formulas-used)
  - [Project value](#project-value)
  - [Future improvements](#future-improvements)

---

# Español

## Resumen del proyecto

Este repositorio contiene un sistema de asistencia hecho en Microsoft Excel. El archivo registra entradas y salidas, clasifica cada registro con un semáforo operativo (`VERDE`, `AMARILLO`, `ROJO`, `ROJO FUERTE`, `FALTA` o una novedad autorizada) y resume resultados por supervisor, colaborador y mes, sin necesidad de macros ni herramientas externas.

Este proyecto forma parte de mi portafolio profesional. La versión publicada es una demostración genérica: representa el mismo diseño y la misma lógica que un sistema real, pero con datos, nombres y volumen totalmente ficticios, pensados solo para ilustrar el funcionamiento.

## Archivo incluido

- [`Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx`](Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx)

Este es el único libro que se publica en este repositorio. No requiere macros, complementos ni software adicional: funciona con fórmulas de Excel, validaciones de datos, filtros, formato condicional y gráficas.

## Qué problema resuelve

En equipos donde la asistencia se controla manualmente (checador, bitácora o reportes sueltos), revisar puntualidad y ausentismo mes a mes implica contar registros a mano por cada colaborador y por cada supervisor. Este archivo automatiza ese conteo:

- Convierte una lista plana de entradas y salidas en un estado inmediato por color (semáforo).
- Aplica reglas de horario propias de cada colaborador y distintas para entre semana / fin de semana, sin fórmulas manuales por persona.
- Separa incumplimientos (retardos, faltas) de excepciones autorizadas (vacaciones, incapacidad, permiso, festivo), para no penalizar ausencias justificadas.
- Entrega a cada supervisor un tablero mensual propio con totales, porcentaje de cumplimiento y promedio de horas, listo para revisión sin depender de un analista o de otro sistema.

## Estructura del libro

El workbook se organiza en tres tipos de hoja:

| Tipo de hoja | Función |
| --- | --- |
| `REGISTRO` | Base principal de asistencia. Aquí se capturan fecha, empleado, entrada, salida y novedades. |
| `PERSONAL` | Catálogo de colaboradores, supervisores, estatus activo y reglas de clasificación por horario. |
| `NORMALIDAD` | Calendario auxiliar con días de la semana y catálogo de meses. |
| Tableros de supervisor | Una hoja por supervisor con el resumen mensual de su equipo. La demo incluye varias hojas de ejemplo con nombres ficticios. |

## Flujo de trabajo

1. Abrir el archivo en Microsoft Excel.
2. Revisar o actualizar el catálogo en `PERSONAL`.
3. Cargar registros diarios en `REGISTRO`.
4. Usar la columna `NOVEDAD` cuando un día tenga justificación autorizada.
5. Elegir el mes en el selector de cada hoja de supervisor.
6. Revisar conteos, porcentaje verde, registros, promedio de horas y gráfica.

> Nota: como el archivo usa fórmulas, Excel recalcula los resultados al abrirlo. La vista previa de GitHub no siempre muestra el workbook igual que Excel de escritorio; para verlo con fórmulas activas hay que descargarlo y abrirlo en Excel.

## Lógica del semáforo

`REGISTRO` es la base de datos operativa, con encabezados congelados y filtro sobre el rango principal. Cada fila calcula automáticamente, a partir de la fecha, el empleado, la entrada y la salida:

| Columna | Descripción |
| --- | --- |
| `NOMBRE` / `SUPERVISOR` | Se obtienen automáticamente desde `PERSONAL` mediante búsqueda por número de empleado. |
| `DÍA` / `MES` / `TIPO DÍA` | Se calculan a partir de la fecha (día de la semana, mes y si es entre semana o fin de semana). |
| `SEMÁFORO` | Resultado final de la regla de clasificación. |
| `HORAS` | Horas entre entrada y salida, incluyendo turnos que cruzan la medianoche. |
| `NOVEDAD` | Lista desplegable para registrar excepciones autorizadas. |

La columna `SEMÁFORO` sigue esta prioridad:

1. Si falta fecha o número de empleado, el resultado queda vacío.
2. Si existe una `NOVEDAD` (vacaciones, incapacidad, permiso, festivo), esa excepción tiene prioridad sobre la hora de entrada.
3. Si no hay hora de entrada, se clasifica como `FALTA`.
4. Si hay entrada, se compara contra los umbrales configurados para ese colaborador, evaluando primero los niveles más severos (rojo fuerte → rojo → amarillo → verde).
5. Si el empleado no existe o su configuración no es válida, el resultado es `REVISAR`.

Cada colaborador tiene su propio conjunto de umbrales (hora base, tolerancia amarilla, umbral rojo y umbral rojo fuerte), definidos por separado para días entre semana y para fin de semana. Esto permite que equipos con turnos distintos convivan en el mismo archivo sin duplicar hojas ni fórmulas.

El formato condicional pinta el campo `SEMÁFORO` por estado: verde, amarillo, rojo, rojo fuerte, gris para faltas y morado para las excepciones autorizadas.

## Catálogo de personal

`PERSONAL` es el catálogo maestro: número de empleado, nombre, supervisor asignado, estatus activo (`SÍ`/`NO`) y los umbrales de horario descritos arriba. Solo los colaboradores marcados como activos aparecen en los tableros de supervisor.

Una hoja auxiliar de calendario (`NORMALIDAD`) documenta los días y meses usados por el archivo, aunque `REGISTRO` calcula esa información directamente con fórmulas.

## Tableros por supervisor

Cada supervisor tiene su propia hoja, con la misma estructura:

- Selector de periodo (mes) mediante lista desplegable.
- Lista automática de los colaboradores activos de ese supervisor.
- Conteos mensuales por estado (verde, amarillo, rojo, rojo fuerte, falta, y cada tipo de novedad).
- Totales, porcentaje verde y promedio de horas del periodo.
- Gráfica circular de distribución mensual.

Los conteos se calculan contra `REGISTRO`, filtrando por empleado, mes seleccionado y estado de semáforo. El porcentaje verde se calcula solo sobre los estados operativos; las novedades justificadas se muestran aparte para no mezclarlas con incumplimientos.

## Características principales

- Archivo 100% Excel, sin macros.
- Demo pública con datos y nombres completamente ficticios.
- Catálogo centralizado de personal.
- Clasificación automática por semáforo, con prioridad explícita entre novedad, falta y niveles de retardo.
- Reglas de horario propias por colaborador, diferenciadas entre semana y fin de semana.
- Excepciones autorizadas mediante lista desplegable.
- Indicador de revisión cuando un empleado no existe o su configuración no coincide.
- Cálculo automático de día, mes, tipo de día y horas (incluye turnos que cruzan la medianoche).
- Filtros y formato condicional sobre la base de asistencia.
- Tableros separados por supervisor, con selector mensual, totales, porcentaje verde y promedio de horas.
- Gráfica circular de distribución mensual por supervisor.

## Ejemplo de uso

| Captura | Resultado esperado |
| --- | --- |
| Entrada puntual | `VERDE` |
| Entrada después del umbral amarillo | `AMARILLO` |
| Entrada después del umbral rojo | `ROJO` |
| Entrada después del umbral rojo fuerte | `ROJO FUERTE` |
| Sin hora de entrada | `FALTA` |
| `NOVEDAD = VACACIONES` | `VACACIONES` |
| Número de empleado no existente | Indicador de revisión |

## Control de calidad

Antes de publicar este repositorio se hizo una revisión funcional y de privacidad sobre el archivo completo, no solo sobre esta documentación:

- Se verificó el comportamiento de la lógica de clasificación probando manualmente cada caso de la tabla de [Ejemplo de uso](#ejemplo-de-uso).
- Se revisaron las validaciones de datos y el formato condicional por estado.
- Se auditó la versión demo tanto a nivel de celdas como de elementos internos del archivo (gráficas, comentarios y propiedades del documento), para confirmar que no quedara ningún dato real embebido fuera de las hojas visibles.
- Se confirmó que el archivo con datos reales está excluido del control de versiones y nunca se ha subido al repositorio.

## Cómo adaptarlo

Para usarlo con otro equipo:

1. Reemplazar los colaboradores en `PERSONAL`.
2. Mantener el número de empleado como identificador único.
3. Asignar supervisor a cada colaborador y marcar su estatus activo.
4. Ajustar los umbrales de horario según el turno de cada quien.
5. Crear o duplicar tableros si se requieren más supervisores.
6. Cargar registros nuevos en `REGISTRO`.
7. Extender el rango de fórmulas y filtros conforme crece el volumen de registros.

## Requisitos

- Microsoft Excel de escritorio recomendado.
- Soporte para archivos `.xlsx`.
- Conocimiento básico de captura, filtros y listas desplegables.

No se necesita instalar nada adicional.

## Descargar o clonar

Descarga directa desde GitHub:

1. Abrir el repositorio.
2. Seleccionar `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx`.
3. Usar `Download` o `View raw`.
4. Abrir el archivo en Excel.

Clonar con Git:

```powershell
git clone https://github.com/Marco2004/semaforo-asistencia-excel-Excel-based-traffic-light-system-for-attendance-tracking.git
cd semaforo-asistencia-excel-Excel-based-traffic-light-system-for-attendance-tracking
```

## Privacidad

Este repositorio publica únicamente una versión de demostración con datos ficticios. El archivo con información real correspondiente a este sistema **no** forma parte de este repositorio ni de su historial: se excluye explícitamente del control de versiones y se conserva solo de forma local.

Antes de publicar la demo se reemplazaron nombres, números de empleado y supervisores por valores ficticios, y se revisó tanto el contenido de las celdas como los elementos internos del archivo (gráficas, comentarios y propiedades del documento) para confirmar que no quedara ningún dato real embebido.

Si adaptas este sistema con información real, no se recomienda publicar el archivo con datos internos, nombres reales, números de empleado reales ni registros reales de asistencia.

## Tecnologías y fórmulas usadas

- Microsoft Excel.
- Fórmulas `IF`, `IFERROR`, `INDEX`, `MATCH`, `COUNTIFS`, `AVERAGEIFS`, `SUM`, `WEEKDAY`, `MONTH` y `CHOOSE`.
- Fórmulas de matriz en columnas calculadas.
- Validaciones de datos.
- Filtros.
- Formato condicional.
- Gráficas circulares.

## Valor del proyecto

Este proyecto demuestra:

- Automatización de seguimiento operativo en Excel sin macros.
- Modelado de reglas de asistencia por colaborador y por tipo de día.
- Separación entre incidencias y excepciones justificadas.
- Construcción de tableros de supervisor con fórmulas encadenadas.
- Reducción de conteos manuales para revisión mensual.
- Un proceso de control de calidad y privacidad aplicado antes de publicar el archivo.

## Posibles mejoras futuras

- Agregar capturas de pantalla del workbook.
- Convertir la base de registros en una tabla formal de Excel.
- Agregar una hoja de instrucciones dentro del archivo.
- Crear un tablero consolidado general.
- Agregar una versión Power BI.
- Automatizar la carga de registros desde CSV o un sistema externo.

---

# English

## Project summary

This repository contains an attendance tracking system built in Microsoft Excel. The workbook records check-in and check-out data, classifies each record with a traffic-light status (`VERDE`/GREEN, `AMARILLO`/YELLOW, `ROJO`/RED, `ROJO FUERTE`/STRONG RED, `FALTA`/ABSENT, or an authorized exception), and summarizes results by supervisor, employee, and month — no macros or external tools required.

This project is part of my professional portfolio. The published version is a generic demonstration: it mirrors the same design and logic as a real system, but with entirely fictional data, names, and volume, meant only to illustrate how it works.

## Included file

- [`Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx`](Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx)

This is the only workbook published in this repository. It does not require macros, add-ins, or additional software: it works with Excel formulas, data validation, filters, conditional formatting, and charts.

## What problem it solves

In teams where attendance is tracked manually (a time clock, a logbook, or loose reports), reviewing punctuality and absenteeism month by month means counting records by hand for every employee and every supervisor. This workbook automates that count:

- Turns a flat list of check-ins and check-outs into an immediate color-coded status.
- Applies each employee's own schedule rules, different for weekdays versus weekends, without manual per-person formulas.
- Separates attendance issues (lateness, absences) from authorized exceptions (vacation, sick leave, permits, holidays), so justified absences aren't penalized.
- Gives each supervisor their own monthly dashboard with totals, compliance percentage, and average hours, ready for review without an analyst or an external system.

## Workbook structure

The workbook is organized into three kinds of sheets:

| Sheet type | Purpose |
| --- | --- |
| `REGISTRO` | Main attendance database. Date, employee, check-in, check-out, and exceptions are entered here. |
| `PERSONAL` | Employee catalog with supervisors, active status, and schedule classification rules. |
| `NORMALIDAD` | Helper calendar with weekdays and a month catalog. |
| Supervisor dashboards | One sheet per supervisor summarizing their team each month. The demo includes a few sample sheets with fictional names. |

## Workflow

1. Open the file in Microsoft Excel.
2. Review or update the catalog in `PERSONAL`.
3. Load daily records in `REGISTRO`.
4. Use the `NOVEDAD` column when a day has an authorized justification.
5. Select the month in the dropdown on each supervisor sheet.
6. Review counts, green percentage, records, average hours, and the chart.

> Note: because the workbook uses formulas, Excel recalculates results when it opens the file. GitHub's preview does not always render the workbook the way desktop Excel does; to see it with live formulas, download it and open it in Excel.

## Traffic-light logic

`REGISTRO` is the operational database, with frozen headers and a filter on the main range. Each row automatically calculates, from the date, employee, check-in, and check-out:

| Column | Description |
| --- | --- |
| `NOMBRE` / `SUPERVISOR` | Automatically retrieved from `PERSONAL` by looking up the employee number. |
| `DÍA` / `MES` / `TIPO DÍA` | Calculated from the date (weekday, month, and whether it's a weekday or a weekend). |
| `SEMÁFORO` | Final result of the classification rule. |
| `HORAS` | Hours between check-in and check-out, including shifts that cross midnight. |
| `NOVEDAD` | Dropdown list for recording authorized exceptions. |

The `SEMÁFORO` column follows this priority:

1. If date or employee number is missing, the result stays blank.
2. If `NOVEDAD` is filled in (vacation, sick leave, permit, holiday), that exception takes priority over the check-in time.
3. If there is no check-in time, the record is classified as `FALTA`.
4. If there is a check-in time, it's compared against that employee's configured thresholds, checking the most severe levels first (strong red → red → yellow → green).
5. If the employee doesn't exist or their configuration is invalid, the result is a review flag.

Each employee has their own set of thresholds (base time, yellow tolerance, red threshold, and strong-red threshold), defined separately for weekdays and weekends. This lets teams with different shifts coexist in the same file without duplicating sheets or formulas.

Conditional formatting colors the `SEMÁFORO` field by status: green, yellow, red, strong red, gray for absences, and purple for authorized exceptions.

## Employee catalog

`PERSONAL` is the master catalog: employee number, name, assigned supervisor, active status (yes/no), and the schedule thresholds described above. Only employees marked active appear on the supervisor dashboards.

A helper calendar sheet (`NORMALIDAD`) documents the days and months used by the file, although `REGISTRO` calculates that information directly with formulas.

## Supervisor dashboards

Each supervisor has their own sheet, sharing the same structure:

- A month selector via dropdown.
- An automatic list of that supervisor's active employees.
- Monthly counts by status (green, yellow, red, strong red, absent, and each exception type).
- Totals, green percentage, and average hours for the period.
- A monthly distribution pie chart.

Counts are calculated against `REGISTRO`, filtering by employee, selected month, and traffic-light status. The green percentage is calculated only over operational states; authorized exceptions are shown separately so they aren't mixed with attendance issues.

## Main features

- 100% Excel workbook, no macros.
- Public demo with entirely fictional data and names.
- Centralized employee catalog.
- Automatic traffic-light classification, with an explicit priority order between exception, absence, and lateness levels.
- Per-employee schedule rules, differentiated between weekdays and weekends.
- Authorized exceptions through a dropdown list.
- Review indicator when an employee does not exist or the configuration does not match.
- Automatic weekday, month, day type, and hours calculation (including overnight shifts).
- Filters and conditional formatting on the attendance database.
- Separate supervisor dashboards with a monthly selector, totals, green percentage, and average hours.
- Monthly distribution pie chart per supervisor.

## Usage example

| Input | Expected result |
| --- | --- |
| On-time check-in | `VERDE` |
| Check-in after yellow threshold | `AMARILLO` |
| Check-in after red threshold | `ROJO` |
| Check-in after strong red threshold | `ROJO FUERTE` |
| No check-in | `FALTA` |
| `NOVEDAD = VACACIONES` | `VACACIONES` |
| Non-existing employee number | Review indicator |

## Quality assurance

Before publishing this repository, the full workbook went through a functional and privacy review, not just this documentation:

- Verified the classification logic by manually testing each case in the [usage example](#usage-example) table.
- Reviewed data validation and conditional formatting per status.
- Audited the demo version at both the cell level and the level of the file's internal objects (charts, comments, and document properties), to confirm no real data remained embedded outside the visible sheets.
- Confirmed that the workbook with real data is excluded from version control and has never been uploaded to the repository.

## How to adapt it

To use it with another team:

1. Replace the employees in `PERSONAL`.
2. Keep the employee number as a unique identifier.
3. Assign a supervisor to each employee and mark their active status.
4. Adjust the schedule thresholds to match each person's shift.
5. Create or duplicate dashboards if more supervisors are needed.
6. Load new records in `REGISTRO`.
7. Extend the formula and filter ranges as the volume of records grows.

## Requirements

- Microsoft Excel desktop is recommended.
- Support for `.xlsx` files.
- Basic knowledge of data entry, filters, and dropdown lists.

No additional installation is required.

## Download or clone

Direct download from GitHub:

1. Open the repository.
2. Select `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx`.
3. Use `Download` or `View raw`.
4. Open the file in Excel.

Clone with Git:

```powershell
git clone https://github.com/Marco2004/semaforo-asistencia-excel-Excel-based-traffic-light-system-for-attendance-tracking.git
cd semaforo-asistencia-excel-Excel-based-traffic-light-system-for-attendance-tracking
```

## Privacy

This repository publishes only a demonstration version with fictional data. The workbook with real information for this system is **not** part of this repository or its history: it is explicitly excluded from version control and kept only locally.

Before publishing the demo, names, employee numbers, and supervisors were replaced with fictional values, and both cell contents and the file's internal objects (charts, comments, and document properties) were reviewed to confirm no real data remained embedded.

If you adapt this system with real information, it is not recommended to publish the file with internal data, real names, real employee numbers, or real attendance records.

## Technologies and formulas used

- Microsoft Excel.
- Formulas: `IF`, `IFERROR`, `INDEX`, `MATCH`, `COUNTIFS`, `AVERAGEIFS`, `SUM`, `WEEKDAY`, `MONTH`, and `CHOOSE`.
- Array formulas in calculated columns.
- Data validation.
- Filters.
- Conditional formatting.
- Pie charts.

## Project value

This project demonstrates:

- Operational tracking automation in Excel with no macros.
- Attendance rule modeling per employee and per day type.
- Separation between attendance issues and justified exceptions.
- Supervisor dashboard construction with chained formulas.
- Reduction of manual counting for monthly review.
- A quality-assurance and privacy process applied before publishing the file.

## Future improvements

- Add workbook screenshots.
- Convert the records database into a formal Excel table.
- Add an instruction sheet inside the workbook.
- Create a consolidated general dashboard.
- Add a Power BI version.
- Automate record loading from CSV or an external system.

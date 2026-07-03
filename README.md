# Sistema de Asistencia con Semaforo en Excel / Excel Attendance Traffic Light System

Este repositorio contiene un sistema de asistencia hecho en Microsoft Excel. El archivo registra entradas y salidas, clasifica cada registro con un semaforo operativo y resume resultados por supervisor, colaborador y mes.

This repository contains an attendance tracking system built in Microsoft Excel. The workbook records check-in and check-out data, classifies each record with a traffic-light status, and summarizes results by supervisor, employee, and month.

---

# Espanol

## Archivo incluido

- `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx`

Este es el libro principal del proyecto. No requiere macros, complementos ni software adicional. Funciona con formulas de Excel, validaciones, filtros, formato condicional y graficas.

La version publicada es una demo anonimizada. Los nombres, numeros de empleado, supervisores y registros son ficticios y se usan solo para demostrar el funcionamiento del sistema sin exponer informacion real.

## Que hace

El archivo convierte registros de asistencia en indicadores faciles de revisar:

- Relaciona cada numero de empleado con su nombre y supervisor.
- Calcula automaticamente dia de la semana, mes y tipo de dia.
- Clasifica cada entrada como `VERDE`, `AMARILLO`, `ROJO`, `ROJO FUERTE`, `FALTA` o una novedad autorizada.
- Permite registrar novedades como `VACACIONES`, `INCAPACIDAD`, `PERMISO` y `FESTIVO`.
- Maneja reglas de horario distintas para lunes-viernes y sabado-domingo.
- Resume resultados mensuales por supervisor y colaborador.
- Muestra totales, porcentaje verde, cantidad de registros, promedio de horas y grafica de distribucion mensual.

## Estructura del libro

El workbook tiene 6 hojas visibles:

| Hoja | Funcion |
| --- | --- |
| `REGISTRO` | Base principal de asistencia. Aqui se capturan fecha, empleado, entrada, salida y novedades. |
| `PERSONAL` | Catalogo de colaboradores, supervisores, estatus activo y reglas de clasificacion por horario. |
| `NORMALIDAD` | Calendario auxiliar 2026 con dias de la semana y catalogo de meses. |
| `ALEJANDRO TORRES LUNA` | Tablero mensual del equipo de ese supervisor. |
| `CAMILA RIVERA NAVA` | Tablero mensual del equipo de ese supervisor. |
| `MATEO HERRERA SOLIS` | Tablero mensual del equipo de ese supervisor. |

## Flujo de trabajo

1. Abrir `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx` en Microsoft Excel.
2. Revisar o actualizar el catalogo en `PERSONAL`.
3. Cargar registros diarios en `REGISTRO`.
4. Usar `NOVEDAD` cuando un dia tenga justificacion autorizada.
5. Elegir el mes en cada hoja de supervisor.
6. Revisar conteos, porcentaje verde, registros, promedio de horas y grafica.

> Nota: como el archivo usa formulas, Excel puede recalcular resultados al abrirlo. La vista previa de GitHub no siempre muestra el workbook igual que Excel de escritorio.

## Hoja `REGISTRO`

`REGISTRO` es la base de datos operativa. Tiene encabezados congelados, filtro sobre el rango principal y formulas preparadas hasta la fila 1722.

Columnas:

| Columna | Descripcion |
| --- | --- |
| `FECHA` | Fecha del registro de asistencia. |
| `No. EMP` | Numero de empleado ficticio; funciona como llave contra `PERSONAL`. |
| `ENTRADA` | Hora de entrada usada para clasificar el semaforo. |
| `SALIDA` | Hora de salida usada para calcular horas trabajadas. |
| `NOMBRE` | Se obtiene automaticamente desde `PERSONAL` con `INDEX` + `MATCH`. |
| `SUPERVISOR` | Se obtiene automaticamente desde `PERSONAL` con `INDEX` + `MATCH`. |
| `DIA` | Dia de la semana calculado con `WEEKDAY` y `CHOOSE`. |
| `MES` | Mes calculado con `MONTH` y `CHOOSE`. |
| `TIPO DIA` | Clasifica el dia como `LV` o `FIN`. |
| `SEMAFORO` | Resultado final de la regla de clasificacion. |
| `HORAS` | Horas entre entrada y salida; contempla salidas despues de medianoche. |
| `NOVEDAD` | Lista desplegable para `VACACIONES`, `INCAPACIDAD`, `PERMISO` o `FESTIVO`. |

## Regla de clasificacion del semaforo

La columna `SEMAFORO` sigue esta prioridad:

1. Si falta fecha o numero de empleado, deja el resultado vacio.
2. Si existe una `NOVEDAD`, usa esa novedad en mayusculas como clasificacion final.
3. Si no hay hora de entrada, clasifica como `FALTA`.
4. Si hay entrada, compara la hora contra las reglas del empleado en `PERSONAL`.
5. Si no encuentra datos validos del empleado, devuelve `REVISAR`.

La comparacion cambia segun `TIPO DIA`:

| Tipo de dia | Reglas usadas |
| --- | --- |
| `LV` | Usa `VERDE L-V`, `AMARILLO L-V`, `ROJO L-V` y `ROJO FUERTE L-V`. |
| `FIN` | Usa `VERDE S-D`, `AMARILLO S-D`, `ROJO S-D` y `ROJO FUERTE S-D`. |

La regla evalua primero los niveles mas severos:

| Resultado | Logica general |
| --- | --- |
| `VERDE` | Entrada dentro del rango esperado. |
| `AMARILLO` | Entrada igual o posterior al umbral amarillo. |
| `ROJO` | Entrada igual o posterior al umbral rojo. |
| `ROJO FUERTE` | Entrada igual o posterior al umbral mas severo. |
| `FALTA` | No hay hora de entrada y no existe novedad. |
| `REVISAR` | El empleado o sus reglas no se encontraron correctamente. |

El formato condicional pinta el campo `SEMAFORO` por estado: verde, amarillo, rojo, rojo fuerte, gris para faltas y morado para novedades.

## Hoja `PERSONAL`

`PERSONAL` es el catalogo maestro. En la demo contiene 19 colaboradores activos distribuidos en 3 supervisores.

Columnas:

| Columna | Descripcion |
| --- | --- |
| `No. EMP` | Identificador unico del colaborador. |
| `NOMBRE` | Nombre ficticio del colaborador. |
| `SUPERVISOR` | Supervisor asignado. |
| `ACTIVO` | Lista desplegable con `SI` / `NO`. Solo los activos entran en tableros. |
| `VERDE L-V` | Hora base esperada de lunes a viernes. |
| `AMARILLO L-V` | Umbral de alerta amarilla de lunes a viernes. |
| `ROJO L-V` | Umbral rojo de lunes a viernes. |
| `ROJO FUERTE L-V` | Umbral rojo fuerte de lunes a viernes. |
| `VERDE S-D` | Hora base esperada para sabado y domingo. |
| `AMARILLO S-D` | Umbral amarillo para sabado y domingo. |
| `ROJO S-D` | Umbral rojo para sabado y domingo. |
| `ROJO FUERTE S-D` | Umbral rojo fuerte para sabado y domingo. |
| `IDX SUP` | Indice incremental por supervisor para listar asesores activos. |
| `LLAVE` | Llave `SUPERVISOR|IDX` usada por los tableros. |

## Reglas de horario incluidas

La demo muestra distintos horarios de entrada para probar escenarios reales:

- Turnos de 08:00, 09:00, 11:00, 13:00, 13:30 y 14:00 entre semana.
- Reglas separadas para fines de semana.
- Escalones de clasificacion por minuto: base, amarillo, rojo y rojo fuerte.

Esto permite adaptar el archivo a equipos con diferentes horarios sin duplicar hojas ni formulas principales.

## Hoja `NORMALIDAD`

`NORMALIDAD` funciona como apoyo de calendario.

Incluye:

- Fechas de 2026.
- Dia de la semana correspondiente.
- Catalogo de meses de enero a diciembre.

Aunque `REGISTRO` calcula dia y mes con formulas directas, esta hoja ayuda a documentar y validar la normalidad del calendario usado por el archivo.

## Tableros por supervisor

Las hojas de supervisor tienen la misma estructura:

- Nombre del supervisor.
- Selector de periodo en `C5` con lista de meses.
- Lista automatica de asesores activos del supervisor.
- Conteos mensuales por estado.
- Totales por clasificacion.
- Porcentaje verde.
- Total de registros y promedio de horas.
- Grafica circular de distribucion mensual.

Columnas principales del tablero:

| Columna | Indicador |
| --- | --- |
| `No. EMP` | Colaborador listado automaticamente desde `PERSONAL`. |
| `NOMBRE` | Nombre relacionado con el numero de empleado. |
| `VERDE` | Conteo mensual de registros verdes. |
| `AMARILLO` | Conteo mensual de alertas amarillas. |
| `ROJO` | Conteo mensual de alertas rojas. |
| `ROJO FUERTE` | Conteo mensual de alertas severas. |
| `FALTA` | Conteo mensual de faltas. |
| `VACACIONES` | Conteo mensual de vacaciones. |
| `FESTIVO` | Conteo mensual de festivos. |
| `INCAPACIDAD` | Conteo mensual de incapacidades. |
| `PERMISO` | Conteo mensual de permisos. |

Los conteos usan `COUNTIFS` contra `REGISTRO`, filtrando por numero de empleado, mes seleccionado y estado de semaforo.

El porcentaje verde se calcula sobre los estados operativos `VERDE`, `AMARILLO`, `ROJO`, `ROJO FUERTE` y `FALTA`. Las novedades justificadas se muestran aparte para no mezclarlas con incumplimientos.

## Caracteristicas principales

- Archivo 100% Excel, sin macros.
- Demo publica con datos ficticios.
- Catalogo centralizado de personal.
- Clasificacion automatica por semaforo.
- Reglas diferenciadas para lunes-viernes y fines de semana.
- Soporte para multiples horarios por colaborador.
- Excepciones autorizadas mediante lista desplegable.
- Indicador `REVISAR` cuando un empleado no existe o su configuracion no coincide.
- Calculo automatico de dia, mes, tipo de dia y horas.
- Rango preparado para mas de 1700 registros.
- Filtros en la base de asistencia.
- Formato condicional por estado.
- Tableros separados por supervisor.
- Selector mensual en cada tablero.
- Totales mensuales por clasificacion.
- Porcentaje verde por supervisor.
- Promedio de horas del periodo.
- Grafica circular de distribucion mensual.

## Ejemplo de uso

| Captura | Resultado esperado |
| --- | --- |
| Fecha + empleado + entrada puntual | `VERDE` |
| Fecha + empleado + entrada despues del umbral amarillo | `AMARILLO` |
| Fecha + empleado + entrada despues del umbral rojo | `ROJO` |
| Fecha + empleado + entrada despues del umbral rojo fuerte | `ROJO FUERTE` |
| Fecha + empleado sin entrada | `FALTA` |
| Fecha + empleado + `NOVEDAD = VACACIONES` | `VACACIONES` |
| Numero de empleado no existente | `REVISAR` o `NO EXISTE` segun la columna calculada |

## Como adaptarlo

Para usarlo con otro equipo:

1. Reemplazar los colaboradores ficticios en `PERSONAL`.
2. Mantener `No. EMP` como identificador unico.
3. Asignar supervisor a cada colaborador.
4. Marcar `ACTIVO` segun corresponda.
5. Ajustar los umbrales de horario L-V y S-D.
6. Crear o duplicar tableros si se requieren mas supervisores.
7. Cargar registros nuevos en `REGISTRO`.
8. Revisar que las formulas se mantengan hasta el rango necesario.

## Requisitos

- Microsoft Excel de escritorio recomendado.
- Soporte para archivos `.xlsx`.
- Conocimiento basico de captura, filtros y listas desplegables.

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

Esta version no contiene informacion real.

Antes de publicarse:

- Se reemplazaron nombres de colaboradores.
- Se reemplazaron numeros de empleado.
- Se reemplazaron supervisores.
- Se dejaron registros ficticios solo para demostrar el funcionamiento.

Si se adapta a datos reales, no se recomienda publicar el archivo con informacion interna, nombres reales, numeros de empleado reales ni registros reales de asistencia.

## Tecnologias y formulas usadas

- Microsoft Excel.
- Formulas `IF`, `IFERROR`, `INDEX`, `MATCH`, `COUNTIFS`, `AVERAGEIFS`, `SUM`, `WEEKDAY`, `MONTH` y `CHOOSE`.
- Formulas de matriz en columnas calculadas.
- Validaciones de datos.
- Filtros.
- Formato condicional.
- Graficas circulares.

## Valor del proyecto

Este proyecto demuestra:

- Automatizacion de seguimiento operativo en Excel.
- Modelado de reglas de asistencia por colaborador.
- Separacion entre incidencias y excepciones justificadas.
- Construccion de tableros de supervisor sin macros.
- Reduccion de conteos manuales.
- Presentacion clara de informacion para revision mensual.

## Posibles mejoras futuras

- Agregar capturas de pantalla del workbook.
- Convertir la base `REGISTRO` y `PERSONAL` en tablas formales de Excel.
- Agregar una hoja de instrucciones dentro del archivo.
- Crear un tablero consolidado general.
- Agregar una version Power BI.
- Automatizar carga de registros desde CSV o sistema externo.

---

# English

## Included file

- `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx`

This is the main workbook for the project. It does not require macros, add-ins, or additional software. It works with Excel formulas, data validation, filters, conditional formatting, and charts.

The published version is an anonymized demo. Employee names, employee numbers, supervisors, and records are fictional and are included only to demonstrate how the system works without exposing real information.

## What it does

The workbook turns attendance records into indicators that are easy to review:

- Links each employee number to the employee name and supervisor.
- Automatically calculates weekday, month, and day type.
- Classifies each check-in as `VERDE`, `AMARILLO`, `ROJO`, `ROJO FUERTE`, `FALTA`, or an authorized exception.
- Supports exceptions such as `VACACIONES`, `INCAPACIDAD`, `PERMISO`, and `FESTIVO`.
- Uses different schedule rules for Monday-Friday and Saturday-Sunday.
- Summarizes monthly results by supervisor and employee.
- Shows totals, green percentage, record count, average hours, and a monthly distribution chart.

## Workbook structure

The workbook has 6 visible sheets:

| Sheet | Purpose |
| --- | --- |
| `REGISTRO` | Main attendance database. Date, employee, check-in, check-out, and exceptions are entered here. |
| `PERSONAL` | Employee catalog with supervisors, active status, and schedule classification rules. |
| `NORMALIDAD` | 2026 helper calendar with weekdays and month catalog. |
| `ALEJANDRO TORRES LUNA` | Monthly dashboard for that supervisor's team. |
| `CAMILA RIVERA NAVA` | Monthly dashboard for that supervisor's team. |
| `MATEO HERRERA SOLIS` | Monthly dashboard for that supervisor's team. |

## Workflow

1. Open `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx` in Microsoft Excel.
2. Review or update the catalog in `PERSONAL`.
3. Load daily records in `REGISTRO`.
4. Use `NOVEDAD` when a day has an authorized justification.
5. Select the month in each supervisor dashboard.
6. Review counts, green percentage, records, average hours, and chart.

> Note: because the workbook uses formulas, Excel may recalculate results when opening the file. GitHub preview may not display the workbook exactly like desktop Excel.

## `REGISTRO` sheet

`REGISTRO` is the operational database. It has frozen headers, a filter on the main range, and formulas prepared down to row 1722.

Columns:

| Column | Description |
| --- | --- |
| `FECHA` | Attendance record date. |
| `No. EMP` | Fictional employee number; used as the key against `PERSONAL`. |
| `ENTRADA` | Check-in time used to classify the traffic-light status. |
| `SALIDA` | Check-out time used to calculate worked hours. |
| `NOMBRE` | Automatically retrieved from `PERSONAL` with `INDEX` + `MATCH`. |
| `SUPERVISOR` | Automatically retrieved from `PERSONAL` with `INDEX` + `MATCH`. |
| `DIA` | Weekday calculated with `WEEKDAY` and `CHOOSE`. |
| `MES` | Month calculated with `MONTH` and `CHOOSE`. |
| `TIPO DIA` | Classifies the day as `LV` or `FIN`. |
| `SEMAFORO` | Final result of the classification rule. |
| `HORAS` | Hours between check-in and check-out; supports overnight exits. |
| `NOVEDAD` | Dropdown list for `VACACIONES`, `INCAPACIDAD`, `PERMISO`, or `FESTIVO`. |

## Traffic-light classification rule

The `SEMAFORO` column follows this priority:

1. If date or employee number is missing, the result stays blank.
2. If `NOVEDAD` is filled in, that exception is used as the final classification.
3. If there is no check-in time, the record is classified as `FALTA`.
4. If there is a check-in time, it is compared against the employee's rules in `PERSONAL`.
5. If valid employee data is not found, the result is `REVISAR`.

The comparison changes depending on `TIPO DIA`:

| Day type | Rules used |
| --- | --- |
| `LV` | Uses `VERDE L-V`, `AMARILLO L-V`, `ROJO L-V`, and `ROJO FUERTE L-V`. |
| `FIN` | Uses `VERDE S-D`, `AMARILLO S-D`, `ROJO S-D`, and `ROJO FUERTE S-D`. |

The rule evaluates the most severe levels first:

| Result | General logic |
| --- | --- |
| `VERDE` | Check-in is within the expected range. |
| `AMARILLO` | Check-in is equal to or later than the yellow threshold. |
| `ROJO` | Check-in is equal to or later than the red threshold. |
| `ROJO FUERTE` | Check-in is equal to or later than the most severe threshold. |
| `FALTA` | There is no check-in time and no exception. |
| `REVISAR` | Employee or rule data was not found correctly. |

Conditional formatting colors the `SEMAFORO` field by status: green, yellow, red, strong red, gray for absences, and purple for exceptions.

## `PERSONAL` sheet

`PERSONAL` is the master catalog. The demo includes 19 active employees distributed across 3 supervisors.

Columns:

| Column | Description |
| --- | --- |
| `No. EMP` | Unique employee identifier. |
| `NOMBRE` | Fictional employee name. |
| `SUPERVISOR` | Assigned supervisor. |
| `ACTIVO` | Dropdown list with `SI` / `NO`. Only active employees appear in dashboards. |
| `VERDE L-V` | Expected base time for Monday-Friday. |
| `AMARILLO L-V` | Yellow alert threshold for Monday-Friday. |
| `ROJO L-V` | Red threshold for Monday-Friday. |
| `ROJO FUERTE L-V` | Strong red threshold for Monday-Friday. |
| `VERDE S-D` | Expected base time for Saturday-Sunday. |
| `AMARILLO S-D` | Yellow threshold for Saturday-Sunday. |
| `ROJO S-D` | Red threshold for Saturday-Sunday. |
| `ROJO FUERTE S-D` | Strong red threshold for Saturday-Sunday. |
| `IDX SUP` | Incremental index by supervisor used to list active advisors. |
| `LLAVE` | `SUPERVISOR|IDX` key used by dashboards. |

## Included schedule rules

The demo includes different check-in schedules to represent real scenarios:

- Weekday shifts at 08:00, 09:00, 11:00, 13:00, 13:30, and 14:00.
- Separate weekend rules.
- Classification steps by minute: base, yellow, red, and strong red.

This allows the workbook to adapt to teams with different schedules without duplicating the main sheets or formulas.

## `NORMALIDAD` sheet

`NORMALIDAD` works as a helper calendar.

It includes:

- 2026 dates.
- Matching weekday.
- Month catalog from January to December.

Although `REGISTRO` calculates weekday and month with direct formulas, this sheet helps document and validate the calendar used by the workbook.

## Supervisor dashboards

Supervisor sheets share the same structure:

- Supervisor name.
- Period selector in `C5` with a month dropdown.
- Automatic list of active advisors for the supervisor.
- Monthly counts by status.
- Totals by classification.
- Green percentage.
- Total records and average hours.
- Monthly distribution pie chart.

Main dashboard columns:

| Column | Indicator |
| --- | --- |
| `No. EMP` | Employee listed automatically from `PERSONAL`. |
| `NOMBRE` | Name linked to the employee number. |
| `VERDE` | Monthly count of green records. |
| `AMARILLO` | Monthly count of yellow alerts. |
| `ROJO` | Monthly count of red alerts. |
| `ROJO FUERTE` | Monthly count of severe red alerts. |
| `FALTA` | Monthly count of absences. |
| `VACACIONES` | Monthly count of vacation days. |
| `FESTIVO` | Monthly count of holidays. |
| `INCAPACIDAD` | Monthly count of sick leave records. |
| `PERMISO` | Monthly count of authorized leave records. |

Counts use `COUNTIFS` against `REGISTRO`, filtering by employee number, selected month, and traffic-light status.

The green percentage is calculated over operational states: `VERDE`, `AMARILLO`, `ROJO`, `ROJO FUERTE`, and `FALTA`. Authorized exceptions are shown separately so they are not mixed with attendance issues.

## Main features

- 100% Excel workbook, no macros.
- Public demo with fictional data.
- Centralized employee catalog.
- Automatic traffic-light classification.
- Separate Monday-Friday and weekend rules.
- Support for multiple employee schedules.
- Authorized exceptions through a dropdown list.
- `REVISAR` indicator when an employee does not exist or the configuration does not match.
- Automatic weekday, month, day type, and hours calculation.
- Range prepared for more than 1700 records.
- Filters in the attendance database.
- Conditional formatting by status.
- Separate supervisor dashboards.
- Monthly selector in each dashboard.
- Monthly totals by classification.
- Green percentage by supervisor.
- Average hours for the period.
- Monthly distribution pie chart.

## Usage example

| Input | Expected result |
| --- | --- |
| Date + employee + on-time check-in | `VERDE` |
| Date + employee + check-in after yellow threshold | `AMARILLO` |
| Date + employee + check-in after red threshold | `ROJO` |
| Date + employee + check-in after strong red threshold | `ROJO FUERTE` |
| Date + employee without check-in | `FALTA` |
| Date + employee + `NOVEDAD = VACACIONES` | `VACACIONES` |
| Non-existing employee number | `REVISAR` or `NO EXISTE`, depending on the calculated column |

## How to adapt it

To use it with another team:

1. Replace the fictional employees in `PERSONAL`.
2. Keep `No. EMP` as a unique identifier.
3. Assign a supervisor to each employee.
4. Mark `ACTIVO` as needed.
5. Adjust the L-V and S-D schedule thresholds.
6. Create or duplicate dashboards if more supervisors are needed.
7. Load new records in `REGISTRO`.
8. Confirm that formulas cover the required range.

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

This version does not contain real information.

Before publishing:

- Employee names were replaced.
- Employee numbers were replaced.
- Supervisors were replaced.
- Fictional records were kept only to demonstrate how the workbook works.

If the workbook is adapted to real data, it is not recommended to publish internal information, real names, real employee numbers, or real attendance records.

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

- Operational tracking automation in Excel.
- Attendance rule modeling per employee.
- Separation between attendance issues and justified exceptions.
- Supervisor dashboard creation without macros.
- Reduction of manual counting.
- Clear presentation of information for monthly review.

## Future improvements

- Add workbook screenshots.
- Convert `REGISTRO` and `PERSONAL` into formal Excel tables.
- Add an instruction sheet inside the workbook.
- Create a consolidated general dashboard.
- Add a Power BI version.
- Automate record loading from CSV or an external system.

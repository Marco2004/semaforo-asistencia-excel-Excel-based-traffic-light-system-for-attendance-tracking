# Sistema de Asistencia con Semaforo en Excel

Excel-based traffic-light system for attendance tracking.

## Espanol

Sistema en Microsoft Excel para registrar asistencia, clasificar entradas con un semaforo operativo y resumir resultados por supervisor, colaborador y mes.

Este repositorio publica una version demo anonimizada. Los nombres, numeros de empleado, supervisores y registros incluidos son ficticios y se usan solo para demostrar el funcionamiento del archivo sin exponer informacion real.

## English

Microsoft Excel system for recording attendance, classifying check-ins with a traffic-light status, and summarizing results by supervisor, employee, and month.

This repository publishes an anonymized demo version. Employee names, employee numbers, supervisors, and records are fictional and are included only to demonstrate the workbook without exposing real information.

---

## Archivo principal / Main file

- `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx`

No requiere macros, complementos ni software adicional. Funciona con formulas de Excel, validaciones, filtros, formato condicional y graficas.

It does not require macros, add-ins, or additional software. It works with Excel formulas, data validation, filters, conditional formatting, and charts.

## Documentacion / Documentation

| Archivo | Proposito |
| --- | --- |
| `README.md` | Presentacion general, uso rapido y estructura del workbook. |
| `SECURITY.md` | Politica de seguridad, privacidad de datos y reporte responsable. |
| `LICENSE` | Licencia del proyecto. |

| File | Purpose |
| --- | --- |
| `README.md` | General overview, quick usage, and workbook structure. |
| `SECURITY.md` | Security policy, data privacy, and responsible reporting. |
| `LICENSE` | Project license. |

## Que hace / What it does

- Relaciona cada numero de empleado con su nombre y supervisor.
- Calcula dia de la semana, mes y tipo de dia.
- Clasifica cada entrada como `VERDE`, `AMARILLO`, `ROJO`, `ROJO FUERTE`, `FALTA` o una novedad autorizada.
- Permite marcar excepciones: `VACACIONES`, `INCAPACIDAD`, `PERMISO` y `FESTIVO`.
- Maneja reglas de horario separadas para lunes-viernes y fines de semana.
- Resume resultados mensuales por supervisor y colaborador.
- Muestra totales, porcentaje verde, registros, promedio de horas y grafica de distribucion mensual.

English:

- Links each employee number with its name and supervisor.
- Calculates weekday, month, and day type.
- Classifies each check-in as `VERDE`, `AMARILLO`, `ROJO`, `ROJO FUERTE`, `FALTA`, or an authorized exception.
- Supports exceptions: `VACACIONES`, `INCAPACIDAD`, `PERMISO`, and `FESTIVO`.
- Uses separate schedule rules for Monday-Friday and weekends.
- Summarizes monthly results by supervisor and employee.
- Shows totals, green percentage, records, average hours, and a monthly distribution chart.

## Estructura del workbook / Workbook structure

| Hoja / Sheet | Funcion / Purpose |
| --- | --- |
| `REGISTRO` | Base principal de asistencia. Main attendance database. |
| `PERSONAL` | Catalogo de colaboradores, supervisores y reglas de horario. Employee catalog, supervisors, and schedule rules. |
| `NORMALIDAD` | Calendario auxiliar 2026. 2026 helper calendar. |
| `ALEJANDRO TORRES LUNA` | Tablero mensual por supervisor. Monthly supervisor dashboard. |
| `CAMILA RIVERA NAVA` | Tablero mensual por supervisor. Monthly supervisor dashboard. |
| `MATEO HERRERA SOLIS` | Tablero mensual por supervisor. Monthly supervisor dashboard. |

## Flujo de uso / Usage flow

1. Abrir `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx` en Microsoft Excel.
2. Revisar o actualizar el catalogo en `PERSONAL`.
3. Cargar registros diarios en `REGISTRO`.
4. Usar `NOVEDAD` cuando exista una justificacion autorizada.
5. Elegir el mes en cada tablero de supervisor.
6. Revisar conteos, porcentaje verde, registros, promedio de horas y grafica.

English:

1. Open `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx` in Microsoft Excel.
2. Review or update the catalog in `PERSONAL`.
3. Load daily records in `REGISTRO`.
4. Use `NOVEDAD` when an authorized justification exists.
5. Select the month in each supervisor dashboard.
6. Review counts, green percentage, records, average hours, and chart.

## Logica de clasificacion / Classification logic

La columna `SEMAFORO` sigue esta prioridad:

1. Si falta fecha o numero de empleado, deja el resultado vacio.
2. Si existe una `NOVEDAD`, usa esa novedad como clasificacion final.
3. Si no hay hora de entrada, clasifica como `FALTA`.
4. Si hay entrada, compara la hora contra las reglas del colaborador en `PERSONAL`.
5. Si el colaborador o sus reglas no se encuentran, devuelve `REVISAR`.

English:

1. If date or employee number is missing, the result stays blank.
2. If `NOVEDAD` is filled in, that exception becomes the final classification.
3. If there is no check-in time, the record is classified as `FALTA`.
4. If there is a check-in time, it is compared against the employee rules in `PERSONAL`.
5. If employee data or rules are not found, the result is `REVISAR`.

## Columnas principales / Main columns

### `REGISTRO`

| Columna / Column | Descripcion / Description |
| --- | --- |
| `FECHA` | Fecha del registro. Attendance record date. |
| `No. EMP` | Identificador del colaborador. Employee identifier. |
| `ENTRADA` | Hora de entrada. Check-in time. |
| `SALIDA` | Hora de salida. Check-out time. |
| `NOMBRE` | Nombre obtenido desde `PERSONAL`. Name retrieved from `PERSONAL`. |
| `SUPERVISOR` | Supervisor obtenido desde `PERSONAL`. Supervisor retrieved from `PERSONAL`. |
| `DIA` | Dia de la semana. Weekday. |
| `MES` | Mes calculado. Calculated month. |
| `TIPO DIA` | `LV` o `FIN`. `LV` or `FIN`. |
| `SEMAFORO` | Clasificacion final. Final classification. |
| `HORAS` | Horas entre entrada y salida. Hours between check-in and check-out. |
| `NOVEDAD` | Excepcion autorizada. Authorized exception. |

### `PERSONAL`

| Columna / Column | Descripcion / Description |
| --- | --- |
| `No. EMP` | Identificador unico. Unique identifier. |
| `NOMBRE` | Nombre ficticio. Fictional name. |
| `SUPERVISOR` | Supervisor asignado. Assigned supervisor. |
| `ACTIVO` | `SI` / `NO`. |
| `VERDE L-V` | Hora base lunes-viernes. Monday-Friday base time. |
| `AMARILLO L-V` | Umbral amarillo lunes-viernes. Monday-Friday yellow threshold. |
| `ROJO L-V` | Umbral rojo lunes-viernes. Monday-Friday red threshold. |
| `ROJO FUERTE L-V` | Umbral severo lunes-viernes. Monday-Friday strong red threshold. |
| `VERDE S-D` | Hora base fin de semana. Weekend base time. |
| `AMARILLO S-D` | Umbral amarillo fin de semana. Weekend yellow threshold. |
| `ROJO S-D` | Umbral rojo fin de semana. Weekend red threshold. |
| `ROJO FUERTE S-D` | Umbral severo fin de semana. Weekend strong red threshold. |
| `IDX SUP` | Indice por supervisor. Supervisor index. |
| `LLAVE` | Llave para tableros. Dashboard key. |

## Tableros / Dashboards

Cada hoja de supervisor incluye:

- Selector de mes.
- Lista automatica de colaboradores activos.
- Conteos por `VERDE`, `AMARILLO`, `ROJO`, `ROJO FUERTE`, `FALTA`, `VACACIONES`, `FESTIVO`, `INCAPACIDAD` y `PERMISO`.
- Totales mensuales.
- Porcentaje verde.
- Total de registros y promedio de horas.
- Grafica circular de distribucion mensual.

English:

- Month selector.
- Automatic list of active employees.
- Counts by `VERDE`, `AMARILLO`, `ROJO`, `ROJO FUERTE`, `FALTA`, `VACACIONES`, `FESTIVO`, `INCAPACIDAD`, and `PERMISO`.
- Monthly totals.
- Green percentage.
- Total records and average hours.
- Monthly distribution pie chart.

## Tecnologias / Technologies

- Microsoft Excel.
- Formulas: `IF`, `IFERROR`, `INDEX`, `MATCH`, `COUNTIFS`, `AVERAGEIFS`, `SUM`, `WEEKDAY`, `MONTH`, `CHOOSE`.
- Validaciones de datos / Data validation.
- Filtros / Filters.
- Formato condicional / Conditional formatting.
- Graficas circulares / Pie charts.

## Privacidad / Privacy

Este repositorio no contiene datos reales. Para detalles sobre manejo de datos, uso seguro y reporte de problemas, consulta `SECURITY.md`.

This repository does not contain real data. For details about data handling, safe usage, and reporting issues, see `SECURITY.md`.

## Licencia / License

Este proyecto esta publicado bajo la licencia incluida en `LICENSE`.

This project is published under the license included in `LICENSE`.

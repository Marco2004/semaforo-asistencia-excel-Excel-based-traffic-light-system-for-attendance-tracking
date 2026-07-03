# Sistema de Asistencia con Semaforo en Excel

Sistema en Microsoft Excel para revisar asistencia, retardos, faltas, excepciones y cumplimiento de horarios mediante una clasificacion visual tipo semaforo.

Este repositorio contiene una version demo anonimizada. Todos los nombres, numeros de empleado, supervisores y registros incluidos son ficticios y se usan solo para mostrar el funcionamiento del archivo.

## Contenido

- [Descripcion](#descripcion)
- [Archivo incluido](#archivo-incluido)
- [Requisitos](#requisitos)
- [Instalacion y descarga](#instalacion-y-descarga)
- [Como usar el archivo](#como-usar-el-archivo)
- [Estructura del libro](#estructura-del-libro)
- [Ejemplo de flujo de trabajo](#ejemplo-de-flujo-de-trabajo)
- [Clasificacion del semaforo](#clasificacion-del-semaforo)
- [Datos ficticios y privacidad](#datos-ficticios-y-privacidad)
- [Valor del proyecto](#valor-del-proyecto)
- [English version](#excel-attendance-traffic-light-system)

## Descripcion

El archivo ayuda a convertir registros de entrada y salida en indicadores faciles de revisar. En lugar de contar manualmente retardos, faltas o excepciones, el sistema clasifica cada registro y resume los resultados por supervisor, colaborador y periodo.

La idea principal es tener una herramienta sencilla para seguimiento operativo:

- Capturar o pegar registros de asistencia.
- Clasificar automaticamente cada dia con un estado de semaforo.
- Marcar excepciones como vacaciones, incapacidad, permiso o festivo.
- Consultar resultados resumidos por supervisor.
- Ver metricas mensuales por colaborador.

## Archivo incluido

- `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx`

Este es el archivo que debe abrirse para probar el sistema. Es una copia publica y anonimizada del proyecto.

## Requisitos

Para usar el archivo se recomienda:

- Microsoft Excel de escritorio.
- Windows o macOS con soporte para archivos `.xlsx`.
- Conocimiento basico de Excel: abrir hojas, editar celdas y filtrar tablas.

No requiere instalacion de macros, complementos ni software adicional.

## Instalacion y descarga

### Opcion 1: Descargar desde GitHub

1. Entrar al repositorio en GitHub.
2. Dar clic en el archivo `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx`.
3. Usar el boton `Download` o `View raw` para descargarlo.
4. Abrir el archivo en Microsoft Excel.
5. Si Excel muestra una advertencia de archivo descargado de internet, habilitar la edicion solo si confias en la fuente del repositorio.

### Opcion 2: Clonar el repositorio

Si usas Git, puedes clonar el proyecto:

```powershell
git clone https://github.com/TU_USUARIO/semaforo-asistencia-excel.git
cd semaforo-asistencia-excel
```

Despues abre el archivo:

```text
Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx
```

## Como usar el archivo

### 1. Abrir el archivo

Abre `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx` en Excel.

El libro contiene hojas de registro, catalogo de personal, calendario auxiliar y reportes por supervisor.

### 2. Revisar el catalogo de personal

Ve a la hoja `PERSONAL`.

Esta hoja contiene el listado de colaboradores demo, su numero de empleado, supervisor asignado, estado activo y reglas usadas para clasificar los registros.

Ejemplo ficticio:

| No. EMP | NOMBRE | SUPERVISOR | ACTIVO |
| --- | --- | --- | --- |
| 7001 | SOFIA MORALES VEGA | CAMILA RIVERA NAVA | SI |
| 7002 | DIEGO RAMIREZ PENA | CAMILA RIVERA NAVA | SI |
| 7003 | VALERIA CASTILLO ROJAS | MATEO HERRERA SOLIS | SI |

Uso recomendado:

- Agregar colaboradores nuevos en esta hoja si se quiere adaptar el archivo.
- Mantener el numero de empleado como identificador unico.
- Revisar que el supervisor coincida con la hoja de resumen correspondiente.
- Marcar como activo solo al personal que se desea incluir en los reportes.

### 3. Revisar o capturar registros de asistencia

Ve a la hoja `REGISTRO`.

Esta hoja funciona como base principal de datos. Cada fila representa un registro de asistencia de un colaborador en una fecha.

Ejemplo ficticio:

| FECHA | No. EMP | ENTRADA | SALIDA | NOMBRE | SUPERVISOR | SEMAFORO | NOVEDAD |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 01/06/2026 | 7001 | 08:00 | 17:00 | SOFIA MORALES VEGA | CAMILA RIVERA NAVA | VERDE | |
| 01/06/2026 | 7002 | 08:12 | 17:00 | DIEGO RAMIREZ PENA | CAMILA RIVERA NAVA | AMARILLO | |
| 02/06/2026 | 7003 | - | - | VALERIA CASTILLO ROJAS | MATEO HERRERA SOLIS | FALTA | |
| 03/06/2026 | 7004 | - | - | MARIANA LOPEZ SANTOS | ALEJANDRO TORRES LUNA | VACACIONES | VACACIONES |

Uso recomendado:

- Capturar la fecha del registro.
- Capturar o pegar el numero de empleado.
- Capturar entrada y salida cuando existan.
- Usar la columna `NOVEDAD` cuando el dia tenga una excepcion.
- Evitar escribir manualmente sobre formulas si el archivo ya calcula campos automaticamente.

### 4. Usar la columna `NOVEDAD`

La columna `NOVEDAD` permite marcar excepciones. Cuando se llena, el sistema puede usar esa novedad como clasificacion del dia.

Ejemplos ficticios:

| Situacion | NOVEDAD recomendada | Resultado esperado |
| --- | --- | --- |
| El colaborador esta de vacaciones | VACACIONES | El dia se cuenta como vacaciones |
| El colaborador tiene incapacidad | INCAPACIDAD | El dia se cuenta como incapacidad |
| El colaborador tiene permiso autorizado | PERMISO | El dia se cuenta como permiso |
| Es un dia festivo | FESTIVO | El dia se cuenta como festivo |
| No hay excepcion | Dejar vacio | El semaforo se calcula con entrada/salida |

Esta columna es util para evitar que dias justificados aparezcan como faltas o retardos.

### 5. Consultar hojas de supervisor

Las hojas de supervisor muestran un resumen del equipo asignado.

En estas hojas puedes revisar:

- Total de registros verdes.
- Total de registros amarillos.
- Total de registros rojos.
- Total de registros rojo fuerte.
- Total de faltas.
- Total de vacaciones.
- Total de festivos.
- Total de incapacidades.
- Total de permisos.
- Porcentaje de cumplimiento.
- Registros u horas promedio segun la configuracion del archivo.
- Grafica de distribucion mensual por colaborador.

Uso recomendado:

- Seleccionar o revisar el periodo del reporte.
- Comparar colaboradores del mismo equipo.
- Detectar casos con muchas alertas amarillas, rojas o faltas.
- Identificar excepciones justificadas separadas de incumplimientos.

## Estructura del libro

### `PERSONAL`

Catalogo base de colaboradores.

Columnas principales:

- `No. EMP`: identificador ficticio del colaborador.
- `NOMBRE`: nombre ficticio del colaborador.
- `SUPERVISOR`: supervisor ficticio asignado.
- `ACTIVO`: indica si el colaborador se incluye en reportes.
- Columnas de reglas: parametros usados para clasificar asistencia en dias laborales y fines de semana.

### `REGISTRO`

Base de datos de asistencia.

Columnas principales:

- `FECHA`: fecha del registro.
- `No. EMP`: identificador del colaborador.
- `ENTRADA`: hora de entrada.
- `SALIDA`: hora de salida.
- `NOMBRE`: nombre relacionado con el numero de empleado.
- `SUPERVISOR`: supervisor relacionado con el colaborador.
- `DIA`: dia de la semana calculado.
- `MES`: mes calculado.
- `TIPO DIA`: indica si es dia laboral o fin de semana.
- `SEMAFORO`: clasificacion final del registro.
- `HORAS`: horas calculadas entre entrada y salida.
- `NOVEDAD`: excepcion manual como vacaciones, permiso, incapacidad o festivo.

### `NORMALIDAD`

Hoja auxiliar para calendario, dias y meses.

Se usa para apoyar calculos como:

- Dia de la semana.
- Nombre del mes.
- Separacion entre dias laborales y fines de semana.

### Hojas de supervisor

Hojas de reporte por equipo.

Funcionan como tableros resumidos para revisar el comportamiento mensual de asistencia de los colaboradores asignados a cada supervisor.

## Ejemplo de flujo de trabajo

Supongamos que se desea revisar el mes de junio.

1. Se agregan o revisan colaboradores en `PERSONAL`.
2. Se cargan registros diarios en `REGISTRO`.
3. Para registros normales, se capturan entrada y salida.
4. Para dias justificados, se selecciona una `NOVEDAD`.
5. El archivo clasifica cada fila con un estado de semaforo.
6. Las hojas de supervisor cuentan los resultados por colaborador.
7. El responsable revisa quienes tienen buen cumplimiento, retardos frecuentes o faltas.

Ejemplo:

| Caso | Datos capturados | Clasificacion |
| --- | --- | --- |
| Entrada puntual | Entrada 08:00, salida 17:00 | VERDE |
| Retardo leve | Entrada 08:12, salida 17:00 | AMARILLO |
| Retardo mayor | Entrada 08:35, salida 17:00 | ROJO |
| Sin registro | Entrada vacia, salida vacia | FALTA |
| Dia justificado | NOVEDAD = VACACIONES | VACACIONES |

## Clasificacion del semaforo

La clasificacion puede adaptarse segun las reglas internas del archivo.

- `VERDE`: asistencia dentro del rango esperado.
- `AMARILLO`: retardo leve o primera alerta.
- `ROJO`: retardo mayor.
- `ROJO FUERTE`: incumplimiento mas severo.
- `FALTA`: ausencia o registro incompleto segun la regla configurada.
- `VACACIONES`: dia marcado como vacaciones.
- `FESTIVO`: dia marcado como festivo.
- `INCAPACIDAD`: dia marcado como incapacidad.
- `PERMISO`: dia marcado como permiso.

## Datos ficticios y privacidad

Esta version no contiene datos reales.

Antes de publicarse:

- Los nombres fueron reemplazados por nombres inventados.
- Los numeros de empleado fueron reemplazados por identificadores ficticios.
- Los supervisores fueron reemplazados por nombres ficticios.
- El archivo original se mantiene fuera del repositorio.
- La informacion se presenta solo con fines de demostracion profesional.

Importante: si se adapta este archivo para una empresa real, no se recomienda publicar registros reales de asistencia, nombres reales, numeros de empleado reales ni informacion interna.

## Tecnologias usadas

- Microsoft Excel.
- Formulas condicionales.
- `IF`.
- `COUNTIFS`.
- Catalogos auxiliares.
- Listas desplegables.
- Reglas de clasificacion.
- Resumen por periodo.
- Tableros por supervisor.

## Valor del proyecto

Este proyecto demuestra capacidad para:

- Automatizar reportes operativos en Excel.
- Transformar registros crudos en indicadores.
- Separar incidencias reales de excepciones justificadas.
- Crear tableros simples para seguimiento de equipos.
- Reducir conteos manuales y errores de revision.
- Presentar informacion clara para toma de decisiones.

## Posibles mejoras futuras

- Agregar capturas de pantalla del archivo.
- Crear una version en Power BI.
- Crear una version automatizada con Python.
- Agregar instrucciones dentro del mismo libro de Excel.
- Agregar validaciones adicionales para evitar capturas incompletas.

---

# Excel Attendance Traffic Light System

Microsoft Excel system for reviewing attendance, lateness, absences, exceptions, and schedule compliance through a visual traffic light classification.

This repository contains an anonymized demo version. All names, employee numbers, supervisors, and records included in the file are fictional and are used only to demonstrate how the workbook works.

## Contents

- [Description](#description)
- [Included File](#included-file)
- [Requirements](#requirements)
- [Installation and Download](#installation-and-download)
- [How to Use the Workbook](#how-to-use-the-workbook)
- [Workbook Structure](#workbook-structure)
- [Workflow Example](#workflow-example)
- [Traffic Light Classification](#traffic-light-classification)
- [Fictional Data and Privacy](#fictional-data-and-privacy)
- [Project Value](#project-value)

## Description

The workbook helps turn clock-in and clock-out records into easy-to-review metrics. Instead of manually counting late arrivals, absences, or exceptions, the system classifies each record and summarizes the results by supervisor, employee, and period.

The main purpose is to provide a simple operational tracking tool:

- Enter or paste attendance records.
- Automatically classify each day with a traffic light status.
- Mark exceptions such as vacation, sick leave, personal leave, or holidays.
- Review summarized results by supervisor.
- View monthly metrics by employee.

## Included File

- `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx`

This is the file that should be opened to test the system. It is a public, anonymized copy of the project.

## Requirements

Recommended requirements:

- Microsoft Excel desktop version.
- Windows or macOS with support for `.xlsx` files.
- Basic Excel knowledge: opening sheets, editing cells, and filtering tables.

No macros, add-ins, or additional software are required.

## Installation and Download

### Option 1: Download from GitHub

1. Open the repository on GitHub.
2. Click `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx`.
3. Use the `Download` or `View raw` button to download the file.
4. Open the file in Microsoft Excel.
5. If Excel shows a warning because the file was downloaded from the internet, enable editing only if you trust the repository source.

### Option 2: Clone the Repository

If you use Git, clone the project:

```powershell
git clone https://github.com/YOUR_USERNAME/semaforo-asistencia-excel.git
cd semaforo-asistencia-excel
```

Then open:

```text
Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx
```

## How to Use the Workbook

### 1. Open the file

Open `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx` in Excel.

The workbook includes attendance records, an employee catalog, a helper calendar, and supervisor reports.

### 2. Review the employee catalog

Go to the `PERSONAL` sheet.

This sheet contains the demo employee list, employee number, assigned supervisor, active status, and rules used to classify records.

Fictional example:

| EMP No. | NAME | SUPERVISOR | ACTIVE |
| --- | --- | --- | --- |
| 7001 | SOFIA MORALES VEGA | CAMILA RIVERA NAVA | YES |
| 7002 | DIEGO RAMIREZ PENA | CAMILA RIVERA NAVA | YES |
| 7003 | VALERIA CASTILLO ROJAS | MATEO HERRERA SOLIS | YES |

Recommended use:

- Add new employees in this sheet if adapting the workbook.
- Keep the employee number as a unique identifier.
- Make sure the supervisor matches the corresponding summary sheet.
- Mark as active only the employees that should be included in reports.

### 3. Review or enter attendance records

Go to the `REGISTRO` sheet.

This is the main data sheet. Each row represents one attendance record for one employee on one date.

Fictional example:

| DATE | EMP No. | CHECK-IN | CHECK-OUT | NAME | SUPERVISOR | STATUS | EXCEPTION |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 06/01/2026 | 7001 | 08:00 | 17:00 | SOFIA MORALES VEGA | CAMILA RIVERA NAVA | GREEN | |
| 06/01/2026 | 7002 | 08:12 | 17:00 | DIEGO RAMIREZ PENA | CAMILA RIVERA NAVA | YELLOW | |
| 06/02/2026 | 7003 | - | - | VALERIA CASTILLO ROJAS | MATEO HERRERA SOLIS | ABSENCE | |
| 06/03/2026 | 7004 | - | - | MARIANA LOPEZ SANTOS | ALEJANDRO TORRES LUNA | VACATION | VACATION |

Recommended use:

- Enter the record date.
- Enter or paste the employee number.
- Enter check-in and check-out times when available.
- Use the exception column when the day has an authorized exception.
- Avoid manually overwriting formulas if the workbook already calculates fields automatically.

### 4. Use the `NOVEDAD` exception column

The `NOVEDAD` column is used to flag exceptions. When filled in, the system can use that exception as the final classification for the day.

Fictional examples:

| Situation | Recommended exception | Expected result |
| --- | --- | --- |
| Employee is on vacation | VACACIONES | The day is counted as vacation |
| Employee has sick leave | INCAPACIDAD | The day is counted as sick leave |
| Employee has authorized personal leave | PERMISO | The day is counted as personal leave |
| It is a holiday | FESTIVO | The day is counted as holiday |
| No exception applies | Leave blank | Status is calculated from check-in/check-out |

This column helps prevent justified days from being counted as absences or lateness.

### 5. Review supervisor sheets

Supervisor sheets show summaries for each assigned team.

In these sheets you can review:

- Total green records.
- Total yellow records.
- Total red records.
- Total strong red records.
- Total absences.
- Total vacation days.
- Total holidays.
- Total sick leave days.
- Total personal leave days.
- Compliance percentage.
- Records or average hours depending on the workbook configuration.
- Monthly distribution chart by employee.

Recommended use:

- Review the report period.
- Compare employees in the same team.
- Detect cases with frequent yellow, red, or absence records.
- Identify justified exceptions separately from attendance issues.

## Workbook Structure

### `PERSONAL`

Base employee catalog.

Main columns:

- `No. EMP`: fictional employee identifier.
- `NOMBRE`: fictional employee name.
- `SUPERVISOR`: assigned fictional supervisor.
- `ACTIVO`: indicates whether the employee is included in reports.
- Rule columns: parameters used to classify attendance on weekdays and weekends.

### `REGISTRO`

Attendance database.

Main columns:

- `FECHA`: record date.
- `No. EMP`: employee identifier.
- `ENTRADA`: check-in time.
- `SALIDA`: check-out time.
- `NOMBRE`: name linked to the employee number.
- `SUPERVISOR`: supervisor linked to the employee.
- `DIA`: calculated weekday.
- `MES`: calculated month.
- `TIPO DIA`: indicates weekday or weekend.
- `SEMAFORO`: final record classification.
- `HORAS`: calculated hours between check-in and check-out.
- `NOVEDAD`: manual exception such as vacation, personal leave, sick leave, or holiday.

### `NORMALIDAD`

Helper calendar sheet.

Used to support calculations such as:

- Weekday name.
- Month name.
- Difference between weekdays and weekends.

### Supervisor Sheets

Team report sheets.

They work as summary dashboards to review the monthly attendance behavior of employees assigned to each supervisor.

## Workflow Example

Assume you want to review June.

1. Employees are added or reviewed in `PERSONAL`.
2. Daily records are loaded into `REGISTRO`.
3. For normal records, check-in and check-out times are entered.
4. For justified days, an exception is selected in `NOVEDAD`.
5. The workbook classifies each row with a traffic light status.
6. Supervisor sheets count the results by employee.
7. The reviewer identifies good compliance, frequent lateness, or absences.

Example:

| Case | Captured data | Classification |
| --- | --- | --- |
| On-time check-in | Check-in 08:00, check-out 17:00 | GREEN |
| Minor lateness | Check-in 08:12, check-out 17:00 | YELLOW |
| Major lateness | Check-in 08:35, check-out 17:00 | RED |
| No record | Empty check-in, empty check-out | ABSENCE |
| Justified day | EXCEPTION = VACACIONES | VACATION |

## Traffic Light Classification

The classification can be adapted depending on the workbook's internal rules.

- `GREEN`: attendance within the expected range.
- `YELLOW`: minor lateness or first alert.
- `RED`: greater lateness.
- `STRONG RED`: more severe non-compliance.
- `ABSENCE`: absence or incomplete record according to the configured rule.
- `VACATION`: day marked as vacation.
- `HOLIDAY`: day marked as holiday.
- `SICK LEAVE`: day marked as sick leave.
- `PERSONAL LEAVE`: day marked as personal leave.

## Fictional Data and Privacy

This version does not contain real data.

Before publication:

- Names were replaced with fictional names.
- Employee numbers were replaced with fictional identifiers.
- Supervisors were replaced with fictional names.
- The original file is kept outside the repository.
- The information is presented only for professional demonstration purposes.

Important: if this workbook is adapted for a real company, real attendance records, real names, real employee numbers, or internal information should not be published.

## Technologies Used

- Microsoft Excel.
- Conditional formulas.
- `IF`.
- `COUNTIFS`.
- Helper catalogs.
- Dropdown lists.
- Classification rules.
- Period summaries.
- Supervisor dashboards.

## Project Value

This project demonstrates the ability to:

- Automate operational reports in Excel.
- Transform raw records into indicators.
- Separate real attendance issues from justified exceptions.
- Create simple dashboards for team tracking.
- Reduce manual counting and review errors.
- Present clear information for decision-making.

## Future Improvements

- Add workbook screenshots.
- Create a Power BI version.
- Create an automated Python version.
- Add instructions inside the Excel workbook.
- Add extra validations to prevent incomplete records.


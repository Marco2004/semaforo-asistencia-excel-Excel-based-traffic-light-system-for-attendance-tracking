# Sistema de Asistencia con Semaforo en Excel

Sistema en Microsoft Excel para registrar asistencia, clasificar entradas con un semaforo operativo y resumir resultados por supervisor, colaborador y mes.

El repositorio publica una version demo anonimizada: nombres, numeros de empleado, supervisores y registros fueron reemplazados por informacion ficticia para poder mostrar la logica del archivo sin exponer datos reales.

## Archivo incluido

- `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx`

Este es el libro principal. No requiere macros, complementos ni software adicional; funciona con formulas, validaciones, formato condicional, filtros y graficas de Excel.

## Que hace

El archivo convierte registros de asistencia en indicadores faciles de revisar:

- Relaciona cada numero de empleado con su nombre y supervisor.
- Calcula dia de la semana, mes y tipo de dia.
- Clasifica cada registro como `VERDE`, `AMARILLO`, `ROJO`, `ROJO FUERTE`, `FALTA` o una novedad autorizada.
- Permite marcar excepciones como `VACACIONES`, `INCAPACIDAD`, `PERMISO` y `FESTIVO`.
- Maneja reglas de horario diferentes para lunes-viernes y sabado-domingo.
- Resume resultados mensuales por supervisor y por colaborador.
- Muestra totales, porcentaje verde, cantidad de registros, promedio de horas y una grafica de distribucion mensual.

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
6. Revisar conteos, porcentaje verde, registros, horas promedio y grafica.

> Nota: como el archivo usa formulas de Excel, al abrirlo por primera vez Excel puede recalcular los resultados. La vista previa de GitHub no siempre muestra formulas calculadas igual que Excel de escritorio.

## Hoja `REGISTRO`

`REGISTRO` es la base de datos operativa. Tiene encabezados congelados, filtro sobre el rango principal y formulas preparadas hasta la fila 1722.

Columnas:

| Columna | Descripcion |
| --- | --- |
| `FECHA` | Fecha del registro de asistencia. |
| `No. EMP` | Numero de empleado ficticio; es la llave contra `PERSONAL`. |
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

### Regla de clasificacion

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

El formato condicional pinta `SEMAFORO` con colores: verde, amarillo, rojo, rojo fuerte, gris para faltas y morado para novedades.

## Hoja `PERSONAL`

`PERSONAL` es el catalogo maestro. En la demo contiene 19 colaboradores activos distribuidos en 3 supervisores.

Columnas:

| Columna | Descripcion |
| --- | --- |
| `No. EMP` | Identificador unico del colaborador. |
| `NOMBRE` | Nombre ficticio del colaborador. |
| `SUPERVISOR` | Supervisor asignado. |
| `ACTIVO` | Lista desplegable con `SÍ` / `NO` en el archivo demo. Solo los activos entran en tableros. |
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

### Reglas de horario incluidas

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

Los conteos usan `COUNTIFS` contra `REGISTRO`, filtrando por:

- Numero de empleado.
- Mes seleccionado.
- Estado de semaforo.

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

## English summary

Excel attendance workbook that classifies check-in records with a traffic-light status, supports authorized exceptions, uses per-employee schedule thresholds, and provides monthly supervisor dashboards. The published workbook is an anonymized demo with fictional data only.

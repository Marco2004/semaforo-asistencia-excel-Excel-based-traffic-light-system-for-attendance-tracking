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
  - [Guía de uso paso a paso](#guía-de-uso-paso-a-paso)
  - [Lógica del semáforo](#lógica-del-semáforo)
  - [Catálogo de personal](#catálogo-de-personal)
  - [Casos especiales de horario](#casos-especiales-de-horario)
  - [Tableros por supervisor](#tableros-por-supervisor)
  - [Arquitectura interna y fórmulas clave](#arquitectura-interna-y-fórmulas-clave)
  - [Características principales](#características-principales)
  - [Ejemplo de uso](#ejemplo-de-uso)
  - [Control de calidad](#control-de-calidad)
  - [Cómo adaptarlo](#cómo-adaptarlo)
  - [Requisitos](#requisitos)
  - [Instalación y puesta en marcha](#instalación-y-puesta-en-marcha)
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
  - [Step-by-step usage guide](#step-by-step-usage-guide)
  - [Traffic-light logic](#traffic-light-logic)
  - [Employee catalog](#employee-catalog)
  - [Special schedule cases](#special-schedule-cases)
  - [Supervisor dashboards](#supervisor-dashboards)
  - [Internal architecture and key formulas](#internal-architecture-and-key-formulas)
  - [Main features](#main-features)
  - [Usage example](#usage-example)
  - [Quality assurance](#quality-assurance)
  - [How to adapt it](#how-to-adapt-it)
  - [Requirements](#requirements)
  - [Installation and setup](#installation-and-setup)
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
| `PERSONAL` | Catálogo de colaboradores, supervisores, estatus activo y reglas de clasificación por horario (el horario **vigente hoy** de cada quien). |
| `NORMALIDAD` | Calendario auxiliar con días de la semana y catálogo de meses. |
| `EXCEPCIONES_FECHA` | Horario especial para un día puntual (junta, evento, capacitación), para todo el equipo o para un empleado en concreto. |
| `HISTORIAL_HORARIOS` | Respaldo de horarios anteriores, con su rango de fechas de vigencia, para que un cambio de turno no altere el semáforo de días ya pasados. |
| Tableros de supervisor | Una hoja por supervisor con el resumen mensual de su equipo. La demo incluye varias hojas de ejemplo con nombres ficticios. |

## Flujo de trabajo

1. Abrir el archivo en Microsoft Excel.
2. Revisar o actualizar el catálogo en `PERSONAL`.
3. Cargar registros diarios en `REGISTRO`.
4. Usar la columna `NOVEDAD` cuando un día tenga justificación autorizada (`VACACIONES`, `INCAPACIDAD`, `PERMISO`, `FESTIVO`, `DESCANSO`, `DESCANSO POR DINAMICA` o `DINAMICA`).
5. Elegir el mes en el selector de cada hoja de supervisor.
6. Revisar conteos, porcentaje verde, registros, promedio de horas y gráfica.

> Nota: como el archivo usa fórmulas, Excel recalcula los resultados al abrirlo. La vista previa de GitHub no siempre muestra el workbook igual que Excel de escritorio; para verlo con fórmulas activas hay que descargarlo y abrirlo en Excel.

## Guía de uso paso a paso

El sistema tiene dos tipos de usuario, cada uno con su propio recorrido dentro del mismo archivo:

**Rol 1 — Quien administra el catálogo (RH / coordinación):**

1. Da de alta al colaborador en `PERSONAL` con su número de empleado, nombre y supervisor asignado.
2. Marca `ACTIVO = SÍ`. Este campo es lo único que decide si el colaborador aparece en el tablero de su supervisor; no hace falta tocar ninguna fórmula.
3. Define sus ocho umbrales de horario (verde, amarillo, rojo y rojo fuerte, uno para entre semana y otro para fin de semana). Estos umbrales son independientes por colaborador, así que turnos distintos conviven en el mismo catálogo.
4. Si el colaborador deja el equipo, cambia `ACTIVO` a `NO` en lugar de borrar la fila: conserva su historial en `REGISTRO` sin que siga apareciendo en los tableros vigentes.

**Rol 2 — Quien captura asistencia (día a día):**

1. Agrega una fila en `REGISTRO` por cada evento: fecha, número de empleado, hora de entrada y hora de salida.
2. Si el día tuvo una justificación autorizada, la selecciona en la lista desplegable de `NOVEDAD` (`VACACIONES`, `INCAPACIDAD`, `PERMISO`, `FESTIVO`, `DESCANSO`, `DESCANSO POR DINAMICA` o `DINAMICA`); si no, la deja vacía.
3. El resto de la fila (nombre, supervisor, día, mes, tipo de día, semáforo y horas) se calcula solo, apenas hay fecha, número de empleado y horas capturadas.
4. Si una fila muestra `NO EXISTE` en nombre/supervisor o `REVISAR` en el semáforo, el número de empleado no coincide con `PERSONAL` (typo, empleado inactivo o umbrales incompletos). Se corrige en el catálogo, no en `REGISTRO`.

**Rol 3 — Supervisor que revisa su equipo (mensual):**

1. Abre su propia hoja (una por supervisor) y elige el mes en el selector desplegable.
2. La lista de colaboradores activos de su equipo aparece automáticamente; no necesita filtrar nada a mano.
3. Revisa los conteos por estado, el porcentaje verde, el promedio de horas y la gráfica circular del periodo.
4. Si algún colaborador no aparece, casi siempre es porque su `ACTIVO` en `PERSONAL` no está en `SÍ` o porque su supervisor asignado no coincide exactamente con el nombre de la hoja.

**Errores comunes y cómo resolverlos:**

| Señal en el archivo | Causa típica | Solución |
| --- | --- | --- |
| `NO EXISTE` en `NOMBRE`/`SUPERVISOR` | El número de empleado en `REGISTRO` no está en `PERSONAL` | Verificar el número de empleado o darlo de alta en `PERSONAL` |
| `REVISAR` en `SEMÁFORO` | El empleado existe pero sus umbrales de horario están incompletos o mal capturados | Completar los ocho umbrales del colaborador en `PERSONAL` |
| Un colaborador no aparece en el tablero de su supervisor | `ACTIVO` no está en `SÍ`, o el nombre del supervisor no coincide exactamente con el de la hoja | Corregir el campo `ACTIVO` o el nombre del supervisor en `PERSONAL` |
| Los totales no cambian al capturar un registro nuevo | El archivo no ha recalculado, o la fila se capturó fuera del rango que usan las fórmulas | Forzar recálculo (`Ctrl+Alt+F9`) o extender el rango de fórmulas/filtro |

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

El formato condicional pinta el campo `SEMÁFORO` por estado: verde, amarillo, rojo, rojo fuerte, gris para faltas y morado para las excepciones autorizadas (`VACACIONES`, `INCAPACIDAD`, `PERMISO`, `FESTIVO`, `DESCANSO`, `DESCANSO POR DINAMICA`, `DINAMICA`).

## Catálogo de personal

`PERSONAL` es el catálogo maestro: número de empleado, nombre, supervisor asignado, estatus activo (`SÍ`/`NO`) y los umbrales de horario descritos arriba. Solo los colaboradores marcados como activos aparecen en los tableros de supervisor.

Una hoja auxiliar de calendario (`NORMALIDAD`) documenta los días y meses usados por el archivo, aunque `REGISTRO` calcula esa información directamente con fórmulas.

## Casos especiales de horario

`REGISTRO` no compara la hora de entrada directamente contra `PERSONAL`. Primero calcula, para cada fila (en 3 columnas ocultas al final de `REGISTRO`: `UMBRAL AMARILLO`, `UMBRAL ROJO` y `UMBRAL ROJO FUERTE`), cuál era el umbral que en verdad aplicaba ese día para ese colaborador, revisando en este orden:

1. **`EXCEPCIONES_FECHA`** — ¿hay una excepción para ese empleado en esa fecha exacta?
2. **`EXCEPCIONES_FECHA`** — si no, ¿hay una excepción general para esa fecha (con `No. EMP` vacío, o sea "aplica a todos")?
3. **`HISTORIAL_HORARIOS`** — si no, ¿ese empleado tenía un horario distinto vigente en esa fecha (porque ya cambió de turno)?
4. **`PERSONAL`** — si nada de lo anterior aplica, se usa el horario actual del colaborador (el comportamiento de siempre).

No necesitas tocar ninguna fórmula para usar esto: solo llena la hoja que corresponda cuando se dé el caso. Si nunca las usas, el archivo funciona exactamente igual que antes.

**Caso 1 — Un día en específico piden que todos (o algunos) entren a cierta hora:**

En `EXCEPCIONES_FECHA` agrega una fila con la fecha y los 4 horarios (verde, amarillo, rojo, rojo fuerte — los mismos 4 niveles que usa `PERSONAL`) que aplican ese día:
- Deja `No. EMP` **vacío** si el horario especial aplica a todo el equipo.
- Pon el número de empleado si solo aplica a una persona (por ejemplo, alguien con un permiso especial de llegar más tarde ese día).

Ese día, el semáforo de `REGISTRO` usa esos umbrales en vez de los umbrales normales de `PERSONAL`, sin afectar ningún otro día.

**Caso 2 — Un colaborador cambia de horario a la mitad del periodo:**

Si simplemente editas sus umbrales en `PERSONAL`, **todo su historial pasado en `REGISTRO` se recalcularía con el horario nuevo**, lo cual estaría mal. Para evitarlo:

1. Antes de cambiar nada en `PERSONAL`, agrega una fila en `HISTORIAL_HORARIOS` con: número de empleado, la fecha desde la que aplicó su horario **anterior** (`VIGENTE DESDE`), la fecha en que dejó de aplicar (`VIGENTE HASTA` = el día antes del cambio), y los 8 umbrales que tenía ese horario anterior (los mismos que ya tenía capturados en `PERSONAL`).
2. Ahora sí, actualiza los umbrales en `PERSONAL` con el horario nuevo.

A partir de ahí, los registros con fecha dentro del rango guardado en `HISTORIAL_HORARIOS` siguen usando el horario viejo, y los registros nuevos (después de `VIGENTE HASTA`) usan automáticamente el horario que quedó en `PERSONAL`.

## Tableros por supervisor

Cada supervisor tiene su propia hoja, con la misma estructura:

- Selector de periodo (mes) mediante lista desplegable.
- Lista automática de los colaboradores activos de ese supervisor.
- Conteos mensuales por estado (verde, amarillo, rojo, rojo fuerte, falta, y cada tipo de novedad: `VACACIONES`, `FESTIVO`, `INCAPACIDAD`, `PERMISO`, `DESCANSO`, `DESCANSO POR DINAMICA`, `DINAMICA`).
- Totales, porcentaje verde y promedio de horas del periodo.
- Gráfica circular de distribución mensual, ubicada a la derecha de todas las columnas de novedad para no taparlas.

Los conteos se calculan contra `REGISTRO`, filtrando por empleado, mes seleccionado y estado de semáforo. El porcentaje verde se calcula solo sobre los estados operativos; las novedades justificadas se muestran aparte, cada una en su propia columna, para no mezclarlas con incumplimientos.

## Arquitectura interna y fórmulas clave

El archivo no usa una sola fórmula "mágica": encadena varias técnicas de Excel, cada una resolviendo un problema puntual. Así fluye la información entre hojas:

```
PERSONAL (catálogo maestro)
  └─ columna LLAVE = SUPERVISOR & "|" & posición consecutiva entre sus activos

EXCEPCIONES_FECHA / HISTORIAL_HORARIOS (casos especiales, opcionales)
  └─ umbrales que sustituyen a PERSONAL solo para una fecha, o solo mientras estuvieron vigentes
        │
        ▼
REGISTRO (captura diaria)
  ├─ trae NOMBRE / SUPERVISOR desde PERSONAL buscando por número de empleado
  ├─ calcula DÍA, MES y TIPO DÍA a partir de la fecha
  ├─ resuelve el umbral efectivo del día (columnas ocultas UMBRAL AMARILLO/ROJO/ROJO FUERTE):
  │   EXCEPCIONES_FECHA (empleado) → EXCEPCIONES_FECHA (todos) → HISTORIAL_HORARIOS (vigente ese día) → PERSONAL (actual)
  └─ compara la hora de entrada contra esos umbrales ya resueltos → SEMÁFORO
        │
        ▼
Tableros de supervisor
  ├─ reconstruyen la lista de activos de ESE supervisor buscando "SUPERVISOR|1", "SUPERVISOR|2"... en LLAVE
  ├─ cuentan resultados del mes elegido contra REGISTRO (COUNTIFS)
  └─ promedian horas (AVERAGEIFS) y calculan % VERDE sobre el total operativo
```

Algunas fórmulas reales del archivo, simplificadas para lectura (las columnas exactas están en la hoja):

Búsqueda cruzada de nombre/supervisor por número de empleado (`REGISTRO`):
```excel
=IF($B2="","",IFERROR(INDEX(PERSONAL!$B$2:$B$80,MATCH($B2,PERSONAL!$A$2:$A$80,0)),"NO EXISTE"))
```

Horas trabajadas, incluyendo turnos que cruzan la medianoche (`REGISTRO`):
```excel
=IF(OR($C2="",$D2=""),"",IF($D2>=$C2,($D2-$C2)*24,(1-$C2+$D2)*24))
```

Clasificación del semáforo, evaluando primero los niveles más severos (`REGISTRO`):
```excel
=IF(OR($A2="",$B2=""),"",
  IF($L2<>"",UPPER($L2),
  IF($C2="","FALTA",
  IFERROR(
    IF($C2>=$O2,"ROJO FUERTE",
    IF($C2>=$N2,"ROJO",
    IF($C2>=$M2,"AMARILLO","VERDE"))),
  "REVISAR"))))
```
`$M2`, `$N2` y `$O2` son las 3 columnas ocultas (`UMBRAL AMARILLO`, `UMBRAL ROJO`, `UMBRAL ROJO FUERTE`) que resuelven el umbral efectivo de ese día, con esta prioridad (simplificada; cada paso es en realidad un `INDEX/MATCH` con `IFERROR` de respaldo):
```excel
=IFERROR(excepción del empleado en EXCEPCIONES_FECHA,
  IFERROR(excepción general en EXCEPCIONES_FECHA,
    IFERROR(horario vigente en HISTORIAL_HORARIOS para esa fecha,
      horario actual en PERSONAL)))
```
Ver [Casos especiales de horario](#casos-especiales-de-horario) para el detalle de cuándo se usa cada nivel.

Clave compuesta que permite reconstruir el equipo de cada supervisor sin macros (`PERSONAL`):
```excel
' Columna IDX SUP: posición consecutiva del colaborador activo dentro de su supervisor
=IF($A2="","",IF($D2<>"SÍ","",COUNTIFS($C$2:C2,C2,$D$2:D2,"SÍ")))
' Columna LLAVE: combina supervisor + posición en un identificador único
=IF(M2="","",C2&"|"&M2)
```

Lectura de esa clave desde el tablero del supervisor, fila por fila:
```excel
=IFERROR(INDEX(PERSONAL!$A:$A,MATCH($B$3&"|"&1,PERSONAL!$N:$N,0)),"")
```
`$B$3` es el nombre del supervisor de esa hoja; el `&"|"&1`, `&"|"&2`, etc. avanza una posición por fila, así que la lista de colaboradores activos se arma sola y se corre automáticamente si alguien deja de estar activo.

Conteo mensual por estado y promedio de horas (tablero de supervisor):
```excel
=COUNTIFS(REGISTRO!$B$2:$B$1722,$B8,REGISTRO!$H$2:$H$1722,$C$5,REGISTRO!$J$2:$J$1722,"VERDE")
=IFERROR(AVERAGEIFS(REGISTRO!$K$2:$K$1722,REGISTRO!$F$2:$F$1722,$B$3,REGISTRO!$H$2:$H$1722,$C$5),0)
=IF(SUM(D20:H20)=0,0,D20/SUM(D20:H20))
```

Validación de datos que evita capturas inválidas:
- Lista desplegable en `NOVEDAD`: `VACACIONES, INCAPACIDAD, PERMISO, FESTIVO, DESCANSO, DESCANSO POR DINAMICA, DINAMICA`.
- Rango de hora válido en entrada/salida: `AND(hora>=00:00:00, hora<=23:59:59)`.
- Lista desplegable de mes en cada tablero de supervisor: `ENERO...DICIEMBRE`.

Todo esto corre con fórmulas nativas de Excel (incluyendo fórmulas de matriz en las columnas calculadas de `REGISTRO`); no hay VBA, Power Query ni conexiones externas.

## Características principales

- Archivo 100% Excel, sin macros.
- Demo pública con datos y nombres completamente ficticios.
- Catálogo centralizado de personal.
- Clasificación automática por semáforo, con prioridad explícita entre novedad, falta y niveles de retardo.
- Reglas de horario propias por colaborador, diferenciadas entre semana y fin de semana.
- Excepciones de horario por fecha (para todo el equipo o para un empleado), sin afectar otros días.
- Historial de cambios de horario, para que un cambio de turno no altere el semáforo de registros ya pasados.
- Excepciones autorizadas mediante lista desplegable.
- Indicador de revisión cuando un empleado no existe o su configuración no coincide.
- Cálculo automático de día, mes, tipo de día y horas (incluye turnos que cruzan la medianoche).
- Filtros y formato condicional sobre la base de asistencia.
- Tableros separados por supervisor, con selector mensual, totales, porcentaje verde y promedio de horas.
- Gráfica circular de distribución mensual por supervisor, con colores fijos por segmento (no dependen del tema de Excel), para que se vean igual en cualquier versión de Excel.

## Ejemplo de uso

| Captura | Resultado esperado |
| --- | --- |
| Entrada puntual | `VERDE` |
| Entrada después del umbral amarillo | `AMARILLO` |
| Entrada después del umbral rojo | `ROJO` |
| Entrada después del umbral rojo fuerte | `ROJO FUERTE` |
| Sin hora de entrada | `FALTA` |
| `NOVEDAD = VACACIONES` | `VACACIONES` |
| `NOVEDAD = DESCANSO` | `DESCANSO` |
| `NOVEDAD = DESCANSO POR DINAMICA` | `DESCANSO POR DINAMICA` |
| `NOVEDAD = DINAMICA` | `DINAMICA` |
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

## Instalación y puesta en marcha

No hay instalador: es un solo archivo `.xlsx`. Los pasos son de configuración, no de instalación de software.

1. **Obtener el archivo.** Descárgalo desde este repositorio (ver [Descargar o clonar](#descargar-o-clonar)) o copia el que ya tengas.
2. **Abrirlo con Excel de escritorio**, no con la vista previa de GitHub ni con un lector web: solo el Excel de escritorio recalcula las fórmulas y respeta el formato condicional y las gráficas.
3. **Habilitar contenido si Excel lo pide.** Al venir de una descarga, Excel puede abrir el archivo en "Vista protegida". Selecciona `Habilitar edición`. El archivo no contiene macros, así que no debe aparecer ninguna advertencia de seguridad de macros; si aparece, verifica que estás abriendo el `.xlsx` original y no una copia renombrada como `.xlsm`.
4. **Verificar el cálculo automático.** En `Fórmulas > Opciones para calcular`, confirma que esté en `Automático`. Si en algún momento los totales no se actualizan, fuerza un recálculo completo con `Ctrl+Alt+F9`.
5. **Revisar el idioma regional de Excel.** Las fórmulas usan `;` o `,` como separador de argumentos según la configuración regional de Windows; si Excel marca error en una fórmula al abrir el archivo en un equipo con configuración regional distinta, es ese separador, no un error de la lógica del archivo.
6. **Compatibilidad.** Se probó en Excel de escritorio (Microsoft 365 / Excel 2019 o superior). Excel Online y la app móvil pueden abrirlo para consulta, pero algunas fórmulas de matriz y la interacción con listas desplegables se comportan mejor en escritorio. No se ha probado en LibreOffice Calc ni Google Sheets; al ser fórmulas estándar debería importarse, pero el formato condicional y las gráficas pueden requerir ajuste manual.
7. **Primer uso.** Antes de capturar datos reales, sigue la [guía de uso paso a paso](#guía-de-uso-paso-a-paso) para dar de alta al menos un colaborador de prueba y confirmar que el semáforo y los tableros calculan como se espera en tu equipo.

## Descargar o clonar

Descarga directa desde GitHub:

1. Abrir el repositorio.
2. Seleccionar `Sistema_Asistencia_Semaforo_2026_DEMO_ANONIMIZADO.xlsx`.
3. Usar `Download` o `View raw`.
4. Abrir el archivo en Excel.

Clonar con Git:

```powershell
git clonehttps://github.com/Marco2004/semaforo-asistencia-excel-Excel-based-traffic-light-system-for-attendance-tracking.git
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
| `PERSONAL` | Employee catalog with supervisors, active status, and schedule classification rules (each employee's **currently active** schedule). |
| `NORMALIDAD` | Helper calendar with weekdays and a month catalog. |
| `EXCEPCIONES_FECHA` | Special schedule for a specific date (a meeting, event, or training), for the whole team or for a single employee. |
| `HISTORIAL_HORARIOS` | Backup of past schedules with their effective date range, so a shift change doesn't retroactively alter the traffic light of days that already happened. |
| Supervisor dashboards | One sheet per supervisor summarizing their team each month. The demo includes a few sample sheets with fictional names. |

## Workflow

1. Open the file in Microsoft Excel.
2. Review or update the catalog in `PERSONAL`.
3. Load daily records in `REGISTRO`.
4. Use the `NOVEDAD` column when a day has an authorized justification (`VACACIONES`, `INCAPACIDAD`, `PERMISO`, `FESTIVO`, `DESCANSO`, `DESCANSO POR DINAMICA`, or `DINAMICA`).
5. Select the month in the dropdown on each supervisor sheet.
6. Review counts, green percentage, records, average hours, and the chart.

> Note: because the workbook uses formulas, Excel recalculates results when it opens the file. GitHub's preview does not always render the workbook the way desktop Excel does; to see it with live formulas, download it and open it in Excel.

## Step-by-step usage guide

The system has three kinds of users, each with their own path through the same file:

**Role 1 — Whoever administers the catalog (HR / coordination):**

1. Register the employee in `PERSONAL` with employee number, name, and assigned supervisor.
2. Set `ACTIVO = SÍ` (yes). This single field decides whether the employee shows up on their supervisor's dashboard — no formula needs to be touched.
3. Define their eight schedule thresholds (green, yellow, red, and strong red, one set for weekdays and one for weekends). Thresholds are independent per employee, so different shifts coexist in the same catalog.
4. If someone leaves the team, switch `ACTIVO` to `NO` instead of deleting the row: it keeps their history in `REGISTRO` without showing them on current dashboards.

**Role 2 — Whoever captures attendance (day to day):**

1. Add one row per event in `REGISTRO`: date, employee number, check-in time, and check-out time.
2. If the day had an authorized justification, pick it from the `NOVEDAD` dropdown (`VACACIONES`, `INCAPACIDAD`, `PERMISO`, `FESTIVO`, `DESCANSO`, `DESCANSO POR DINAMICA`, or `DINAMICA`); otherwise leave it blank.
3. The rest of the row (name, supervisor, day, month, day type, traffic light, and hours) calculates itself as soon as date, employee number, and times are entered.
4. If a row shows `NO EXISTE` in name/supervisor or a review flag in the traffic-light column, the employee number doesn't match `PERSONAL` (typo, inactive employee, or incomplete thresholds). Fix it in the catalog, not in `REGISTRO`.

**Role 3 — Supervisor reviewing their team (monthly):**

1. Open their own sheet (one per supervisor) and pick the month from the dropdown.
2. The list of their team's active employees appears automatically — no manual filtering needed.
3. Review counts by status, the green percentage, average hours, and the period's pie chart.
4. If an employee is missing, it's almost always because their `ACTIVO` field in `PERSONAL` isn't set to yes, or their assigned supervisor doesn't exactly match the sheet's name.

**Common issues and how to fix them:**

| Signal in the file | Typical cause | Fix |
| --- | --- | --- |
| `NO EXISTE` in name/supervisor | The employee number in `REGISTRO` isn't in `PERSONAL` | Check the employee number or register it in `PERSONAL` |
| Review flag in the traffic-light column | The employee exists but their schedule thresholds are incomplete or miscaptured | Fill in all eight thresholds for that employee in `PERSONAL` |
| An employee is missing from their supervisor's dashboard | `ACTIVO` isn't set to yes, or the supervisor name doesn't match the sheet exactly | Fix the `ACTIVO` field or the supervisor name in `PERSONAL` |
| Totals don't change after entering a new record | The workbook hasn't recalculated, or the row was entered outside the range the formulas cover | Force a recalculation (`Ctrl+Alt+F9`) or extend the formula/filter range |

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

Conditional formatting colors the `SEMÁFORO` field by status: green, yellow, red, strong red, gray for absences, and purple for authorized exceptions (`VACACIONES`, `INCAPACIDAD`, `PERMISO`, `FESTIVO`, `DESCANSO`, `DESCANSO POR DINAMICA`, `DINAMICA`).

## Employee catalog

`PERSONAL` is the master catalog: employee number, name, assigned supervisor, active status (yes/no), and the schedule thresholds described above. Only employees marked active appear on the supervisor dashboards.

A helper calendar sheet (`NORMALIDAD`) documents the days and months used by the file, although `REGISTRO` calculates that information directly with formulas.

## Special schedule cases

`REGISTRO` doesn't compare check-in time directly against `PERSONAL`. For every row it first works out, in 3 hidden helper columns at the end of `REGISTRO` (`UMBRAL AMARILLO`, `UMBRAL ROJO`, `UMBRAL ROJO FUERTE`), which threshold actually applied to that employee on that date, checking in this order:

1. **`EXCEPCIONES_FECHA`** — is there an exception for that specific employee on that exact date?
2. **`EXCEPCIONES_FECHA`** — if not, is there a general exception for that date (blank `No. EMP`, meaning "applies to everyone")?
3. **`HISTORIAL_HORARIOS`** — if not, did that employee have a different schedule in effect on that date (because their shift already changed since)?
4. **`PERSONAL`** — if none of the above apply, use the employee's current schedule (today's default behavior).

You don't need to touch any formula to use this — just fill in the relevant sheet when the situation comes up. If you never use them, the file behaves exactly as before.

**Case 1 — On a specific day, everyone (or some people) is asked to arrive at a set time:**

Add a row in `EXCEPCIONES_FECHA` with the date and the 4 thresholds (green, yellow, red, strong red — the same 4 levels `PERSONAL` uses) that apply that day:
- Leave `No. EMP` **blank** if the special schedule applies to the whole team.
- Enter the employee number if it only applies to one person (for example, someone authorized to arrive later that specific day).

That day, `REGISTRO`'s traffic light uses those thresholds instead of the employee's normal `PERSONAL` thresholds, without affecting any other day.

**Case 2 — An employee's schedule changes partway through the period:**

If you simply edit their thresholds in `PERSONAL`, **their entire past history in `REGISTRO` would be recalculated with the new schedule**, which would be wrong. To avoid that:

1. Before changing anything in `PERSONAL`, add a row in `HISTORIAL_HORARIOS` with: employee number, the date their **previous** schedule started applying (`VIGENTE DESDE`), the date it stopped applying (`VIGENTE HASTA` = the day before the change), and the 8 thresholds that old schedule had (the same ones already captured in `PERSONAL`).
2. Now update the thresholds in `PERSONAL` with the new schedule.

From then on, records dated within the range saved in `HISTORIAL_HORARIOS` keep using the old schedule, and new records (after `VIGENTE HASTA`) automatically use whatever is currently in `PERSONAL`.

## Supervisor dashboards

Each supervisor has their own sheet, sharing the same structure:

- A month selector via dropdown.
- An automatic list of that supervisor's active employees.
- Monthly counts by status (green, yellow, red, strong red, absent, and each exception type: `VACACIONES`, `FESTIVO`, `INCAPACIDAD`, `PERMISO`, `DESCANSO`, `DESCANSO POR DINAMICA`, `DINAMICA`).
- Totals, green percentage, and average hours for the period.
- A monthly distribution pie chart, positioned to the right of every exception column so none of them are hidden behind it.

Counts are calculated against `REGISTRO`, filtering by employee, selected month, and traffic-light status. The green percentage is calculated only over operational states; authorized exceptions are shown separately, each in its own column, so they aren't mixed with attendance issues.

## Internal architecture and key formulas

The file doesn't rely on one "magic" formula: it chains several Excel techniques, each solving one specific problem. This is how data flows between sheets:

```
PERSONAL (master catalog)
  └─ LLAVE column = SUPERVISOR & "|" & consecutive position among their active employees

EXCEPCIONES_FECHA / HISTORIAL_HORARIOS (optional special cases)
  └─ thresholds that replace PERSONAL only for one date, or only while they were in effect
        │
        ▼
REGISTRO (daily entry)
  ├─ pulls NOMBRE / SUPERVISOR from PERSONAL by looking up the employee number
  ├─ calculates DÍA, MES, and TIPO DÍA from the date
  ├─ resolves that day's effective threshold (hidden columns UMBRAL AMARILLO/ROJO/ROJO FUERTE):
  │   EXCEPCIONES_FECHA (employee) → EXCEPCIONES_FECHA (everyone) → HISTORIAL_HORARIOS (in effect that day) → PERSONAL (current)
  └─ compares the check-in time against those already-resolved thresholds → SEMÁFORO
        │
        ▼
Supervisor dashboards
  ├─ rebuild that supervisor's active-employee list by looking up "SUPERVISOR|1", "SUPERVISOR|2"... in LLAVE
  ├─ count the selected month's results against REGISTRO (COUNTIFS)
  └─ average hours (AVERAGEIFS) and compute % green over the operational total
```

Some of the actual formulas in the file, simplified for readability (the exact columns live in the sheet):

Cross-sheet lookup of name/supervisor by employee number (`REGISTRO`):
```excel
=IF($B2="","",IFERROR(INDEX(PERSONAL!$B$2:$B$80,MATCH($B2,PERSONAL!$A$2:$A$80,0)),"NO EXISTE"))
```

Hours worked, including shifts that cross midnight (`REGISTRO`):
```excel
=IF(OR($C2="",$D2=""),"",IF($D2>=$C2,($D2-$C2)*24,(1-$C2+$D2)*24))
```

Traffic-light classification, checking the most severe levels first (`REGISTRO`):
```excel
=IF(OR($A2="",$B2=""),"",
  IF($L2<>"",UPPER($L2),
  IF($C2="","FALTA",
  IFERROR(
    IF($C2>=$O2,"ROJO FUERTE",
    IF($C2>=$N2,"ROJO",
    IF($C2>=$M2,"AMARILLO","VERDE"))),
  "REVISAR"))))
```
`$M2`, `$N2`, and `$O2` are the 3 hidden columns (`UMBRAL AMARILLO`, `UMBRAL ROJO`, `UMBRAL ROJO FUERTE`) that resolve that day's effective threshold, with this priority (simplified; each step is actually an `INDEX/MATCH` with an `IFERROR` fallback):
```excel
=IFERROR(employee-specific exception in EXCEPCIONES_FECHA,
  IFERROR(general exception in EXCEPCIONES_FECHA,
    IFERROR(schedule in effect that date in HISTORIAL_HORARIOS,
      current schedule in PERSONAL)))
```
See [Special schedule cases](#special-schedule-cases) for the detail of when each level kicks in.

Composite key that lets each supervisor's team be rebuilt without macros (`PERSONAL`):
```excel
' IDX SUP column: consecutive position of the active employee within their supervisor
=IF($A2="","",IF($D2<>"SÍ","",COUNTIFS($C$2:C2,C2,$D$2:D2,"SÍ")))
' LLAVE column: combines supervisor + position into a unique identifier
=IF(M2="","",C2&"|"&M2)
```

Reading that key back from the supervisor dashboard, row by row:
```excel
=IFERROR(INDEX(PERSONAL!$A:$A,MATCH($B$3&"|"&1,PERSONAL!$N:$N,0)),"")
```
`$B$3` is that sheet's supervisor name; the `&"|"&1`, `&"|"&2`, etc. advances one position per row, so the active-employee list assembles itself and automatically shifts if someone stops being active.

Monthly count per status and average hours (supervisor dashboard):
```excel
=COUNTIFS(REGISTRO!$B$2:$B$1722,$B8,REGISTRO!$H$2:$H$1722,$C$5,REGISTRO!$J$2:$J$1722,"VERDE")
=IFERROR(AVERAGEIFS(REGISTRO!$K$2:$K$1722,REGISTRO!$F$2:$F$1722,$B$3,REGISTRO!$H$2:$H$1722,$C$5),0)
=IF(SUM(D20:H20)=0,0,D20/SUM(D20:H20))
```

Data validation that prevents invalid entries:
- Dropdown list in `NOVEDAD`: `VACACIONES, INCAPACIDAD, PERMISO, FESTIVO, DESCANSO, DESCANSO POR DINAMICA, DINAMICA`.
- Valid time range for check-in/check-out: `AND(time>=00:00:00, time<=23:59:59)`.
- Month dropdown on each supervisor dashboard: `ENERO...DICIEMBRE`.

All of this runs on native Excel formulas (including array formulas in `REGISTRO`'s calculated columns); there is no VBA, Power Query, or external connections.

## Main features

- 100% Excel workbook, no macros.
- Public demo with entirely fictional data and names.
- Centralized employee catalog.
- Automatic traffic-light classification, with an explicit priority order between exception, absence, and lateness levels.
- Per-employee schedule rules, differentiated between weekdays and weekends.
- Date-specific schedule exceptions (for the whole team or one employee), without affecting other days.
- Schedule change history, so a shift change doesn't retroactively alter the traffic light of past records.
- Authorized exceptions through a dropdown list.
- Review indicator when an employee does not exist or the configuration does not match.
- Automatic weekday, month, day type, and hours calculation (including overnight shifts).
- Filters and conditional formatting on the attendance database.
- Separate supervisor dashboards with a monthly selector, totals, green percentage, and average hours.
- Monthly distribution pie chart per supervisor, with fixed per-slice colors (not theme-dependent), so it looks the same across Excel versions.

## Usage example

| Input | Expected result |
| --- | --- |
| On-time check-in | `VERDE` |
| Check-in after yellow threshold | `AMARILLO` |
| Check-in after red threshold | `ROJO` |
| Check-in after strong red threshold | `ROJO FUERTE` |
| No check-in | `FALTA` |
| `NOVEDAD = VACACIONES` | `VACACIONES` |
| `NOVEDAD = DESCANSO` | `DESCANSO` |
| `NOVEDAD = DESCANSO POR DINAMICA` | `DESCANSO POR DINAMICA` |
| `NOVEDAD = DINAMICA` | `DINAMICA` |
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

## Installation and setup

There's no installer: it's a single `.xlsx` file. The steps below are configuration, not software installation.

1. **Get the file.** Download it from this repository (see [Download or clone](#download-or-clone)) or copy the one you already have.
2. **Open it with desktop Excel**, not GitHub's preview or a web viewer: only desktop Excel recalculates formulas and honors conditional formatting and charts correctly.
3. **Enable content if Excel asks.** Since it comes from a download, Excel may open it in "Protected View." Click `Enable Editing`. The file contains no macros, so no macro-security warning should appear; if one does, confirm you're opening the original `.xlsx` and not a copy renamed to `.xlsm`.
4. **Check automatic calculation.** Under `Formulas > Calculation Options`, confirm it's set to `Automatic`. If totals ever stop updating, force a full recalculation with `Ctrl+Alt+F9`.
5. **Check Excel's regional settings.** Formulas use `;` or `,` as the argument separator depending on Windows' regional configuration; if Excel flags a formula error on a machine with different regional settings, that's the separator, not a problem with the file's logic.
6. **Compatibility.** Tested on desktop Excel (Microsoft 365 / Excel 2019 or later). Excel Online and the mobile app can open it for viewing, but some array formulas and dropdown interactions behave better on desktop. It hasn't been tested in LibreOffice Calc or Google Sheets; since the formulas are standard it should import, but conditional formatting and charts may need manual adjustment.
7. **First use.** Before entering real data, follow the [step-by-step usage guide](#step-by-step-usage-guide) to register at least one test employee and confirm the traffic light and dashboards calculate as expected for your team.

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

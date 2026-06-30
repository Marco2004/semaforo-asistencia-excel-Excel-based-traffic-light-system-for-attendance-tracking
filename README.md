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

Contiene los registros de asistencia.

Ejemplo ficticio:

| FECHA | No. EMP | ENTRADA | SALIDA | SEMAFORO |
| --- | --- | --- | --- | --- |
| 01/06/2026 | 7001 | 08:00 | 17:00 | VERDE |
| 01/06/2026 | 7002 | 08:12 | 17:00 | AMARILLO |
| 02/06/2026 | 7003 | - | - | FALTA |

### Hojas de supervisor

Muestran el resumen del equipo asignado:

- Total de registros verdes.
- Total de registros amarillos.
- Total de registros rojos.
- Total de faltas.
- Porcentaje de cumplimiento.
- Promedio o conteo de horas segun el registro disponible.

## Clasificacion del semaforo

La clasificacion permite identificar rapidamente el estado de asistencia:

- `VERDE`: asistencia dentro del rango esperado.
- `AMARILLO`: retardo leve o alerta inicial.
- `ROJO`: retardo mayor.
- `ROJO FUERTE`: incumplimiento mas severo.
- `FALTA`: ausencia o registro incompleto segun la regla configurada.

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


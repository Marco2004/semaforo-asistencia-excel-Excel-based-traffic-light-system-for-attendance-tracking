# Tests / Pruebas

## Espanol

Este proyecto es un workbook de Excel, por lo que las pruebas principales son validaciones de estructura, privacidad y funcionamiento manual.

## Validaciones actuales

- GitHub Actions valida que existan los archivos profesionales requeridos.
- GitHub Actions valida que el workbook demo este presente.
- GitHub Actions revisa nombres de archivos que puedan indicar datos privados accidentales.

## Validaciones manuales recomendadas

- Abrir el workbook en Microsoft Excel.
- Confirmar que no hay macros inesperadas.
- Revisar que `REGISTRO`, `PERSONAL`, `NORMALIDAD` y tableros existan.
- Probar que `SEMAFORO` calcule estados esperados.
- Confirmar que las novedades sobrescriben la clasificacion normal.
- Confirmar que no hay datos reales.

## English

This project is an Excel workbook, so the main tests are structure, privacy, and manual functionality validations.

## Current validations

- GitHub Actions validates that required professional files exist.
- GitHub Actions validates that the demo workbook is present.
- GitHub Actions checks filenames that could indicate accidental private data.

## Recommended manual validations

- Open the workbook in Microsoft Excel.
- Confirm that there are no unexpected macros.
- Verify that `REGISTRO`, `PERSONAL`, `NORMALIDAD`, and dashboards exist.
- Test that `SEMAFORO` calculates expected states.
- Confirm that exceptions override normal classification.
- Confirm that no real data is included.

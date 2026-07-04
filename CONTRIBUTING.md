# Contributing / Guia de Contribucion

## Espanol

Gracias por tu interes en mejorar este proyecto. Este repositorio contiene una demo publica de un workbook de Excel, por lo que las contribuciones deben cuidar especialmente la privacidad de datos.

## Como contribuir

1. Haz fork del repositorio.
2. Clona tu fork.
3. Crea una rama descriptiva.
4. Realiza los cambios.
5. Revisa que no existan datos reales o sensibles.
6. Haz commit con un mensaje claro.
7. Haz push a tu rama.
8. Abre un Pull Request.

Ejemplo:

```powershell
git checkout -b feature/mejora-documentacion
git add .
git commit -m "Mejorar documentacion del workbook"
git push origin feature/mejora-documentacion
```

## Estilo de cambios

- Mantener la documentacion en espanol e ingles cuando aplique.
- Usar nombres claros para archivos y secciones.
- No subir archivos con datos reales.
- No modificar el workbook original sin explicar el cambio.
- Mantener formulas, rangos y hojas documentadas si se actualiza el Excel.

## Pruebas y revision

Antes de abrir un Pull Request:

- Abre el workbook en Microsoft Excel.
- Verifica que las formulas calculen correctamente.
- Confirma que no haya macros inesperadas.
- Revisa que `README.md`, `SECURITY.md` y `docs/WORKBOOK.md` sigan actualizados.
- Ejecuta los checks de GitHub Actions si estan disponibles.

## Pull Requests

Un Pull Request debe incluir:

- Descripcion clara del cambio.
- Motivo del cambio.
- Evidencia de prueba o revision manual.
- Confirmacion de que no se agregaron datos reales.

---

## English

Thank you for your interest in improving this project. This repository contains a public demo Excel workbook, so contributions must pay special attention to data privacy.

## How to contribute

1. Fork the repository.
2. Clone your fork.
3. Create a descriptive branch.
4. Make your changes.
5. Confirm that no real or sensitive data is included.
6. Commit with a clear message.
7. Push your branch.
8. Open a Pull Request.

Example:

```powershell
git checkout -b feature/documentation-improvement
git add .
git commit -m "Improve workbook documentation"
git push origin feature/documentation-improvement
```

## Change style

- Keep documentation in Spanish and English when applicable.
- Use clear names for files and sections.
- Do not upload files with real data.
- Do not modify the original workbook without explaining the change.
- Keep formulas, ranges, and sheets documented when updating the Excel file.

## Testing and review

Before opening a Pull Request:

- Open the workbook in Microsoft Excel.
- Verify that formulas calculate correctly.
- Confirm that there are no unexpected macros.
- Review that `README.md`, `SECURITY.md`, and `docs/WORKBOOK.md` remain up to date.
- Run GitHub Actions checks when available.

## Pull Requests

A Pull Request should include:

- Clear description of the change.
- Reason for the change.
- Testing or manual review evidence.
- Confirmation that no real data was added.

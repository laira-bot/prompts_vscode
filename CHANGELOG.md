# Changelog

Todos los cambios notables de este repositorio se documentan en este archivo.

El formato se basa en [Keep a Changelog](https://keepachangelog.com/es-ES/1.1.0/),
y este proyecto usa un versionado simple por fecha dado que es una guía de
consulta en evolución continua, no un paquete de software versionado.

## [Unreleased]

### Added
- `LICENSE` — se adopta Creative Commons Attribution 4.0 International (CC BY 4.0) para el contenido del repositorio.
- `CHANGELOG.md` — este archivo, para llevar registro de cambios relevantes en la guía.

### Changed
- Se fusionaron `guia.md` y `guia-copilot-vscode.md` (contenido redundante) en un único documento: `guia-copilot-vscode.md`. Ver PR #1.

### Removed
- `guia.md` — contenido incorporado a `guia-copilot-vscode.md`.

## [2026-07-06] - Versión inicial

### Added
- `README.md` — flujo de implementación de un proyecto con el entorno agéntico (`/new`, `/init`, `/create-instructions`).
- `guia-copilot-vscode.md` — guía de creación y desarrollo de proyectos con GitHub Copilot.
- `guia.md` — guía técnica alternativa del ciclo de vida del proyecto con Copilot.
- `archivos-objetivos-especificaciones.md` — cómo integrar `objetivos.md`/`especificaciones.md` como contexto para Copilot.
- `creacion-objetivos-especificaciones-proyecto.md` — plantillas para generar `objetivos-proyecto.md` y `especificaciones-proyecto.md`.
- `instrucciones-y-prompts-para-agentes.md` — diferencias entre `/init` y `/create-instructions`, y meta-prompt generador de ambos.

# LMS FECA — Plataforma de gestión de cursos

Implementación de un LMS institucional sobre **Moodle 5.2**.

## Stack

- Moodle 5.2 (rama `MOODLE_502_STABLE`)
- PHP 8.3 / Apache 2.4
- MariaDB 10.11
- Docker + Docker Compose (solo entorno local)
- Producción: NEUBOX, plan GP-600 (AlmaLinux 9.4 + cPanel)

## Estructura

| Carpeta | Contenido | Versionado |
|---|---|---|
| `docker/` | Dockerfile y configuración de PHP | Sí |
| `docs/` | Requerimientos y documentación técnica | Sí |
| `plugins/` | Plugins desarrollados para este proyecto | Sí |
| `scripts/` | Utilidades de instalación y mantenimiento | Sí |
| `moodle/` | Core de Moodle (clon independiente) | No |
| `moodledata/` | Datos de usuarios y caché | No |

## Reglas del proyecto

1. **Nunca se modifica el core de Moodle.** Toda personalización va en un plugin.
2. `config.php` y `.env` no se versionan; usar los archivos `.example` como plantilla.

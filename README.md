# Proyecto-Integrador
Nuestro Proyecto Integrador se basa en crear una plataforma (SIGABU) para fortalecer la gestión integral de los procesos de salud mental, apoyo psicosocial e inclusión universitaria.

## Reglas de Colaboración

Este proyecto sigue el modelo **GitFlow**, elegido por dos razones propias del contexto de SIGABU: (1) el sistema maneja **datos sensibles de salud mental** bajo la Ley 1581 de 2012, por lo que se necesita un flujo con etapas de estabilización antes de que cualquier cambio llegue a producción; y (2) el proyecto se compone de **módulos con ciclos de vida distintos** (backend/BD, app móvil, IA/NLP, QA), lo que se beneficia de ramas de larga duración que permiten integrar y probar cada módulo de forma controlada antes de liberarlo.

### Estructura de ramas

| Rama | Propósito | Reglas |
|---|---|---|
| `main` | Código en producción. Siempre estable y desplegable. | Protegida. Solo recibe merges desde `release/*` o `hotfix/*` vía Pull Request aprobado. |
| `develop` | Integración continua del trabajo de todo el equipo. | Protegida. Recibe merges desde `feature/*` vía Pull Request. |
| `feature/<módulo>-<descripción>` | Desarrollo de una funcionalidad puntual. | Se crea desde `develop`. Ejemplos: `feature/backend-auth-roles`, `feature/ia-transcripcion`, `feature/movil-agendamiento`. |
| `release/<versión>` | Preparación de una nueva versión (pruebas finales, ajustes menores). | Se crea desde `develop`. Al cerrarse, se mergea a `main` y a `develop`. |
| `hotfix/<descripción>` | Corrección urgente sobre producción. | Se crea desde `main`. Al cerrarse, se mergea a `main` y a `develop`. |

### Convención de nombres

- Ramas: minúsculas, separadas por guiones, con prefijo del módulo responsable (`backend-`, `movil-`, `ia-`, `qa-`).
- Commits: formato `tipo: descripción breve` (ej. `feat: agregar endpoint de consentimiento informado`, `fix: corregir clasificación de riesgo en NLP`, `docs: actualizar README`).

### Proceso de Pull Request

1. Antes de abrir un PR, la rama debe estar actualizada respecto a su rama base (`develop` o `main`) para evitar conflictos.
2. Todo PR hacia `develop` o `main` requiere **al menos 1 revisión aprobada** antes de poder mergearse (configurado como protección de rama en GitHub).
3. Dado que SIGABU procesa información sensible de salud, cualquier PR que toque **autenticación, control de acceso, almacenamiento de datos o el pipeline de IA/NLP** debe ser revisado obligatoriamente por el integrante responsable de Backend/BD o QA, según corresponda, sin importar quién más lo apruebe.
4. El autor de un PR no puede aprobar su propio cambio.
5. Los conflictos y comentarios de revisión deben resolverse antes del merge; no se permite mergear con revisiones pendientes de respuesta.

### Responsabilidades por rol (equipo SIGABU)

| Integrante | Rol | Revisa principalmente |
|---|---|---|
| Juan Esteban Vera | Backend / BD | Seguridad, control de acceso, modelo de datos |
| Jimy Fabian Ramírez | Frontend móvil | UX/UI, integración con la API |
| Salomón Galviz | IA / NLP | Transcripción, análisis semántico, clasificación de riesgo |
| Stiven Gonzalez | QA + Gestión | Pruebas, documentación, tablero, relación con Bienestar |

### Protección de la rama `main`

- Push directo deshabilitado: todo cambio debe llegar mediante Pull Request.
- Mínimo 1 aprobación requerida antes de mergear.
- Esta configuración aplica igualmente a `develop` como buena práctica adicional del equipo, dado el volumen de módulos en paralelo.

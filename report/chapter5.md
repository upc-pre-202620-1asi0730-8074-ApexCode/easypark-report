# Capítulo V: Product Implementation, Validation & Deployment

## 5.1. Software Configuration Management
### 5.1.1. Software Development Environment Configuration
Con el objetivo de garantizar un desarrollo fluido, estandarizado y consistente en todos los miembros del equipo ApexCodeSolutions, se ha definido el siguiente entorno de desarrollo para la startup EasyPark:

| Actividad                           | Producto           | Propósito / Uso                                                                                            |
| ----------------------------------- | ------------------ | ---------------------------------------------------------------------------------------------------------- |
| Product Management                  | Trello             | Gestión del Product Backlog, planificación de Sprints y seguimiento de tareas.                             |
| Requirements Management             | Miro / UXPRESSIA   | Elaboración de descubrimiento (User persona, Empathy maps, Journey maps) para la definición de requisitos. |
| UX/UI Design                        | Figma              | Diseño de la guía de estilo, prototipos de baja fidelidad (wireframes) y alta fidelidad (mockups).         |
| User Flows & Wireflows              | LucidChart         | Elaboración de Wireflows y Userflows.                                                                      |
| Class Diagrams & Data Base Design   | PlantUML           | Elaboración de diagramas de clases y diseño de base de datos.                                              |
| Software Development (Landing Page) | Visual Studio Code | IDE para el desarrollo de la Landing Page con HTML5, CSS y JS.                                             |
| Version Control                     | Github / Rider     | Alojamiento de repositorios y gestión de versiones aplicando Gitflow y Conventional Commits.               |
| Documentation                       | Markdown           | Documentación del reporte del proyecto.                                                                    |

### 5.1.2. Source Code Management
El código fuente del proyecto se gestionará utilizando Git como sistema de control de versiones y GitHub como plataforma de alojamiento, bajo una organización pública. Se adoptará un enfoque estructurado que favorezca la colaboración, la modularidad y el despliegue continuo mediante repositorios independientes para cada componente del sistema.

**Estrategia de Ramas (GitFlow)**

Se implementará un flujo de trabajo basado en GitFlow con el objetivo de garantizar la estabilidad y trazabilidad del desarrollo:

**- main**: Rama principal que contiene únicamente código estable, probado y desplegado en producción. Cada versión liberada deberá estar debidamente etiquetada.

**- develop**: Rama de integración contínua donde se consolidan los avances antes de su liberación a producción.

**- feature** [nombre]: Ramas temporales creadas a partir de develop para el desarrollo de nuevas funcionalidades o User Stories. Una vez finalizadas, se integran nuevamente a develop mediante un Pull Request (PR).

**- hotifx** [nombre]: Ramas destinadas a la corrección de errores críticos detectados en producción (main), que requieren una solución inmediata.


**Convención de Commits (Conventional Commits)**

Para mantener un historial claro, consistente y facilitar la generación automática de changelogs, todos los commits deberán seguir el estándar de Conventional Commits:

**Tipos permitidos**

**-feat**: Nueva funcionalidad
(ej. feat(ordering): add automated order validation policy)

**-fix**: Corrección de errores
(ej. fix(auth): resolve token expiration on mobile devices)

**-docs**: Cambios en documentación
(ej. docs(interviews): update stakeholder interview records)

**-style**: Cambios de formato que no afectan la lógica del código (espacios, indentación, etc.)

### 5.1.3. Source Code Style Guide & Conventions

- **Naming Conventions:**
    - Variables y Métodos: camelCase (ej. `currentTemperature`).
    - Clases e Interfaces: PascalCase (ej. `LaboratoryController`).
    - Constantes: UPPER_CASE (ej. `MAX_GAS_LEVEL`).
    - Archivos CSS/HTML/Componentes: kebab-case (ej. `dashboard-view.component.html`).

- **Guías de Estilo por Lenguaje:**
    - Java: Google Java Style Guide.
    - TypeScript/Angular: Angular Coding Style Guide y Google TypeScript Style Guide.
    - HTML/CSS: Google HTML/CSS Style Guide.
### 5.1.4. Software Deployment Configuration

En esta sección se especifica la configuración y los pasos necesarios para el despliegue de cada uno de los productos que conforman la solución **EasyPark**. Se ha adoptado un enfoque de **Continuous Deployment (CD)** para asegurar que los cambios validados en los repositorios de GitHub se reflejen automáticamente en los entornos de producción mediante **GitHub Actions**.

| Producto | Entorno de Despliegue | Pipeline / Herramienta |
|---|---|---|
| **Landing Page** |  GitHub Pages | GitHub Actions |

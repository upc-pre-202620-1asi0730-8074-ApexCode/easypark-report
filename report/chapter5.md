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

## 5.2 Landing Page, Services & Applications Implementation.

En esta sección se describe el proceso de implementación del producto EasyPark, incluyendo el desarrollo, pruebas, documentación y despliegue del Landing Page. Para este avance, se implementó la primera versión del Landing Page, orientada a presentar la propuesta de valor del sistema. El desarrollo se realizó utilizando tecnologías web y GitHub como herramienta de control de versiones.

### 5.2.1 Sprint 1

En esta sección se presenta el avance del Sprint 1 en términos de desarrollo del producto y trabajo colaborativo del equipo. Durante este sprint se realizó la implementación de la primera versión del Landing Page de EasyPark, enfocada en presentar la propuesta de valor del sistema.

Asimismo, se incluyen las evidencias relacionadas con la planificación del sprint, la organización del equipo, el backlog definido, el desarrollo realizado, así como los resultados obtenidos y la colaboración durante el proceso.

#### 5.2.1.1 Sprint Planning 1.
En esta sección se describen los principales acuerdos y definiciones realizadas durante el Sprint Planning del Sprint 1, enfocado en la implementación del Landing Page de EasyPark.

<table>
  <tr>
    <th>Sprint #</th>
    <td>Sprint 1</td>
  </tr>

  <tr>
    <th colspan="2">Sprint Planning Background</th>
  </tr>

  <tr>
    <td>Date</td>
    <td>2026 - 09 - 15</td>
  </tr>

  <tr>
    <td>Time</td>
    <td>17:30</td>
  </tr>

  <tr>
    <td>Prepared By</td>
    <td>Evangelista Ygnacio, Sergio Joaquin</td>
  </tr>

  <tr>
    <td>Attendees (to planning meeting)</td>
    <td>
      Saravia Huaricancha, Arturo Axel Negón Muñoz, Cayo Manuel Stefano Martín Farón,
      Alexis Sebastián Lucas Córdova, Alvar
    </td>
  </tr>

  <tr>
    <td>Sprint 1 Review Summary</td>
    <td>
      Durante el Sprint 1 se logró implementar correctamente el Landing Page
      responsive de EasyPark, incluyendo navegación entre secciones, adaptación
      móvil y soporte multilenguaje. Además, el equipo consolidó la estructura
      base del frontend y definió estándares iniciales de trabajo colaborativo
      utilizando GitFlow y Trello para la gestión de tareas.
    </td>
  </tr>

  <tr>
    <td>Sprint 1 Retrospective Summary</td>
    <td>
      El equipo identificó como principal fortaleza la buena distribución de
      tareas y la comunicación constante durante el desarrollo del Sprint 1.
      Sin embargo, se detectaron pequeños retrasos en la integración de
      componentes y validaciones responsive, por lo que para este sprint se
      acordó mejorar la coordinación durante los merges y aumentar la
      frecuencia de revisiones entre integrantes.
    </td>
  </tr>
</table>

#### 5.2.1.2 Aspect Leaders and Collaborators.

En esta sección se define la matriz de liderazgo y colaboración (LACX) del Sprint 1, la cual permite identificar claramente las responsabilidades de cada integrante del equipo en los distintos aspectos del desarrollo.

Para este sprint, los principales aspectos considerados están relacionados con la implementación del Landing Page,incluyendo la estructura visual, navegación entre secciones y adaptación responsive.

Estos aspectos fueron definidos en base a las funcionalidades abordadas en el sprint y permiten organizar de manera eficiente el trabajo del equipo.

| **Team Member (Last Name, First Name)** | **GitHub Username** | **Estructura del Landing Page** | **Navegación entre Secciones** | **Diseño Responsive** |
|---|---|---|---|---|
| Evangelista Ygnacio, Sergio Joaquin | Sergi9017 | C | L | C |
| Saravia Huaricancha, Arturo Axel | thunder053 | L | C | C |
| Negrón Muñoz, Cayo Manuel Stefano | fano1106-n | C | C | C |
| Martín Farro, Alexis Sebastián | axismf | C | C | C |
| Lucas Córdova, Alvar | Alvarl C | C | C | L |

#### 5.2.1.3 Sprint Backlog 1.

El Sprint 1 tuvo como objetivo principal la implementación del Landing Page de EasyPark, permitiendo presentar la propuesta de valor del sistema mediante una interfaz clara, estructurada y accesible.
Para la gestión del Sprint Backlog, se utilizó una herramienta de control de tareas basada en tableros (Trello), donde se organizaron los User Stories y sus respectivos tasks en columnas según su estado de avance.
A continuación, se presenta el tablero correspondiente al Sprint 1 junto con su enlace:
https://trello.com/b/KxGrDhN2/sprintseasypark


| Sprint # | User Story                                         | Work-Item / Task                 | Descripción                                                            | Estimación (Horas) | Assigned To | Status |
|---|----------------------------------------------------|----------------------------------|------------------------------------------------------------------------|---:|---|---|
| Sprint 1 | US-41 Conocer EasyPark                             | Setup Static Proj                | Inicializar el repositorio                                             | 4 | Sergio | Done |
| Sprint 1 | US-42 Conocer beneficios para conductores          | Maquetar sección "For Drivers"   | Crear contenedor y tarjetas interactivas                               | 3 | Arturo | Done |
| Sprint 1 | US-43 Conocer beneficios para administradores      | Maquetar sección "For Operators" | Desarrollar el layout de la sección                                    | 3 | Alvar | Done |
| Sprint 1 | US-44 Conocer funcionalidades principales          | Grid de funcionalidades          | Implementar una cuadrícula responsive                                  | 4 | Alexis | Done |
| Sprint 1 | US-45 Conocer funcionamiento de reservas           | Maquetar "Step-by-step"          | Crear sección de pasos secuenciales que muestran el flujo del conductor | 3 | Cayo | Done |
| Sprint 1 | US-46 Conocer gestión digital para administradores | Vista previa de Dashboard        | Colocar mock-up del panel                                              | 2 | Alexis | Done |
| Sprint 1 | US-47 Conocer integración progresiva con IoT       | Banner informativo               | Implementar bloque destacado que explica la adopción de hardware       | 2 | Sergio | Done |
| Sprint 1 | US-48 Consultar preguntas frecuentes               | Estructurar FAQ                  | Maquetar lista de preguntas                                            | 4 | Cayo | Done |
| Sprint 1 | US-49 Contactar con EasyPark                       | Maquetar footer                  | Añadir información de contacto                                         | 2 | Alvar | Done |
| Sprint 1 | US-50 Acceder a la aplicación web                  | Header / Navbar                  | Implementar la barra de navegación superior                            | 4 | Arturo | Done |
![Backlog - Trello.png](../assets/images/Backlog%20-%20Trello.png)

#### 5.2.1.4 Development Evidence for Sprint Review.

#### 5.2.1.5 Execution Evidence for Sprint Review.

1. Captura de la Landing Page
![Landing Page - Register Button.png](../assets/images/Landing%20Page%20-%20Register%20Button.png)

2. Captura del apartado "Quienes somos": 
![Landing Page - Info.png](../assets/images/Landing%20Page%20-%20Info.png)

3. Captura del apartado "Beneficios":
![Landing Page - Benefits.png](../assets/images/Landing%20Page%20-%20Benefits.png)

4. Captura del apartado "Funcionalidades":
![Landing Page - Functionalities.png](../assets/images/Landing%20Page%20-%20Functionalities.png)

5. Captura del apartado "Precios":
![Landing Page - Plans.png](../assets/images/Landing%20Page%20-%20Plans.png)

6. Captura del apartado "Testimonios":
![Landing Page - Testimonials.png](../assets/images/Landing%20Page%20-%20Testimonials.png)

7. Captura del apartado "FAQ (frequently asked questions)":
![Landing Page - FAQ.png](../assets/images/Landing%20Page%20-%20FAQ.png)

8. Captura del apartado "Contacto" 
![Landing Page - Contact.png](../assets/images/Landing%20Page%20-%20Contact.png)

#### 5.2.1.6 Services Documentation Evidence for Sprint Review.
N/A. Durante el Sprint 1 el esfuerzo de desarrollo se enfocó exclusivamente en la creación del sitio web estático promocional (Landing Page), por lo que aún no se han implementado APIs RESTful ni Endpoints backend que requieran ser documentados a través de Swagger/OpenAPI. Esta documentación se estructurará a partir del Sprint 2.

#### 5.2.1.7 Software Deployment Evidence for Sprint Review.
Para el despliegue continuo (CI/CD) de este Sprint, se configuró el entorno de GitHub Pages conectado directamente al repositorio de GitHub del Landing Page estático, permitiendo publicaciones automáticas y ultra-rápidas con cada PR fusionado en la rama main.:

* Landing Page (Estática): Mantenida y automatizada mediante GitHub Pages. https://upc-pre-202620-1asi0730-8074-apexcode.github.io/easypark-website/

#### 5.2.1.8 Team Collaboration Insights during Sprint.

Todos los miembros del equipo han participado activamente en la implementación de los productos del Sprint 1, lo cual se evidencia mediante los reportes de actividad y contribución del repositorio de GitHub de la organización Apex Code Solutions.
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
| Database Management                 | MySQL 8 / MySQL Workbench     | Motor de base de datos relacional y herramienta de administración y consulta.               |
| API Documentation                   | OpenAPI / Scalar           |  Documento OpenAPI generado por el propio API y explorado de forma interactiva mediante Scalar.                                                                    |
| Software Development (Web Services) | JetBrains Rider           |  IDE para el desarrollo del RESTful API con C# y ASP.NET Core 10.                                   |
| Containerization                    | Docker Desktop / Docker Compose | Ejecución local de MySQL 8.4 y del RESTful API en contenedores; imagen del API para el despliegue. |
| Automated Testing                   | xUnit / WebApplicationFactory / SQLite en memoria | Pruebas de dominio e integración del RESTful API (`dotnet test`). |
| Cloud Database                      | Aiven for MySQL | Base de datos MySQL remota con TLS para el entorno desplegado. |
| Web Services Hosting                | Render (Docker) | Publicación del contenedor del RESTful API con URL HTTPS. |
| Web Application Hosting             | Firebase Hosting | Publicación de la Web Application compilada con Vite. |

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
    - **C# (RESTful API):** clases, interfaces (prefijo `I`), métodos, propiedades y constantes en PascalCase (ej. `ReservationCommandService`, `IParkingSpaceRepository`); variables locales y parámetros en camelCase (ej. `plateNumber`).
    - **JavaScript (Web Application):** variables y funciones en camelCase (ej. `currentReservation`); clases en PascalCase (ej. `AccessMovement`); constantes de módulo en UPPER_CASE.
    - **Archivos Vue, CSS y HTML:** kebab-case (ej. `access-form.vue`, `parking-stay-list.vue`).
    - **Base de datos:** tablas y columnas en `snake_case` y en inglés, según 4.8.
- **Guías de estilo por lenguaje:**
    - C# y ASP.NET Core: Microsoft C# Coding Conventions.
    - JavaScript y Vue 3: Vue Style Guide oficial.
    - HTML/CSS: Google HTML/CSS Style Guide.
- **Organización del código:** cada bounded context se organiza en las capas `Domain`, `Application`, `Infrastructure` e `Interfaces` en el backend, y en `domain`, `application`, `infrastructure` y `presentation` en el frontend.
- **Commits:** Conventional Commits con alcance por bounded context (ej. `feat(reservations): add create reservation endpoint`).
### 5.1.4. Software Deployment Configuration

En esta sección se especifica la configuración y los pasos necesarios para el despliegue de cada uno de los productos que conforman la solución **EasyPark**. Se ha adoptado un enfoque de **Continuous Deployment (CD)** para asegurar que los cambios validados en los repositorios de GitHub se reflejen automáticamente en los entornos de producción mediante **GitHub Actions**.

| Producto | Entorno de despliegue | Pipeline / Herramienta | Estado (AV2) |
|---|---|---|---|
| **Landing Page** | GitHub Pages | GitHub Actions | Desplegado. Pendiente: enlazar *Log in / Sign up* con la Web Application (T3-15) |
| **Web Application (SPA)** | Firebase Hosting | `npm ci`, `npm run build` y `firebase deploy --only hosting --project easypark-5ffb2` | Desplegada: https://easypark-5ffb2.web.app |
| **RESTful Web Services** | Render (ASP.NET Core 10) | Docker, CORS, JWT, migraciones de EF Core y conexion MySQL TLS | Desplegado: https://easypark-backend-qheu.onrender.com |
| **Base de datos** | Aiven for MySQL | Migraciones `20261025150000_InitialCreate` y `20261102000000_ExtendedFeatures`; TLS obligatorio | Servicio accesible desde Render; esquema previsto de 15 tablas |

Consideraciones de los planes gratuitos (consultadas el 25/10/2026): Render suspende el servicio tras 15 minutos sin tráfico y tarda cerca de un minuto en reactivarlo; Aiven puede apagar un servicio gratuito sin actividad y permite encenderlo de nuevo desde su consola; Firebase Spark ofrece 10 GB de almacenamiento y 360 MB/día de transferencia.

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
      Saravia Huaricancha, Arturo Axel; 
      Negrón Muñoz, Cayo Manuel Stefano; 
      Martín Farro, Alexis Sebastián;
      Lucas Córdova, Alvar;
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
   ![tb1 Landing Page - Inicio.png](../assets/images/tb1%20Landing%20Page%20-%20Inicio.png)

2. Captura del apartado "Quienes somos":
   ![tb1 Landing Page - About us.png](../assets/images/tb1%20Landing%20Page%20-%20About%20us.png)

3. Captura del apartado "Beneficios":
   ![tb1 Landing Page - Benefits.png](../assets/images/tb1%20Landing%20Page%20-%20Benefits.png)

4. Captura del apartado "Funcionalidades":
   ![tb1 Landing Page - Features.png](../assets/images/tb1%20Landing%20Page%20-%20Features.png)

5. Captura del apartado "Reservas":
   ![tb1 Landing Page - Bookings.png](../assets/images/tb1%20Landing%20Page%20-%20Bookings.png)

6. Captura del apartado "Precios":
   ![tb1 Landing Page -Pricing.png](../assets/images/tb1%20Landing%20Page%20-Pricing.png)

7. Captura del apartado "Technology":
   ![tb1 Landing Page - Technology.png](../assets/images/tb1%20Landing%20Page%20-%20Technology.png)

8. Captura del apartado "Nuestro Equipo":
   ![tb1 Landing Page - Our Team.png](../assets/images/tb1%20Landing%20Page%20-%20Our%20Team.png)

9. Captura del apartado "Contacto"
   ![tb 1 Landing Page -Contact.png](../assets/images/tb%201%20Landing%20Page%20-Contact.png)

10. Captura del apartado "Pie de pagina"
    ![tb1 Landing Page - Footer.png](../assets/images/tb1%20Landing%20Page%20-%20Footer.png)

#### 5.2.1.6 Services Documentation Evidence for Sprint Review.
N/A. Durante el Sprint 1 el esfuerzo de desarrollo se enfocó exclusivamente en la creación del sitio web estático promocional (Landing Page), por lo que aún no se han implementado APIs RESTful ni Endpoints backend que requieran ser documentados a través de Swagger/OpenAPI. Esta documentación se estructurará a partir del Sprint 2.

#### 5.2.1.7 Software Deployment Evidence for Sprint Review.
Para el despliegue continuo (CI/CD) de este Sprint, se configuró el entorno de GitHub Pages conectado directamente al repositorio de GitHub del Landing Page estático, permitiendo publicaciones automáticas y ultra-rápidas con cada PR fusionado en la rama main.:

* Landing Page (Estática): Mantenida y automatizada mediante GitHub Pages. https://upc-pre-202620-1asi0730-8074-apexcode.github.io/easypark-website/

#### 5.2.1.8 Team Collaboration Insights during Sprint.

Todos los miembros del equipo han participado activamente en la implementación de los productos del Sprint 1, lo cual se evidencia mediante los reportes de actividad y contribución del repositorio de GitHub de la organización Apex Code Solutions.

### 5.2.2 Sprint 2

#### 5.2.2.1 Sprint Planning

En esta sección se describen los principales acuerdos y definiciones realizadas durante el Sprint Planning del Sprint 2, enfocado en la implementación del Frontend Web Application de EasyPark.

<table>
  <tr>
    <th>Sprint #</th>
    <td>Sprint 2</td>
  </tr>

  <tr>
    <th colspan="2">Sprint Planning Background</th>
  </tr>

  <tr>
    <td>Date</td>
    <td>2026 - 10 - 04</td>
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
      Saravia Huaricancha, Arturo Axel; 
      Negrón Muñoz, Cayo Manuel Stefano; 
      Martín Farro, Alexis Sebastián;
      Lucas Córdova, Alvar;
    </td>
  </tr>

  <tr>
    <td>Sprint 1 Review Summary</td>
    <td>
      Durante el Sprint 1 se logró implementar correctamente el Landing Page
      responsive de EasyPark, incluyendo navegación entre secciones, adaptación
      móvil y soporte multilenguaje. La revisión del AV1 se observó que que la Landing page no manejaba multiidioma, en el BenchMark no se encontraban todos los precios, no se habían colocado Tecnical Stories, no se debían colocar Story Points de 8, tambien realizar una revisión de la BD y separar el capítulo de conclusiones y recomendaciones. 
    </td>
  </tr>

  <tr>
    <td>Sprint 1 Retrospective Summary</td>
    <td>
      El equipo mejoró en cuanto participación y hubo mejor comunicación entre los  miembros. Se acordó que cada integrante lidere un bounded context de la Frontend Application en su propia rama y que las correciones de la AV1 se resuelvan dentro del Sprint 2.
    </td>
  </tr>

<tr>
    <td>Sprint Goal & User Stories</td>
    <td>
      Our focus is on que el conductor pueda buscar y reservar un espacio, y el personal operativo pueda registrar el ingreso, la ocupación y la salida de los vehículos en la plataforma.
      We believe it delivers reducción en el tiempo de búsqueda para conductores y mayor control operativo to los administradores de estacionamientos independientes.
      This will be confirmed when el conductor complete una reserva en la aplicación y el administrador pueda visualizar el cambio de estado (a "Ocupado" o "Reservado") en su panel de control en tiempo real.
    </td>
  </tr>

<tr>
    <td>Sprint 2 Velocity</td>
    <td>
    34
    </td>
  </tr>

<tr>
    <td>Sum of Story Points</td>
    <td>
    34
    </td>
  </tr>

</table>

#### 5.2.2.2 Aspect Leaders and Collaborators
Para el Sprint 2, el liderazgo se distribuyó según los Bounded Contexts definidos en el Design-Level EventStorming. La arquitectura se basa en un monolito modular con un contenedor Frontend en Vue 3 y un Backend RESTful API en ASP.NET Core.


| **Team Member (Last Name, First Name)** | **GitHub Username** | **Profile and Vehicles** | **Notifications** | **Monitoring and Alerts** | **Parking Management** | **Analytics and Reporting** | **Reservations** | **Access Control** |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Evangelista Ygnacio, Sergio Joaquin | Sergi9017 | C | C | C | L | C | C | C |
| Saravia Huaricancha, Arturo Axel | thunder053 | L | C | C | C | C | C | L |
| Negrón Muñoz, Cayo Manuel Stefano | fano1106-n | C | L | C | C | C | C | C |
| Martín Farro, Alexis Sebastián | axismf | C | C | L | C | C | C | C |
| Lucas Córdova, Alvar | Alvarl  | C | C | C | C | L | L | C |

#### 5.2.2.3 Sprint Backlog 2
El Sprint 2 incluye las historias críticas del Product Backlog (Epics 1, 2 y 3) que quedaron en estado To-Do durante el Sprint 1 como se puede observar en el Trello:
https://trello.com/b/KxGrDhN2/sprintseasypark

**Tablero del proyecto en Trello**. El Product Backlog contiene las User Stories y Technical Stories pendientes, y las listas de cada Sprint registran el avance de sus historias.

<table>
  <tr>
    <th>Sprint #</th>
    <td>Sprint 2</td>
  </tr>

  <tr>
    <th> User Story </th>
    <th> </th>
    <th> Work-Item / Task </th>
  </tr>

  <tr>
    <td>Id</td>
    <td>Title</td>
    <td>Description</td>
    <td>Estimation(Hours)</td>
    <td>Assigned To</td>
    <td>Status(To-do/ In-Process / To-Review / Done)</td>
  </tr>

  <tr>
    <td> US-01 </td>
    <td> Buscar Estacionamiento por ubicación </td>
    <td> Como conductor, deseo buscar estacionamientos cercanos a mi destino para evaluar opciones disponibles.</td>
    <td> 6</td>
    <td> Saravia, Arturo</td>
    <td>Done</td>
  </tr>

  <tr>
    <td> US-03 </td>
    <td> Consultar disponibilidad de espacios</td>
    <td> Como conductor, deseo ver la disponibilidad en tiempo real para asegurar que encontraré un lugar libre.</td>
    <td> 5</td>
    <td> Evangelista, Sergio</td>
    <td> Done</td>
  </tr>

  <tr>
    <td> US-11 </td>
    <td> Reservar espacio</td>
    <td> Como conductor, deseo reservar un espacio para tener mayor certeza de encontrar estacionamiento al llegar.</td>
    <td> 8</td>
    <td> Lucas, Alvar</td>
    <td> Done</td>
  </tr>

  <tr>
    <td> US-19 </td>
    <td> Registrar ingreso de vehículo</td>
    <td> Como administrador, deseo registrar el ingreso (check-in) de un vehículo para iniciar el cómputo de su permanencia.</td>
    <td> 6</td>
    <td> Martin, Alexis</td>
    <td> Done</td>
  </tr>

  <tr>
    <td> US-20</td>
    <td> Registrar salida de vehículo</td>
    <td> Como administrador, deseo registrar la salida (check-out) de un vehículo para liberar el espacio utilizado.</td>
    <td> 5</td>
    <td> Negrón, Cayo</td>
    <td> Done</td>
  </tr>

  <tr>
    <td> US-21 </td>
    <td> Consultar ocupación actual</td>
    <td> Como administrador, deseo ver la ocupación de mis zonas (ej. "Zona A - Miraflores: 78%") para monitorear la capacidad.</td>
    <td> 5</td>
    <td> Saravia, Arturo</td>
    <td> Done</td>
  </tr>

  <tr>
    <td> TS-03 </td>
    <td> Servicio de disponibilidad</td>
    <td> Como Developer, deseo un endpoint REST para consultar los espacios libres según la zona.</td>
    <td> 6</td>
    <td> Evangelista, Sergio</td>
    <td> Done</td>
  </tr>

  <tr>
    <td> TS-05 </td>
    <td> Servicio de ingreso de vehículos</td>
    <td> Como Developer, deseo un endpoint POST para registrar el evento de ingreso y cambiar el estado del espacio.</td>
    <td> 6</td>
    <td> Lucas, Alvar</td>
    <td> Done</td>
  </tr>

</table>

![Product Backlog 2.png](../assets/images/Product%20Backlog%202.png)

#### 5.2.2.4 Development Evidence for Sprint Review.

En el Sprint 2 se implementó la primera versión de la Frontend Web Application en el repositorio, con Vue 3, PrimeVue, Pinia, Vue Router, vue-i18n y axios, en JavaScript. El código se organiza por bounded context, y cada uno se divide en las capas domain, application, infrastructure y presentation. Arturo Saravia preparó la base del proyecto.

En el repositorio se aplicaron las correcciones de AV1, como por ejemplo que ahora maneja multiidioma.
![tb1 Landing Page - Inicio.png](../assets/images/tb1%20Landing%20Page%20-%20Inicio.png)
Lading page:
https://upc-pre-202620-1asi0730-8074-apexcode.github.io/easypark-landing/index.html?lang=es

#### 5.2.2.5 Execution Evidence for Sprint Review.

Al cierre del Sprint 2, la Frontend Web Application v1.0.0 se encuentra publicada en: https://github.com/upc-pre-202620-1asi0730-8074-ApexCode/easypark-webapp.

La aplicación ofrece una experiencia distinta para cada rol: el operador (administrador) accede a un panel de control donde visualiza reportes y analíticas, supervisa el monitoreo y las alertas, gestiona las instalaciones y registra los accesos; por su parte, el conductor (usuario) cuenta con funcionalidades para buscar estacionamiento, realizar reservaciones, recibir notificaciones, y administrar su perfil junto con sus vehículos registrados. Las vistas que siguen se capturaron con los datos de la API REST simulada (json-server) y en idioma español; la aplicación puede cambiar a inglés desde el selector de idioma gracias al soporte de internacionalización configurado.

#### 5.2.2.6 Services Documentation Evidence for Sprint Review.

Durante este Sprint la Single Page Application consume una API RESTful simulada con json-server, que expone sus recursos bajo el prefijo /api/v1/* siguiendo las convenciones REST. El acceso está protegido mediante un token Bearer emitido por el módulo Identity and Access Management (IAM) durante el inicio de sesión, el cual es adjuntado automáticamente a cada petición por un interceptor de Axios. A continuación se documentan los endpoints implementados y consumidos por los bounded contexts desarrollados en este Sprint:

| **Recurso/Endpoint** | **Bounded Context** | **Verbos HTTP** | **Propósito** |
| :--- | :--- | :--- | :--- |
| /api/v1/authentication/sign-in | IAM | POST | Valida las credenciales y emite el token de sesión del usuario. |
| /api/v1/authentication/sign-up | IAM | POST | Registra una nueva cuenta (conductor u operador). |
| /api/v1/authentication/password | IAM | PUT | Actualiza la contraseña de la cuenta autenticada. |
| /api/v1/profiles | Profiles and Vehicles | GET, POST, PUT | Consulta y gestiona el perfil del conductor u operador. |
| /api/v1/vehicles | Profiles and Vehicles | GET, POST, PUT | Registra y administra los vehículos asociados a un perfil. |

Los demás recursos (parking-facilities, reservations, access-movements, alerts, etc.) se encuentran preconfigurados en la API simulada como contrato de datos para los bounded contexts que se desarrollarán en los siguientes Sprints.

El recorrido de la aplicación es el siguiente:

1.  Apartado de Acceso y registro digital ![EasyPark Admin Accesos y registro digital.png](../assets/images/EasyPark%20Admin%20Accesos%20y%20registro%20digital.png)
2.  Apartado de registro de usuario ![EasyPark Admin Sign In.png](../assets/images/EasyPark%20Admin%20Sign%20In.png)
3.  Apartado de Buscar estacionamiento ![EasyPark Admin Find Parking.png](../assets/images/EasyPark%20Admin%20Find%20Parking.png)
4.  Apartado de reservaciones ![EasyPark Admin My reservations.png](../assets/images/EasyPark%20Admin%20My%20reservations.png)
5.  Apartado de Notificaciones ![EasyPark Admin Notifications.png](../assets/images/EasyPark%20Admin%20Notifications.png)
6.  Apartado de monitoreo y alertas ![EasyPark Admin Monitoreo y alertas.png](../assets/images/EasyPark%20Admin%20Monitoreo%20y%20alertas.png)
7.  Apartado de Mi perfil tipo Admin ![EasyPark Admin Mi perfil.png](../assets/images/EasyPark%20Admin%20Mi%20perfil.png)
8.  Apartado de Mi perfil tipo Usuario ![EasyPark User My profile.png](../assets/images/EasyPark%20User%20My%20profile.png)
9.  Apartado de panel de control ![EasyPark Admin panel Control.png](../assets/images/EasyPark%20Admin%20panel%20Control.png)
10. Apartado de Reportes y analítica ![EasyPark Admin Reportes y Analitica.png](../assets/images/EasyPark%20Admin%20Reportes%20y%20Analitica.png)
11. Apartado de Registrar accesos ![EasyPark Admin Registrar acceso.png](../assets/images/EasyPark%20Admin%20Registrar%20acceso.png)
12. Apartado de Instalaciones ![EasyPark Admin Mis instalaciones.png](../assets/images/EasyPark%20Admin%20Mis%20instalaciones.png)


#### 5.2.2.7 Software Deployment Evidence for Sprint Review.

Frontend Web Application: La aplicación se construye con Vite (npm run build), generando artefactos estáticos optimizados que pueden previsualizarse con npm run preview. El Landing Page del Sprint 1 continúa publicado y automatizado mediante GitHub Pages.

Para el consumo de datos durante este Sprint se utiliza una API REST simulada con json-server (npm run fake-api), que expone los endpoints bajo /api/v1/* e incorpora un middleware de autenticación que emite y valida el token de sesión del módulo IAM. Esto permite validar los flujos de registro, inicio de sesión, gestión de perfil y administración de vehículos de extremo a extremo sin depender aún de infraestructura en la nube.

El despliegue de un backend productivo con base de datos relacional y hosting en la nube está planificado para los siguientes Sprints, una vez que los bounded contexts restantes del equipo estén implementados.

Analíticos de contribución del repositorio con respecto al sprint 2:

![Contribution Sprint2.png](../assets/Contribution%20Sprint2.png)

#### 5.2.2.8 Team Collaboration Insights during Sprint.

El equipo mantuvo un ritmo de trabajo organizado, repartiendo la carga por bounded contexts: en este Sprint se completaron IAM y Profiles and Vehicles, mientras los restantes avanzan en paralelo.

* Se respetó una arquitectura basada en Domain-Driven Design, estructurando cada bounded context en las capas domain/model, application, infrastructure y presentation, lo que mantuvo límites claros entre módulos y evitó que un contexto accediera directamente a la lógica de otro.
* Se reutilizaron los tokens de diseño y el preset personalizado de PrimeVue en componentes reutilizables de Vue, lo que permitió construir las vistas del conductor (inicio de sesión, registro y perfil) manteniendo total consistencia visual con el Landing Page desarrollado en el Sprint 1.
* El soporte de internacionalización (español e inglés) y el layout compartido se mantuvieron centralizados para garantizar coherencia en toda la aplicación.

### 5.2.3 Sprint 3

En esta sección se detalla la evolución del proyecto durante el Sprint 3, que marca la transición de la API simulada con json-server hacia un RESTful API real desarrollado en ASP.NET Core 10 con persistencia en MySQL. El alcance comprende los servicios web de los contextos Identity and Access Management, Profiles and Vehicles, Parking Management, Reservations y Access Control, la documentación del contrato con OpenAPI, el despliegue en la nube de los tres productos y la conexión de la Web Application con la nueva API.

#### 5.2.3.1 Sprint Planning 3

En esta sección se describen los acuerdos, antecedentes y objetivos establecidos durante la reunión de planificación del Sprint 3.

| Campo | Detalle |
|------|--------|
| **Sprint #** | Sprint 3 |
| **Sprint Planning Background** | [PENDIENTE: contexto de la reunión registrado por el equipo] |
| **Date** | 2026-10-20 |
| **Time** | 17:00 |
| **Location** | Reunión virtual |
| **Prepared By** | Martín Farro, Alexis Sebastián |
| **Attendees (Planning Meeting)** | Evangelista Ygnacio, Sergio Joaquin <br> Saravia Huaricancha, Arturo Axel <br> Negrón Muñoz, Cayo Manuel Stefano <br> Martín Farro, Alexis Sebastián <br> Lucas Córdova, Alvar |
| **Sprint 2 Review Summary** | Durante el Sprint 2 se implementó la primera versión de la Frontend Web Application (v1.0.0) con Vue 3, PrimeVue, Pinia, Vue Router y vue-i18n, organizada por bounded context. Se completaron los contextos Identity and Access Management y Profiles and Vehicles, y se aplicaron las correcciones de la AV1. La aplicación consumió una API simulada con json-server, por lo que los datos no persistían en una base de datos real. |
| **Sprint 2 Retrospective Summary** | El equipo mejoró en cuanto participación y hubo mejor comunicación entre los miembros. Se acordó que cada integrante mantenga sus bounded contexts en su propia rama, que se priorice el reemplazo de la API simulada por un RESTful API real y que las correcciones de la TB1 se resuelvan dentro del Sprint 3. |
| **Sprint Goal** | Our focus is on que el conductor pueda buscar un estacionamiento, reservar y cancelar un espacio, y que el personal operativo pueda registrar ingresos y salidas, todo sobre datos persistentes. <br> We believe it delivers información confiable y consistente a conductores y administradores, al reemplazar los datos simulados por un RESTful API con base de datos real. <br> This will be confirmed when la Web Application opere contra el RESTful API desplegado, una reserva creada persista en MySQL y el cambio de estado del espacio se refleje al registrar el ingreso y la salida. |
| **Value Proposition – Visitors** | Acceso directo desde los botones del Landing Page hacia el registro y el inicio de sesión de la Web Application. |
| **Value Proposition – Users** | Reservas, ocupación e historial de ingresos y salidas que se conservan en una base de datos real, en lugar de datos simulados. |
| **Value Proposition – Developers** | Arquitectura en la nube (Firebase Hosting, contenedor Docker y MySQL remoto) con servicios documentados en OpenAPI. |
| **Sprint Completion Criteria** | Acceso desde el Landing Page al inicio de sesión, persistencia en MySQL en la nube, sin errores de CORS entre la Web Application y el API, y documentación OpenAPI accesible en producción. |
| **User Stories incluidas en el Sprint** | US-50: Acceder a la aplicación web (2) <br> TS-01: Servicio de búsqueda de estacionamientos (5) <br> TS-02: Servicio de detalle de estacionamiento (3) <br> TS-04: Servicio de tarifas (3) <br> US-04: Consultar tarifas (2) <br> US-05: Consultar ubicación (3) <br> TS-08: Servicio de creación de reservas (5) <br> US-17: Validar disponibilidad antes de reservar (3) <br> US-12: Consultar reserva activa (3) <br> TS-09: Servicio de consulta de reservas (3) <br> TS-10: Servicio de cancelación de reservas (5) <br> TS-06: Servicio de salida de vehículos (5) |
| **Sprint 3 Velocity** | 42 Story Points |
| **Sum of Story Points** | 42 Story Points |

#### 5.2.3.2 Aspect Leaders and Collaborators

Para el Sprint 3, el liderazgo se mantiene por bounded context, en continuidad con el Sprint 2, y se incorporan dos aspectos transversales: la persistencia y documentación del API, y la integración con el frontend.

| **Team Member (Last Name, First Name)** | **GitHub Username** | **IAM y Profiles and Vehicles** | **Parking Management** | **Reservations** | **Access Control** | **Persistencia y OpenAPI** | **Integración Frontend** |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| Evangelista Ygnacio, Sergio Joaquin | Sergi9017 | C | L | C | C | C | C |
| Saravia Huaricancha, Arturo Axel | thunder053 | L | C | C | L | C | C |
| Negrón Muñoz, Cayo Manuel Stefano | fano1106-n | C | C | C | C | C | L |
| Martín Farro, Alexis Sebastián | axismf | C | C | C | C | L | C |
| Lucas Córdova, Alvar | Alvarl | C | C | L | C | C | C |

#### 5.2.3.3 Sprint Backlog 3

Las historias del Sprint 3 se descomponen en tareas técnicas. Los datos de horas, responsables y estado se completan con lo registrado en Trello.

**URL del Board:** https://trello.com/b/KxGrDhN2/sprintseasypark
![Sprint 3 - Trello.png](../assets/images/Sprint%203%20-%20Trello.png)

| User Story ID | User Story Title | Story Points | Task ID | Task Title | Description | Estimation (Hours) | Assigned To | Status |
| :--- | :--- | :---: | :--- | :--- | :--- | :---: | :--- | :--- |
| US-50 | Acceder a la aplicación web | 2 | T3-01 | Endpoints de autenticación | Registro e inicio de sesión de cuentas con contraseñas con hash y emisión de JWT con rol. | 4 | Saravia, Arturo | Verificado |
| TS-01 | Servicio de búsqueda de estacionamientos | 5 | T3-02 | Endpoint de búsqueda | Consulta de estacionamientos con filtros por ubicación, disponibilidad y tarifa. | 6 | Evangelista, Sergio | Verificado |
| TS-02 | Servicio de detalle de estacionamiento | 3 | T3-03 | Endpoint de detalle | Consulta de un estacionamiento por su identificador, con respuesta 404 si no existe. | 4 | Evangelista, Sergio | Verificado |
| TS-04 / US-04 | Servicio de tarifas / Consultar tarifas | 5 | T3-04 | Consulta de tarifas | Exposición de la tarifa por hora de cada estacionamiento en los recursos del API. | 5 | Evangelista, Sergio | Verificado |
| US-05 | Consultar ubicación | 3 | T3-05 | Datos de ubicación | Dirección y coordenadas del estacionamiento disponibles para el mapa de la aplicación. | 4 | Negrón, Cayo | Verificado |
| TS-08 | Servicio de creación de reservas | 5 | T3-06 | Endpoint de creación de reservas | Comando de creación de reserva con asignación del espacio y persistencia. | 6 | Lucas, Alvar | Verificado |
| US-17 | Validar disponibilidad antes de reservar | 3 | T3-07 | Validación de disponibilidad | Regla de dominio que rechaza la reserva cuando no hay espacios libres. | 4 | Lucas, Alvar | Verificado |
| US-12 / TS-09 | Consultar reserva activa / Servicio de consulta de reservas | 6 | T3-08 | Consulta de reservas | Consulta de reservas por conductor y de la reserva vigente. | 7 | Martín, Alexis | Verificado |
| TS-10 | Servicio de cancelación de reservas | 5 | T3-09 | Cancelación de reservas | Cancelación de una reserva y liberación del espacio asociado. | 6 | Lucas, Alvar | Verificado |
| TS-06 | Servicio de salida de vehículos | 5 | T3-10 | Endpoint de salida | Registro de la salida, cierre de la permanencia y liberación del espacio. | 6 | Saravia, Arturo | Verificado |
| US-01, US-03, US-11, US-19, US-20, US-21, TS-03, TS-05 | Historias del Sprint 2 | — | T3-11 | Migración a la API real | Disponibilidad, ingreso y ocupación operando sobre el RESTful API en lugar de json-server (sin puntos nuevos). | 6 | Martín, Alexis | Verificado |
| (soporte) | Perfiles y vehículos | — | T3-12 | Endpoints de perfiles y vehículos | Recursos necesarios para asociar el vehículo a la reserva (sin puntos nuevos). | 5 | Saravia, Arturo | Verificado |
| (técnica) | Persistencia y documentación | — | T3-13 | MySQL, migraciones y OpenAPI | Contexto de datos con EF Core, migraciones por bounded context y documentación OpenAPI con Scalar. | 8 | Martín, Alexis | Verificado |
| (técnica) | Integración frontend | — | T3-14 | Conexión de la Web Application | Sustituir la URL de json-server por la del RESTful API y ajustar los assemblers. | 6 | Negrón, Cayo | Verificado |
| (técnica) | Integración Landing | — | T3-15 | Enlaces Landing → Web App | Apuntar los botones de acción del Landing Page a la Web Application. | 2 | Negrón, Cayo | Verificado |
| (técnica) | Despliegue del API | — | T3-16 | Dockerización y despliegue del API | Dockerfile, variables de entorno y publicación del RESTful API conectado a MySQL en la nube. | 4 | Martín, Alexis | Done |
| (técnica) | Despliegue de la Web Application | — | T3-17 | Despliegue en Firebase Hosting | Build de Vite apuntando a la URL del API y publicacion de la Web Application en Firebase Hosting. | 3 | Negrón, Cayo | Done |
| | **Total** | **42** | | | | **86** | | |

**Estado técnico de las tareas en el AV2.** El estado de Trello lo registra el equipo; la siguiente tabla indica qué existe en el código entregado. *Implementado* significa que el código fuente está escrito y revisado estáticamente; **no** significa compilado, probado ni desplegado (ver 5.2.3.5 y 5.2.3.7).

| Task ID | Resultado en el código | Ubicación |
| :--- | :--- | :--- |
| T3-01 | Implementado: registro, inicio de sesión, cambio de contraseña, BCrypt y JWT con rol | `EasyPark.Platform/Iam` |
| T3-02 / T3-03 / T3-04 / T3-05 | Implementado: búsqueda con filtros (`q`, `maxHourlyRate`, `onlyAvailable`, distancia por `latitude`/`longitude`), detalle con 404, tarifa, dirección y coordenadas, disponibilidad calculada | `EasyPark.Platform/ParkingManagement` |
| T3-06 / T3-07 | Implementado: creación de reserva con asignación del espacio compatible, validación de disponibilidad y control de concurrencia | `EasyPark.Platform/Reservations` |
| T3-08 | Implementado: consulta por conductor, por vehículo, por estado y por id | `EasyPark.Platform/Reservations` |
| T3-09 | Implementado: cancelación con liberación del espacio y vencimiento automático de reservas sin ingreso | `EasyPark.Platform/Reservations` |
| T3-10 | Implementado: salida con cierre de permanencia, cobro y liberación del espacio (además del ingreso) | `EasyPark.Platform/AccessControl` |
| T3-11 / T3-14 | Implementado: la Web Application usa el RESTful API; las reglas de reserva y acceso se ejecutan en el servidor | `src/*/infrastructure`, `src/*/application` |
| T3-12 | Implementado: perfiles y vehículos con reglas de propiedad | `EasyPark.Platform/Profiles` |
| T3-13 | Implementado: EF Core + MySQL, migración inicial, OpenAPI (Swagger UI y vista Scalar) | `EasyPark.Platform/Shared`, `Program.cs` |
| T3-15 | Enlaces Landing a Web App pendientes de verificacion en el sitio publico; no afirmar completado sin evidencia | `easypark-landing/index.html` |
| T3-16 | Desplegado en Render: `/health/live` HTTP 200 y `/health/ready` HTTP 200 con `database: connected` | `easypark-backend` y Render |
| T3-17 | Desplegado en Firebase Hosting (42 archivos; `Deploy complete!`); prueba en navegador realizada | `easypark-webapp/firebase.json` y Firebase |

#### 5.2.3.4 Development Evidence for Sprint Review

En el Sprint 3 se implementó la primera versión de los Web Services de EasyPark, **EasyPark Platform**, en C# con ASP.NET Core 10. El codigo se organiza como un monolito modular que inicio con cinco bounded contexts —`Iam`, `Profiles`, `ParkingManagement`, `Reservations` y `AccessControl`— y se extendio con `MonitoringAlerts`, `Notifications` y `AnalyticsReporting` y un núcleo compartido (`Shared`). Cada contexto se divide en las capas `Domain` (agregados, objetos de valor, comandos, consultas y contratos de repositorio), `Application` (servicios de comandos y consultas y fachada ACL), `Infrastructure` (configuración de Entity Framework Core y repositorios) e `Interfaces` (controladores REST, recursos y *assemblers*), siguiendo la estructura del proyecto de referencia del curso.

Principales decisiones de implementación:

- **Persistencia:** Entity Framework Core 10 con el proveedor `MySql.EntityFrameworkCore` sobre MySQL 8; quince tablas previstas por dos migraciones de EF Core: ocho iniciales (`20261025150000_InitialCreate`) y siete adicionales (`20261102000000_ExtendedFeatures`); columnas en `snake_case` (ver 4.8.2).
- **Seguridad:** contraseñas con BCrypt, JWT firmado (HS256) con los claims `sub`, `email` y `role`, autorización por rol (`DRIVER`, `OPERATOR_ADMIN`, `OPERATOR_STAFF`) y verificación de propiedad en cada caso de uso.
- **Reglas de negocio en el servidor:** la creación de una reserva asigna y bloquea el espacio en la misma transacción (control de concurrencia optimista en `parking_spots.version`); el registro de un ingreso o una salida valida la reserva, abre o cierra la permanencia, calcula el cobro y actualiza el espacio y la reserva en una sola transacción; las reservas sin ingreso vencen automáticamente.
- **Errores:** respuestas `application/problem+json` con un `code` estable que la Web Application traduce (por ejemplo `no-availability`).
- **Integración:** la Web Application dejó de modificar espacios y reservas desde el navegador y consume los nuevos comandos del API; los módulos de alertas, notificaciones y reportes también tienen implementación de API y frontend en el repositorio integrado; sus flujos completos quedan pendientes de validacion funcional.
- **Pruebas:** proyecto `EasyPark.Platform.Tests` con pruebas de dominio y de integración (xUnit y `WebApplicationFactory`).

Repositorio del backend: https://github.com/upc-pre-202620-1asi0730-8074-ApexCode/easypark-backend. Repositorio de la Web Application: https://github.com/upc-pre-202620-1asi0730-8074-ApexCode/easypark-webapp

En esta iteración la Web Application deja de depender de json-server para los contextos IAM, Profiles and Vehicles, Parking Management, Reservations y Access Control, y consume el RESTful API. Los datos que el usuario crea se guardan en MySQL.

1. Registro e inicio de sesión de un conductor. ![APP - Home.png](../assets/images/APP%20-%20Home.png)
2. Perfil del conductor y registro de su vehículo. ![APP - PROFILE.png](../assets/images/APP%20-%20PROFILE.png)
3. Búsqueda de estacionamientos con tarifa, ubicación y espacios disponibles. ![APP - Search.png](../assets/images/APP%20-%20Search.png)
4. Creación de una reserva. ![APP - Booking.png](../assets/images/APP%20-%20Booking.png)
5. Detalle de la sede para el operador.![APP - Facilities.png](../assets/images/APP%20-%20Facilities.png)
6. Registro del ingreso: espacio *Ocupado* y permanencia abierta. ![APP - Ocupancy.png](../assets/images/APP%20-%20Ocupancy.png)
7. Registro de la salida: permanencia cerrada con el importe cobrado. ![APP - Monitoring.png](../assets/images/APP%20-%20Monitoring.png)
8. Historial de reservas del conductor . ![APP - Bookings.png](../assets/images/APP%20-%20Bookings.png)

**Video de demostración:** [PENDIENTE: agregar enlace real del equipo; no confundir capturas de la interfaz con pruebas E2E].

#### 5.2.3.5 Execution Evidence for Sprint Review

En esta entrega se comprobaron la compilacion del frontend y la conectividad del API desplegado; los recorridos funcionales se documentan separando resultados observados y pruebas aun no realizadas. Esta distincion impide presentar capturas de interfaz como pruebas de todo el ciclo de reserva.

| Prueba | Ejecucion / evidencia | Resultado |
| :--- | :--- | :--- |
| Compilacion de la Web Application | `npm run build` (Vite 8.3.2) | Correcta; 974 modulos transformados |
| Pruebas de contrato API-only | `node --test tests/api-only-contract.test.mjs` | 4/4 correctas: sin json-server, reservas y accesos por API, URL de Render |
| Backend activo | `GET /health/live` | HTTP 200 |
| API y persistencia | `GET /health/ready` | HTTP 200; `{"status":"ready","database":"connected"}` |
| Documentacion de servicios | `GET /swagger`, `GET /openapi/v1.json` | HTTP 200 en ambas rutas |
| CORS del frontend publico | Preflight `OPTIONS /api/v1/authentication/sign-in` desde `https://easypark-5ffb2.web.app` | HTTP 204 con `access-control-allow-origin` correcto |
| IAM y perfiles | Registro/inicio de sesion con cuentas nuevas de conductor y operador; consulta/edicion de perfil | Recorrido manual observado desde la Web Application |
| Parking Management | El operador creo la sede `Prueba1`; el conductor la visualizo primero sin espacios y despues con dos espacios libres | Intercambio de datos observado entre roles, con API y MySQL conectados |
| Reservas y control de acceso | Crear/cancelar reserva, entrada/salida, importe y liberacion del espacio | Pendiente de prueba funcional completa; no afirmar verificado |
| Alertas, notificaciones y reportes | Pantallas y servicios disponibles en codigo | Pendiente comprobar ciclo funcional y persistencia |
| Publicacion | `firebase deploy --only hosting --project easypark-5ffb2` | `Deploy complete!`; 42 archivos publicados |

**Evidencias graficas por adjuntar:** capturas del login, perfil, sede creada y dos espacios libres tomados en la version desplegada; captura de `/health/ready`; historial de despliegues en Firebase y Render. Evitar mostrar JWT, contrasenas o cadenas de conexion.

**Incidencias no cerradas:** el navegador muestra `Invalid PrimeUI License`, pese a que se incluyo una clave Community en el build; `npm audit` reporto siete vulnerabilidades de severidad alta. Se registran como pendientes para el siguiente ciclo, no como pruebas aprobadas.
#### 5.2.3.6 Services Documentation Evidence for Sprint Review

El contrato de los servicios se documenta con OpenAPI. El propio API genera el documento con Swashbuckle y lo publica en tres vistas:

- Swagger UI: https://easypark-backend-qheu.onrender.com/swagger/index.html
- Documento OpenAPI: https://easypark-backend-qheu.onrender.com/openapi/v1.json
- Vista Scalar del mismo documento: https://easypark-backend-qheu.onrender.com/scalar/v1

![swagger 1.png](../assets/images/swagger%201.png)
![swagger 2.png](../assets/images/swagger%202.png)
![swagger 3.png](../assets/images/swagger%203.png)
![Escalar Api.png](../assets/images/Escalar%20Api.png)

Todos los endpoints usan el prefijo `/api/v1`, JSON en camelCase e identificadores enteros, y requieren `Authorization: Bearer <token>` salvo `sign-up` y `sign-in`. La columna *Estado de pruebas* se completa con los códigos HTTP obtenidos al probar cada endpoint (guía en `docs/06-PRUEBAS.md`).

| Bounded Context | Endpoint | Verbo HTTP | Propósito | Parámetros / cuerpo principal | Respuesta | Estado de pruebas |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| IAM | `/api/v1/authentication/sign-up` | POST | Registra una cuenta `DRIVER` u `OPERATOR_ADMIN` | `email`, `password`, `role` | 201 · 400 · 409 | Endpoint documentado; prueba individual pendiente |
| IAM | `/api/v1/authentication/sign-in` | POST | Valida credenciales y emite el JWT | `email`, `password` | 200 `{id, email, role, token}` · 401 · 403 | Endpoint documentado; prueba individual pendiente |
| IAM | `/api/v1/authentication/password` | PUT | Cambia la contraseña de la cuenta autenticada | `currentPassword`, `newPassword` | 200 · 422 | Endpoint documentado; prueba individual pendiente |
| Profiles and Vehicles | `/api/v1/profiles` | GET, POST | Consulta (`?userAccountId=`) y crea el perfil propio | `firstName`, `lastName`, `phone`, `companyName`, `jobTitle` | 200 · 201 · 409 | Endpoint documentado; prueba individual pendiente |
| Profiles and Vehicles | `/api/v1/profiles/{id}` | GET, PUT | Detalle y actualización del perfil propio | — | 200 · 403 · 404 | Endpoint documentado; prueba individual pendiente |
| Profiles and Vehicles | `/api/v1/vehicles` | GET, POST | Lista por `profileId`, búsqueda por `plateNumber` y registro de vehículos | `plateNumber`, `vehicleType`, `color`, `isDefault` | 200 · 201 · 409 | Endpoint documentado; prueba individual pendiente |
| Profiles and Vehicles | `/api/v1/vehicles/{id}` | GET, PUT | Detalle, actualización, vehículo predeterminado y retiro del perfil | `profileId`, `vehicleType`, `color`, `isDefault` | 200 · 403 | Endpoint documentado; prueba individual pendiente |
| Parking Management | `/api/v1/parking-facilities` | GET, POST | Búsqueda (`q`, `maxHourlyRate`, `onlyAvailable`, `latitude`, `longitude`) y registro de estacionamientos | `name`, `address`, `latitude`, `longitude`, `hourlyRate`, `openTime`, `closeTime` | 200 · 201 · 403 | Endpoint documentado; prueba individual pendiente |
| Parking Management | `/api/v1/parking-facilities/{id}` | GET, PUT | Detalle con tarifa, ubicación y disponibilidad; actualización | — | 200 · 404 | Endpoint documentado; prueba individual pendiente |
| Parking Management | `/api/v1/parking-spots` | GET, POST | Espacios de una sede (`facilityId`) y registro de espacios | `facilityId`, `code`, `level`, `spotType` | 200 · 201 · 409 | Endpoint documentado; prueba individual pendiente |
| Parking Management | `/api/v1/parking-spots/{id}` | GET, PUT | Detalle, edición y cambio manual de estado | `code`, `level`, `spotType`, `status` | 200 · 409 | Endpoint documentado; prueba individual pendiente |
| Reservations | `/api/v1/reservations` | GET, POST | Consulta de reservas y creación con asignación de espacio | `vehicleId`, `parkingFacilityId`, `startAt`, `durationMinutes` | 200 · 201 · 409 | Endpoint documentado; prueba individual pendiente |
| Reservations | `/api/v1/reservations/{id}` | GET, PUT | Detalle y cancelación (`status: CANCELLED`) | `status` | 200 · 409 | Endpoint documentado; prueba individual pendiente |
| Reservations | `/api/v1/reservations/{id}/cancellation` | POST | Cancelación explícita | — | 200 · 409 | Endpoint documentado; prueba individual pendiente |
| Access Control | `/api/v1/access-movements` | GET, POST | Historial por sede y registro de ingreso/salida por placa | `parkingFacilityId`, `plateNumber`, `movementType`, `registrationMethod`, `reservationCode` | 200 · 201 (`COMPLETED`, `REJECTED`, `UNDER_REVIEW`) | Endpoint documentado; prueba individual pendiente |
| Access Control | `/api/v1/access-movements/{id}` | GET, PUT | Detalle y cierre de una revisión (`REJECTED`) | `status`, `note` | 200 · 409 | Endpoint documentado; prueba individual pendiente |
| Access Control | `/api/v1/parking-stays` | GET | Permanencias por sede (`parkingFacilityId`, `open`) | — | 200 | Endpoint documentado; prueba individual pendiente |
| Access Control | `/api/v1/parking-stays/{id}` | GET, PUT | Detalle y reasignación de espacio | `parkingSpotId` | 200 · 409 | Endpoint documentado; prueba individual pendiente |

#### 5.2.3.7 Software Deployment Evidence for Sprint Review

El equipo publico la Web Application en Firebase Hosting y la conecto al RESTful API de Render, con base de datos MySQL remota de Aiven. El enlace a Landing Page se conserva, pero sus botones de acceso deben verificarse directamente. La evidencia final incluye las comprobaciones de salud, CORS, Swagger y el despliegue de Vite en Firebase.

| Producto | Plataforma | Estado observado | URL |
| :--- | :--- | :--- | :--- |
| Landing Page | GitHub Pages | Publicada con anterioridad; enlaces a la app pendientes de comprobacion | https://upc-pre-202620-1asi0730-8074-apexcode.github.io/easypark-landing/ |
| Web Application | Firebase Hosting | Nueva compilacion publicada; 42 archivos, `Deploy complete!` | https://easypark-5ffb2.web.app/ |
| RESTful Web Services | Render | HTTP 200 en `/health/live`, `/health/ready`, Swagger y OpenAPI; CORS validado | https://easypark-backend-qheu.onrender.com |
| Base de datos | Aiven MySQL | Conexion confirmada desde Render (`database: connected`); dos migraciones definen 15 tablas | No publicar credenciales |

En la defensa se deben mostrar capturas del panel de despliegue y el recorrido completo que pueda demostrarse; no se debe declarar que reservas, entradas, salidas o notificaciones estan validadas hasta probarlas. El aviso de licencia PrimeUI sigue pendiente y no afecta la verificacion de salud del API.
#### 5.2.3.8 Team Collaboration Insights during Sprint

La colaboración del Sprint 3 se evidencia con las estadísticas de GitHub de los repositorios del RESTful API y de la Web Application (**Insights → Contributors** y **Insights → Commits**), filtradas al periodo del sprint.
![Sprint 3 - Contributions.png](../assets/images/Sprint%203%20-%20Contributions.png)


**Commits comprobados en GitHub (SHA abreviado).** Se presenta la evidencia por repositorio sin atribuir automaticamente la autoria individual; cada integrante debe verificar sus aportes con `git log --author` y GitHub Insights.

| Repositorio | Commit | Evidencia de desarrollo o integracion |
| :--- | :--- | :--- |
| Web Application | [`412ff28`](https://github.com/upc-pre-202620-1asi0730-8074-ApexCode/easypark-webapp/commit/412ff28715e0a059b50115ebf6768fd569fb2c6c) | Integracion API-only, eliminacion de `json-server` y cuatro pruebas de contrato |
| Web Application | [`a5bf352`](https://github.com/upc-pre-202620-1asi0730-8074-ApexCode/easypark-webapp/commit/a5bf352ec) | Incorporacion de `main` con resolucion de conflictos |
| Web Application | [`6274136`](https://github.com/upc-pre-202620-1asi0730-8074-ApexCode/easypark-webapp/commit/6274136a) | Integracion de la rama de IAM |
| Web Application | [`30d50bd`](https://github.com/upc-pre-202620-1asi0730-8074-ApexCode/easypark-webapp/commit/30d50bd657ac6c5d82c1409df65cf3fcd743fad0) | Integracion de pantallas Parking Management |
| Web Application | [`a8da93d`](https://github.com/upc-pre-202620-1asi0730-8074-ApexCode/easypark-webapp/commit/a8da93d208184fc0dc8d33efbfcba3f41c6d07dc) | Cierre final de integracion; `main` y `develop` apuntaron al mismo commit |
| Backend | [`0b3e4c8`](https://github.com/upc-pre-202620-1asi0730-8074-ApexCode/easypark-backend/commit/0b3e4c80f) | Integracion de las funcionalidades extendidas |
| Backend | [`b3d2533`](https://github.com/upc-pre-202620-1asi0730-8074-ApexCode/easypark-backend/commit/b3d25338a) | Restauracion del kernel compartido |
| Backend | [`1ab47fb`](https://github.com/upc-pre-202620-1asi0730-8074-ApexCode/easypark-backend/commit/1ab47fb4c2518b1cc640b846a63de1e4679336af) | Cambio de la ruta raiz a la documentacion Scalar |
| Informe | [`e2eabb53`](https://github.com/upc-pre-202620-1asi0730-8074-ApexCode/easypark-report/commit/e2eabb53b) | Evidencias y enlaces de despliegue de Sprint 3 |

**Trazabilidad pendiente del equipo:** adjuntar captura de GitHub Insights/Contributors, responsables definitivos de cada tarea de Trello y los enlaces al video de demostracion. La fecha y asistentes de la reunion de planning se mantienen segun la documentacion existente.

## 5.3. Validation Interviews

### 5.3.1. Diseño de Entrevistas

**Objetivo.** Validar con usuarios de los dos segmentos que los flujos implementados en la Web Application conectada al RESTful API resuelven los problemas identificados en el capítulo II, y detectar problemas de usabilidad antes del siguiente sprint.

**Participantes.** Al menos tres personas por segmento (conductores; administradores o personal operativo de estacionamientos), distintas de los integrantes del equipo. **Formato:** sesión de 20 a 30 minutos, presencial o por videollamada grabada con consentimiento. El entrevistado usa la versión desplegada de la Web Application con una cuenta de prueba; el entrevistador no guía los clics salvo que la persona quede bloqueada.

**Guion — Segmento 1: Conductores**

1. Presentación del objetivo y consentimiento para grabar.
2. Datos generales: edad aproximada, distrito, frecuencia con la que estaciona en Lima, cómo busca estacionamiento hoy.
3. Tarea 1: registrarse e iniciar sesión.
4. Tarea 2: completar el perfil y registrar su vehículo.
5. Tarea 3: buscar un estacionamiento, revisar tarifa y disponibilidad, y reservar para dentro de una hora.
6. Tarea 4: encontrar la reserva y su código; cancelarla.
7. Preguntas: ¿qué tan claro fue el importe estimado?, ¿confiaría en que el espacio estará disponible?, ¿qué información le faltó?, ¿qué cambiaría?
8. Valoración de 1 a 5 de la facilidad de uso de cada tarea.

**Guion — Segmento 2: Administradores y personal operativo**

1. Presentación y consentimiento.
2. Datos generales: tipo y tamaño del estacionamiento, cómo registra hoy ingresos y salidas.
3. Tarea 1: iniciar sesión, registrar una sede con su tarifa y horario, y crear espacios.
4. Tarea 2: identificar un espacio reservado.
5. Tarea 3: registrar el ingreso de un vehículo con reserva y luego su salida; revisar el importe.
6. Tarea 4: marcar un espacio fuera de servicio y devolverlo al servicio; reasignar una permanencia.
7. Preguntas: ¿el registro por placa es más rápido que su método actual?, ¿qué datos necesita ver en el panel?, ¿qué haría si una placa no está registrada?
8. Valoración de 1 a 5 de cada tarea.

**Registro.** Por cada entrevista se anotan: tiempo empleado por tarea, errores, comentarios textuales relevantes y las valoraciones.

### 5.3.2. Registro de Entrevistas

Las entrevistas de validación deben realizarse con la versión integrada. Esta sección se completa con los datos reales de cada sesión; no contiene datos inventados.

| N.° | Segmento | Entrevistado (nombre o seudónimo, con consentimiento) | Fecha | Duración | Entrevistador | Enlace a la grabación | Resumen de hallazgos |
| :---: | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Conductor | Kevin Romero | 11/11/2026 | 4:00 | Cayo Negron |  | El entrevistado manifesto una percepcion positiva sobre la interfaz del sistema, comento que le parecio muy intuitiva y facil de usar, que los indicadores son accesibles y que los colores le son pertinentes para identicar el estado de las reservas. Destaco la utilidad de los filtros e indicadores. Como aspecto de mejora indico que se podrian usar iconos o imagenes para que sea mas visual la interfaz. |
| 2 | Conductor | Joaquin | 12/11/2026 |  | Alexis Martin | | |
| 3 | Conductor | Fabio Calderon | 13/11/2026 |  | Sergio Evangelista |  | El entrevistado Fabio Calderón evalúa EasyPark de forma mayormente positiva. Le parece clara la información de precio, disponibilidad y horario, y sencillo el flujo de reserva (fecha, hora de inicio, duración y vehículo registrado). Destaca que las notificaciones de “My Reservations” avisan bien cuando el tiempo está por vencer o ya venció. Comenta que suele demorar unos 15 minutos buscando estacionamiento en zonas concurridas dando vueltas, por lo que valora que la app muestre el precio y un indicador de espacios disponibles como información esencial. Los indicadores de espacios libres le ayudan a decidir rápido, y los textos, tarifas y botones le resultan fáciles de leer. Como mejora, sugiere agregar filtros por costo o disponibilidad y una mejor gestión de los estacionamientos cercanos a su localidad. |
| 4 | Conductor | Esteban Chavez | 13/11/2026 |  | Sergio Evangelista | | El entrevistado Esteban Chavez comparte una perspectiva mayormente positiva sobre EasyPark. Encuentra los indicadores de espacios disponibles bastante intuitivos para identificar rápidamente dónde estacionar, y considera que los textos, tarifas y botones principales se entienden bien siempre que sean visibles. Actualmente enfrenta bastante demora al buscar estacionamiento, teniendo que esperar un tiempo considerable hasta encontrar un espacio, por lo que para confiar en la app necesita ver principalmente si hay espacios disponibles y dónde está ubicado el estacionamiento. Como mejora, propone agregar un filtro para ordenar los estacionamientos por precio, distancia y disponibilidad, mostrar el tiempo aproximado para llegar al lugar, y mantener un diseño sencillo con información importante y botones fáciles de identificar.|
| 5 | Administrador / operador | Aristides  Aguirre | 11/11/2026 | 6:34 | Cayo Negron| https://youtu.be/aurQ1eyXE3k | El entrevistado indicó que el dashboard permite identificar rápidamente los espacios libres y ocupados que pueda tener su establecimiento, señaló que la información presentada es clara y no genera sobrecarga visual de manera que no resulta complicada de entender.  |
| 6 | Administrador / operador | Uziel | 12/11/2026 | 13:00 | Arturo Saravia |  https://upcedupe-my.sharepoint.com/:v:/g/personal/u202312447_upc_edu_pe/IQDbI5UQgKyxS5anr2PcOXBcAespTfCwwlYeBZXwOzmPvfo?nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJPbmVEcml2ZUZvckJ1c2luZXNzIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXciLCJyZWZlcnJhbFZpZXciOiJNeUZpbGVzTGlua0NvcHkifX0&e=Mgj6hA | |
| 7 | Administrador / operador | Diego Coartas | 12/11/2026 | 10:38  | Arturo Saravia | https://upcedupe-my.sharepoint.com/:v:/g/personal/u202312447_upc_edu_pe/IQD8251027PKTaTYs2rQPy_jAXnGg-O3oCyeju70hK4w9jw?nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJPbmVEcml2ZUZvckJ1c2luZXNzIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXciLCJyZWZlcnJhbFZpZXciOiJNeUZpbGVzTGlua0NvcHkifX0&e=Is9gFR | |

![VI - KEVIN.png](../assets/images/VI%20-%20KEVIN.png)
![VI - ARISTIDES.png](../assets/images/VI%20-%20ARISTIDES.png)
![VI - ARTURO - DIEGO.png](../assets/images/VI%20-%20ARTURO%20-%20DIEGO.png)
![VI - ARTURO - UZIEL.png](../assets/images/VI%20-%20ARTURO%20-%20UZIEL.png)
### 5.3.3. Evaluaciones según heurísticas

Se aplicará una evaluación heurística a la Web Application integrada usando las diez heurísticas de usabilidad de Jakob Nielsen. Cada hallazgo se registra con la tarea en que apareció, la heurística incumplida, su severidad (0 = no es problema, 1 = cosmético, 2 = menor, 3 = mayor, 4 = catastrófico) y la recomendación.

**Carrera:** Ingeniería de Software · **Curso:** Aplicaciones Web · **Producto:** EasyPark Web Application · **Evaluador(es):** Easypark · **Fecha:** 12/11/2026

**Tareas evaluadas:** registro e inicio de sesión; perfil y vehículos; búsqueda y reserva; cancelación; gestión de sedes y espacios; registro de ingreso y salida.

| Heurística | Descripción |
| :--- | :--- |
| H1 | Visibilidad del estado del sistema |
| H2 | Correspondencia entre el sistema y el mundo real |
| H3 | Control y libertad del usuario |
| H4 | Consistencia y estándares |
| H5 | Prevención de errores |
| H6 | Reconocer antes que recordar |
| H7 | Flexibilidad y eficiencia de uso |
| H8 | Diseño estético y minimalista |
| H9 | Ayudar a reconocer, diagnosticar y recuperarse de errores |
| H10 | Ayuda y documentación |

| N.° | Problema | Tarea / pantalla | Heurística | Severidad | Recomendación |
| :---: | :--- | :--- | :---: | :---: | :--- |
| 1 | La tarjeta del estacionamiento no tiene un botón visible de “Reservar” ni parece clicable. | Buscar estacionamiento | H6, H7 | 2 | Agregar un botón “Reservar” y un efecto hover. |
| 2 | La pantalla de login tiene un separador “or” sin ninguna opción alternativa debajo. | Inicio de sesión	 | H8, H4 | 1 | Mostrar “N/A” o “Sin reservas en el periodo”. |
| 3 | Hallazgo de la entrevista 1 (Kevin Romero): la interfaz podría usar más íconos o imágenes para ser más visual. | General (conductor) | H8, H6 | 1 | Agregar íconos a los estados de reserva y a las tarjetas de estacionamiento. |
| 4 | Hallazgo de la entrevista 1 (Kevin Romero): la interfaz podría usar más íconos o imágenes para ser más visual. | General (conductor) | H8, H6 | 1 | Agregar íconos a los estados de reserva y a las tarjetas de estacionamiento. |
| 5 | Hallazgo de la entrevista 4 (Esteban Chavez): para confiar en la app necesita ver si hay espacios y dónde está el estacionamiento, y propuso mostrar el tiempo aproximado de llegada. Las tarjetas muestran tarifa, dirección y espacios libres, pero no distancia ni tiempo, y el mapa no tiene calles de referencia. | H2, H6 | 2 | Mostrar en cada tarjeta la distancia y el tiempo estimado y agregar un botón "Cómo llegar". |

## 5.4. Video About-the-Product

**Estado:** [PENDIENTE: grabar y publicar la primera versión; pegar aquí la URL y la duración].

**Objetivo:** mostrar en 3 a 5 minutos el problema, la propuesta de valor y el funcionamiento real de EasyPark con la Web Application conectada al RESTful API.

| Escena | Duración aprox. | Contenido | Pantalla / recurso |
| :---: | :---: | :--- | :--- |
| 1 | 0:00–0:30 | El problema: tiempo perdido buscando estacionamiento y registros manuales de los operadores | Landing Page |
| 2 | 0:30–1:00 | La propuesta: reserva anticipada para conductores y control digital para operadores | Landing Page (beneficios) |
| 3 | 1:00–2:00 | Conductor: registro, vehículo, búsqueda con tarifa y disponibilidad, reserva con código | Web Application desplegada |
| 4 | 2:00–3:15 | Operador: sede y espacios, espacio reservado, ingreso por placa, salida con importe | Web Application desplegada |
| 5 | 3:15–3:45 | Respaldo técnico: datos guardados en MySQL y servicios documentados en Swagger | Swagger del API desplegado |
| 6 | 3:45–4:15 | Cierre: próximos pasos y llamado a la acción | Landing Page |

**Checklist antes de publicar:** audio claro; sin contraseñas, tokens ni cadenas de conexión en pantalla; servicio de Render “despierto” antes de grabar; subtítulos o texto en pantalla; URL agregada en esta sección y en el Anexo A.

## 5.5. Video About-the-Team

**Estado:** [PENDIENTE: grabar y publicar la primera versión; pegar aquí la URL y la duración].

**Objetivo:** mostrar en 3 a 5 minutos cómo trabajó el equipo ApexCode durante el proyecto.

| Escena | Contenido | Responsable |
| :---: | :--- | :--- |
| 1 | Presentación del equipo y de la startup ApexCode | Verificado |
| 2 | Cada integrante (30–40 s): rol, bounded context liderado y principal aporte en el Sprint 3 | Cada integrante |
| 3 | Organización: Trello, GitFlow, Conventional Commits y reuniones de planificación y revisión | Verificado |
| 4 | Evidencia de colaboración: GitHub Insights de los repositorios | Verificado |
| 5 | Aprendizajes y dificultades superadas | Verificado |
| 6 | Cierre | Verificado |

**Checklist:** todos los integrantes aparecen; la información coincide con 5.2.3.2 y con el Student Outcome; URL agregada en esta sección y en el Anexo A.

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

En esta sección se describen los principales acuerdos y definiciones realizadas durante el Sprint Planning del Sprint 1, enfocado en la implementación del Landing Page de EasyPark.

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
    </td>
  </tr>

<tr>
    <td>Sprint 1 Retrospective Summary</td>
    <td>
      Our focus is on que el conductor pueda buscar y reservar un espacio, y el personal operativo pueda registrar el ingreso, la ocupación y la salida de los vehículos en la plataforma.
      We believe it delivers reducción en el tiempo de búsqueda para conductores y mayor control operativo to los administradores de estacionamientos independientes.
      This will be confirmed when el conductor complete una reserva en la aplicación y el administrador pueda visualizar el cambio de estado (a "Ocupado" o "Reservado") en su panel de control en tiempo real.
    </td>
  </tr>

<tr>
    <td>Sprint 2 Velocity</td>
    <td>
    42
    </td>
  </tr>

<tr>
    <td>Sum of Story Points</td>
    <td>
    42
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
    <td> Done/td>
  </tr>

</table>

![Product Backlog 2.png](../assets/images/Product%20Backlog%202.png)

#### 5.2.2.4 Development Evidence for Sprint Review.

En el Sprint 2 se implementó la primera versión de la Frontend Web Application en el repositorio, con Vue 3, PrimeVue, Pinia, Vue Router, vue-i18n y axios, en JavaScript. El código se organiza por bounded context, y cada uno se divide en las capas domain, application, infrastructure y presentation. Arturo Saravia preparó la base del proyecto.

En el repositorio se aplicaron las correcciones de AV1.
Lading page:
https://upc-pre-202620-1asi0730-8074-apexcode.github.io/easypark-landing/index.html?lang=es

#### 5.2.2.5 Execution Evidence for Sprint Review.

Al cierre del Sprint 2, la Frontend Web Application v1.0.0 se encuentra publicada en: . La aplicación ofrece una experiencia distinta para cada rol

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

#### 5.2.2.8 Team Collaboration Insights during Sprint.

El equipo mantuvo un ritmo de trabajo organizado, repartiendo la carga por bounded contexts: en este Sprint se completaron IAM y Profiles and Vehicles, mientras los restantes avanzan en paralelo.

* Se respetó una arquitectura basada en Domain-Driven Design, estructurando cada bounded context en las capas domain/model, application, infrastructure y presentation, lo que mantuvo límites claros entre módulos y evitó que un contexto accediera directamente a la lógica de otro.
* Se reutilizaron los tokens de diseño y el preset personalizado de PrimeVue en componentes reutilizables de Vue, lo que permitió construir las vistas del conductor (inicio de sesión, registro y perfil) manteniendo total consistencia visual con el Landing Page desarrollado en el Sprint 1.
* El soporte de internacionalización (español e inglés) y el layout compartido se mantuvieron centralizados para garantizar coherencia en toda la aplicación.
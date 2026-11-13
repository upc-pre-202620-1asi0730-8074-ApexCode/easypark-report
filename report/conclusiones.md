# Conclusiones

Existe una clara necesidad en el sector de la movilidad urbana y la gestión de estacionamientos de contar con una plataforma digital confiable que permita administrar de manera eficiente la disponibilidad de espacios, controlar los ingresos y salidas, y realizar búsquedas de ubicaciones en tiempo real. Los distintos actores involucrados, como administradores de estacionamientos, personal operativo y conductores, requieren herramientas que centralicen la información y reduzcan los errores operativos derivados del uso de métodos manuales y tickets físicos. 

El análisis de requisitos y las funcionalidades definidas evidencian que los usuarios no solo buscan un lugar para estacionar, sino también contar con un sistema integral que les permita reservar con anticipación, recibir notificaciones sobre el tiempo de permanencia, visualizar la ocupación actual y acceder a reportes operativos que faciliten la toma de decisiones. Esto posiciona a EasyPark como una solución completa para la gestión inteligente de estacionamientos urbanos. 

El sistema no se limita a ser una herramienta operativa, sino que también busca optimizar el uso del espacio físico, mejorar la trazabilidad de los vehículos organizándolos por zonas y tipos de usuario, y fortalecer la comunicación entre el administrador y el cliente. De esta manera, contribuye a una gestión más ágil, transparente y orientada a reducir la congestión dentro del entorno vehicular. 

Los resultados obtenidos a partir del análisis funcional, la definición de User Stories y la aplicación de técnicas como Lean UX Canvas e Impact Mapping, muestran que EasyPark tiene el potencial de consolidarse como una solución tecnológica innovadora, escalable y adaptable tanto a pequeños operadores independientes como a infraestructuras de mayor tamaño. 

Durante el desarrollo del proyecto, se utilizaron herramientas de diseño, modelado y dinámicas como el EventStorming que permitieron estructurar de manera clara las funcionalidades del sistema bajo el enfoque de Domain-Driven Design. La elaboración de diagramas (clases, arquitectura de software y base de datos) facilitó la comprensión de la lógica de los Bounded Contexts y la relación entre sus elementos, permitiendo tomar decisiones más acertadas en el diseño técnico. Asimismo, la organización del trabajo mediante el Product Backlog y la priorización de Sprints facilitó una mejor gestión del desarrollo y distribución de tareas dentro del equipo para poder tener resultados como lo fue la Landing Page. 

Por otro lado, a pesar de no contar aún con un backend en la nube, el equipo logró validar las funcionalidades críticas del Sprint 2 (IAM y Profiles and Vehicles) apoyándose de manera efectiva en una API REST simulada (json-server). Esto permitió verificar la navegación, autenticación mediante tokens y consumo de datos sin bloquear el progreso del Frontend.

La distribución del liderazgo por Bounded Contexts resultó ser una estrategia acertada. Permitió al equipo trabajar en paralelo en sus respectivas ramas y, al mismo tiempo, mantener una alta consistencia visual y funcional en todo el proyecto gracias a la reutilización de componentes de PrimeVue, tokens de diseño y centralización del manejo de internacionalización (i18n).

Finalmente, se concluye que EasyPark no solo responde a una necesidad real de reducir el tiempo y estrés al buscar estacionamiento, sino que también representa una oportunidad para que los negocios mejoren significativamente su eficiencia de control, reduzcan pérdidas por registros erróneos y optimicen su supervisión mediante el uso de tecnología.

**Avance de conclusiones del Sprint 3 (TB2).** En este sprint se construyó la primera versión de los Web Services de EasyPark en ASP.NET Core 10, con los bounded contexts de IAM, Profiles and Vehicles, Parking Management, Reservations y Access Control organizados en capas de dominio, aplicación, infraestructura e interfaces, y persistencia en MySQL mediante Entity Framework Core. Trasladar al servidor las reglas que antes resolvía el navegador —asignar y bloquear el espacio al reservar, y registrar ingresos y salidas con su permanencia y su cobro en una sola transacción— corrige inconsistencias del Sprint 2 y es la base para que la información de disponibilidad sea confiable, que era una de las necesidades más repetidas en las entrevistas.

La integración con la Web Application mostró que mantener el contrato REST definido en el Sprint 2 (rutas, nombres de campos e identificadores enteros) reduce el costo de reemplazar la API simulada, y que las diferencias con el diseño de base de datos del capítulo IV deben documentarse en cada iteración (sección 4.8.2). [PENDIENTE: completar esta conclusión con los resultados reales de las pruebas, del despliegue y de las entrevistas de validación del Sprint 3.]

# Recomendaciones

• **Sobre la continuidad del desarrollo del sistema**: Se recomienda continuar con la implementación progresiva de las funcionalidades planificadas, priorizando aquellos módulos que representan el valor diferencial de Easypark. Lo cual permitirá consolidar una experiencia de usuario más eficiente y alineada con las necesidades identificadas durante la etapa de investigación.

• **Sobre la experiencia de usuario (UX/UI)**: Se recomienda seguir perfeccionando la interfaz, dando prioridad a que sea accesible, fácil de recorrer y visualmente clara al mostrar disponibilidad, sectores y avisos. También se debe llevar a cabo pruebas de usabilidad con usuarios reales, con el fin de detectar oportunidades de mejora en la interacción y minimizar dificultades al usar la plataforma.

• **Sobre analítica y toma de decisiones**: Para el mediano plazo, se sugiere sumar soluciones de análisis de datos capaces de mostrar tendencias de ocupación, franjas de mayor demanda y conducta de los usuarios. Esto ayudaría a los administradores a decidir mejor y, además, permitiría aprovechar modelos predictivos para mejorar la administración de los estacionamientos.

• **Adopción exitosa de Arquitectura y Tecnologías**: El equipo logró asentar sólidamente las bases de la Frontend Web Application utilizando Vue 3. La implementación de una arquitectura monolítica modular basada en Domain-Driven Design (DDD) permitió establecer límites claros entre los distintos módulos, organizando el código adecuadamente en las capas de dominio, aplicación, infraestructura y presentación.

• **Priorización del Desarrollo y Despliegue del Backend**: Dado que la validación actual depende de una API simulada (json-server), se recomienda que en el próximo Sprint la prioridad técnica sea el desarrollo del Backend RESTful real en ASP.NET Core y la configuración de la base de datos relacional en la nube. Esto será vital para integrar las lógicas de negocio complejas (como las reservas y el control de ocupación).

• **Refuerzo en la Integración Continua (CI)**: Como los demás Bounded Contexts (Reservations, Monitoring, Access Control) continúan desarrollándose en paralelo por diferentes miembros, se recomienda aumentar la frecuencia de integración de ramas y mantener revisiones de código cruzadas más estrictas para evitar los "pequeños retrasos en la integración" que el equipo ya había identificado como riesgo en el Sprint 1.

• **Sobre la verificación del Sprint 3**: ejecutar las pruebas automatizadas del RESTful API y el recorrido funcional contra MySQL antes de registrar evidencias, y desplegar el API, la base de datos y la Web Application siguiendo las guías del paquete del Sprint 3.

• **Sobre los planes gratuitos de despliegue**: considerar que el servicio gratuito de Render se suspende tras 15 minutos sin tráfico y que Aiven puede apagar una base gratuita sin actividad; activar ambos servicios antes de cada demostración.

• **Sobre los contextos pendientes**: implementar en los siguientes sprints los Web Services de Monitoring and Alerts, Notifications y Analytics and Reporting, que hoy se muestran solo con datos simulados.

# Bibliografía

Career Foundry. (s.f.). What are user flows in User Experience (UX) Design? CareerFoundry.
https://careerfoundry.com/en/blog/ux-design/what-are-user-flows/

Conventional Commits. (s.f.). Conventional Commits 1.0.0. https://www.conventionalcommits.org/

Dittrich, J. (s.f.). A beginner's guide to finding user needs. https://jdittrich.github.io/userNeedResearchBook/

Domain Storytelling. (s.f.). Domain storytelling and requirements. https://domainstorytelling.org/#dst-requirements

Driessen, V. (2010). A successful Git branching model. nvie.com. https://nvie.com/posts/a-successful-git-branchingmodel/

DZone. (s.f.). Acceptance criteria in Scrum: Explanation, examples, and template.
https://dzone.com/articles/acceptance-criteria-in-software-explanation-exampl

IBM. (s.f.-a). As-is scenario map: Build a better understanding of your users' current experience.
https://www.ibm.com/design/thinking/page/toolkit/activity/as-is-scenario-map

IBM. (s.f.-b). Empathy map: Build empathy for your users through a conversation informed by your team's observations.
https://www.ibm.com/design/thinking/page/toolkit/activity/empathy-map

IBM. (s.f.-c). To-be scenario map: Draft a vision of your user's future experience to show how your ideas address their
current needs. https://www.ibm.com/design/thinking/page/toolkit/activity/to-be-scenario-map

Nielsen Norman Group. (s.f.-a). Design systems 101. https://www.nngroup.com/articles/design-systems-101/

Nielsen Norman Group. (s.f.-b). Empathy mapping: The first step in design thinking.
https://www.nngroup.com/articles/empathy-mapping/

Noamtamim. (s.f.). How to use PlantUML with Markdown [Gist]. GitHub.
https://gist.github.com/noamtamim/f11982b28602bd7e604c233fbe9d910f

Open Practice Library. (s.f.-b). Ubiquitous language: Unambiguously define the terms and concepts of a business
domain. https://openpracticelibrary.com/practice/ubiquitous-language/

Scribd. (s.f.). Lean UX – Chapter 3. https://www.scribd.com/document/655516553/Leanux-Sampler

The DDD by Examples Community. (s.f.-a). Big Picture EventStorming. GitHub. https://github.com/ddd-byexamples/library/blob/master/docs/big-picture.md

The DDD by Examples Community. (s.f.-b). Design-level EventStorming. GitHub. https://github.com/ddd-byexamples/library/blob/master/docs/design-level.md

The Markdown Guide. (s.f.). The Markdown Guide. https://www.markdownguide.org/

UXforTheMasses. (s.f.). A step-by-step guide to scenario mapping. http://www.uxforthemasses.com/scenario-mapping/

UXPressia. (s.f.-a). How to create an Impact Map in 4 easy steps? https://uxpressia.com/blog/build-impact-map-4-easysteps

UXPressia. (s.f.-b). User vs. buyer persona: Differences and free template. https://uxpressia.com/blog/user-persona-vsbuyer-persona-difference

Zhurb, A. [connect2grp]. (s.f.). Using PlantUML for creating clear and concise diagrams. Medium.
https://connect2grp.medium.com/using-plantuml-for-creating-clear-and-concise-diagrams-2fc621529560

Aiven. (2026). *Aiven for MySQL free tier*. https://aiven.io/docs/products/mysql/concepts/mysql-free-tier

Docker Inc. (s.f.). *Docker Compose overview*. https://docs.docker.com/compose/

Google. (s.f.). *Firebase pricing*. https://firebase.google.com/pricing

Jones, M., Bradley, J., & Sakimura, N. (2015). *JSON Web Token (JWT)* (RFC 7519). IETF. https://www.rfc-editor.org/rfc/rfc7519

Microsoft. (s.f.-a). *ASP.NET Core documentation*. https://learn.microsoft.com/aspnet/core/

Microsoft. (s.f.-b). *Entity Framework Core: Migrations overview*. https://learn.microsoft.com/ef/core/managing-schemas/migrations/

Microsoft. (s.f.-c). *Integration tests in ASP.NET Core*. https://learn.microsoft.com/aspnet/core/test/integration-tests

Nielsen, J. (1994). *10 usability heuristics for user interface design*. Nielsen Norman Group. https://www.nngroup.com/articles/ten-usability-heuristics/

Oracle. (s.f.). *MySQL Connector/NET Developer Guide: Entity Framework Core support*. https://dev.mysql.com/doc/connector-net/en/connector-net-entityframework-core.html

OpenAPI Initiative. (s.f.). *OpenAPI Specification*. https://spec.openapis.org/oas/latest.html

Render. (2026). *Deploy for free*. https://render.com/docs/free

# Anexos

## Anexo A. Videos de Exposiciones

| Entrega | Título                                                                                                   | Enlace        |
|--------|----------------------------------------------------------------------------------------------------------|---------------|
| AV1 | Presentación de la propuesta de negocio, Lean UX Process y primera versión del Landing Page| https://lix.li/U50Z |
| TB1 | Especificación de requisitos (User Stories, Technical Stories, Impact Mapping y Product Backlog) y propuesta de Product Design | https://lix.li/uZ4zu |
| TB2 | Exposición del Sprint 3 | [PENDIENTE: URL] |
| TB2 | Video About-the-Product (primera versión) | [PENDIENTE: URL] |
| TB2 | Video About-the-Team (primera versión) | [PENDIENTE: URL] |

## Anexo B. Repositorios del Proyecto

| Descripción                          | Enlace |
|--------------------------------------|--------|
| Repositorio del Informe del Proyecto | https://github.com/upc-pre-202620-1asi0730-8074-ApexCode/easypark-report       |
| Repositorio de la Landing Page       | https://github.com/upc-pre-202620-1asi0730-8074-ApexCode/easypark-landing |
| Repositorio de la Aplicación Web     | https://github.com/upc-pre-202620-1asi0730-8074-ApexCode/easypark-webapp |
| Repositorio de los Web Services (RESTful API) | [PENDIENTE: URL] |

## Anexo C. Enlaces de Despliegue (Deployment)

| Descripción                                          | Enlace |
|------------------------------------------------------|--------|
| Deployment de la Landing Page en GitHub Pages        | https://upc-pre-202620-1asi0730-8074-apexcode.github.io/easypark-landing/ |
| Deployment de la Aplicación Web | https://easypark-5ffb2.web.app/ (versión publicada anteriormente; [PENDIENTE: confirmar tras desplegar la versión integrada con el API]) |
| Deployment de los Web Services (Swagger UI) | [PENDIENTE: URL]/swagger |

## Anexo D. Diseño

| Descripción | Enlace                                                                                               |
|------------|------------------------------------------------------------------------------------------------------|
| Link del Figma del Trabajo | https://www.figma.com/design/kNri7YrOA48AbqzttpgeZw/apex-code?node-id=48-3&p=f&t=RGPO5DCljllWouH8-0  |

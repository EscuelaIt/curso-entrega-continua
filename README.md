# Curso de Entrega Continua

Este repositorio es el **proyecto guía** del curso de Integración y Despliegue Continuo (CI/CD).

### Roadmap del curso (sesiones y entregables)

#### 1 - Introducción al concepto de entrega continua

En esta primera sesión se presenta qué problema busca resolver la entrega continua: reducir el costo, el tiempo y el riesgo del cambio. Se introduce la diferencia entre integración continua, entrega continua y despliegue continuo, y se plantea al pipeline de despliegue como la representación ejecutable del proceso de entrega, no como una simple cadena de tareas.

#### 2 - ¿Cómo trabajar para integrar y entregar con frecuencia?

Esta sesión se concentra en las condiciones que hacen viable la integración frecuente: cambios pequeños, bajo trabajo en progreso y trabajo cercano a la rama principal. El foco está puesto en el diseño del software como habilitador del delivery, mostrando por qué la legibilidad, la cohesión, el bajo acoplamiento, la testabilidad y una buena distribución de responsabilidades reducen el costo de cambio y facilitan ramas cortas e integración temprana.

#### 3 - Desempeño en la entrega de software: el enfoque de Accelerate

En esta sesión se introduce *Accelerate* como marco para medir el desempeño de entrega de software con evidencia empírica. Se trabajan las cuatro métricas principales —lead time, deployment frequency, change failure rate y time to restore service— para entender el delivery como un sistema y discutir cómo velocidad y estabilidad pueden mejorar en conjunto.

#### 4 - La arquitectura como habilitador de la entrega continua
Analizamos qué características arquitectónicas facilitan CD: bajo acoplamiento, separación de responsabilidades, límites claros entre componentes y evolución segura del sistema. Introducimos el concepto de **compatibilidad hacia atrás** (API/DB) como requisito práctico, no teórico, y cómo pensar la modularidad con una mirada medible (métricas de componentes, dependencias, puntos de fricción).

#### 5 - Pruebas automatizadas
Nos metemos en testing con criterio de entrega continua: qué tipos de pruebas convienen (unitarias, integración, arquitectura) y por qué el objetivo es **reducir incertidumbre rápido**. Vemos cómo una estrategia de tests mal planteada puede frenar el delivery (tests lentos, frágiles, duplicados) y cómo construir un set mínimo que actúe como red de seguridad real para integrar cambios con frecuencia.

#### 6 - Deployment Pipeline
Construimos la idea de “pipeline” como mecanismo de feedback y control de riesgo, no como un script. Vemos buenas prácticas: stages, separación CI/CD, artefactos, promoción, trazabilidad, y gates de calidad. Luego aterrizamos esto en el proyecto guía: cómo se automatiza el despliegue a un entorno (staging) y cómo se valida post-deploy (smoke tests / healthchecks) para evitar “deploy exitoso pero sistema roto”.

#### 7 - Integración de scripts DDL y configuración de entornos al esquema de despliegue continuo


#### 8 - Release strategies y feature flags
En esta sesión ampliamos el alcance: CD/CI no termina en “subir binarios”. Introducimos **Infraestructura como Código** para reducir variabilidad y dependencia de configuraciones manuales, y definimos un mínimo de observabilidad para operar: health/readiness, logs, métricas básicas y alertas.

#### 9 - Operación y observabilidad
Vemos qué prácticas de trabajo son coherentes con CI/CD: DevOps como enfoque socio-técnico, XP como origen de muchas prácticas técnicas (CI, TDD, refactoring, small releases) y Agile como marco de gestión. La idea no es “repasar metodologías”, sino entender qué comportamientos y restricciones organizacionales habilitan o bloquean el delivery continuo: tamaño de lote, gestión de WIP, definición de terminado, ownership, y cultura de aprendizaje.

#### 10 - Capabilities, adopción y roadmap
Cerramos uniendo piezas que suelen quedar sueltas: **feature flags**, estrategias de branching (trunk-based vs variantes), **semantic versioning**, versionado de APIs, y **migraciones** seguras. También armamos un mapa de adopción realista: por dónde empezar en una organización, qué anti-patrones evitar (gates burocráticos, pipelines lentos, “CI siempre rojo”), y cómo sostener una mejora continua usando métricas. Esta clase funciona como síntesis: del concepto al plan aplicable.
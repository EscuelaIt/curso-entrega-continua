# Curso CI/CD — Proyecto guía

Este repositorio es el **proyecto guía** del curso de Integración y Despliegue Continuo (CI/CD).  
La intención es que el alumno vea el valor real de CD/CI y entienda que **no alcanza con “armar un pipeline”**: el software debe tener condiciones mínimas de **calidad, testabilidad, compatibilidad y operabilidad** para poder desplegar seguido con bajo riesgo.

## Qué vas a construir (resultado)

Al finalizar el curso, este repo queda con:

- **CI** con quality gates (build + tests + análisis estático + artefacto).
- **CD a staging** automático con **smoke tests post-deploy**.
- **Migraciones DB** seguras (patrón **expand/contract**).
- **Feature flags** y estrategia de release (progresivo/simulado).
- **Observabilidad mínima** (health, logs útiles, métrica simple + alerta).
- **Tablero** (o medición aproximada) de métricas **DORA**: lead time, deploy frequency, change failure rate, MTTR.

> Nota: el proyecto trae “dolores” intencionales para que las prácticas tengan sentido. Están diseñados para resolverse incrementalmente.

---

## Stack del proyecto

- **.NET**: API (Minimal API o Web API)
- **DB**: PostgreSQL (recomendado) o SQL Server
- **Infra local**: Docker Compose
- **CI/CD**: GitHub Actions (adaptable a Azure DevOps)
- **Migraciones**: EF Core Migrations (o Flyway/Liquibase si el curso lo decide)

---

## Estructura

```
/src
  /App.Api               # API REST
  /App.Domain            # Dominio (reglas + entidades)
  /App.Infrastructure    # Acceso a datos + repositorios
/tests
  /App.UnitTests         # Tests unitarios
  /App.IntegrationTests  # Tests de integración (DB real)
/infra
  docker-compose.yml     # DB local
  scripts/               # scripts de soporte (migraciones, seed, etc.)
/.github/workflows
  ci.yml                 # pipeline CI
  cd-staging.yml         # pipeline CD (staging)
```

---

## Dominio (simple y deliberado)

Caso típico: **Orders / Inventory**.

- Endpoints CRUD básicos para Orders
- Un par de reglas de negocio (ej. no permitir cancelar orden enviada)
- Persistencia en DB

El dominio es simple a propósito: el foco del curso es delivery, no el negocio.

---

## Requisitos para desarrollo local

- .NET SDK (versión definida en `global.json` o documentación del curso)
- Docker Desktop
- Git

Opcional:

- `dotnet-ef` (si el curso usa EF migrations)
- `curl` o Postman para probar endpoints

---

## Levantar el proyecto localmente

### 1) Base de datos (Docker)

Desde la raíz del repo:

```bash
docker compose -f infra/docker-compose.yml up -d
```

### 2) Configuración

Copiar variables de entorno (ejemplo):

```bash
# Linux/Mac
export ConnectionStrings__AppDb="Host=localhost;Port=5432;Database=app;Username=app;Password=app"

# Windows PowerShell
$env:ConnectionStrings__AppDb="Host=localhost;Port=5432;Database=app;Username=app;Password=app"
```

### 3) Migraciones (si aplica)

```bash
dotnet tool restore
dotnet ef database update --project src/App.Infrastructure --startup-project src/App.Api
```

### 4) Ejecutar API

```bash
dotnet run --project src/App.Api
```

### 5) Smoke test básico

```bash
curl -f http://localhost:5000/health
```

---

## Convenciones de trabajo (obligatorias en el curso)

- **Trunk-based development**
  - `main` es la rama principal
  - cambios pequeños y frecuentes
  - PRs cortos con revisión
- **Branch protection**: no se puede mergear a `main` sin CI verde
- **Definition of Done (mínimo)**:
  - build OK
  - tests OK
  - linters/analyzers OK
  - (cuando aplique) smoke test OK en staging

---

## “Problemas intencionales” del proyecto (para aprender)

Estos problemas están a propósito y se van resolviendo en el transcurso del curso:

- Configuración hardcodeada / manejo pobre de secretos
- Falta de health/readiness real
- Tests insuficientes (pipeline verde pero calidad baja)
- Migraciones DB peligrosas si no se aplican patrones
- Cambios no backward compatible (API/DB) preparados como ejercicios
- Observabilidad mínima o inexistente (para discutir MTTR)

---

# Roadmap del curso (sesiones y entregables)

Cada sesión agrega un **gate** o una capacidad concreta.  
Entre sesiones hay una tarea práctica. Al iniciar cada clase se revisan soluciones ~20 min.

## Sesión 1 — Marco y objetivo del curso
Arrancamos con una visión general de qué es CI/CD y qué problemas reales busca resolver (tiempo de entrega, riesgo, retrabajo). Se explica la dinámica del curso: trabajo en grupos, tareas entre clases y revisión breve al inicio de cada sesión. Presentamos el **proyecto guía** ya armado (el “sistema sobre el que vamos a trabajar”) y dejamos listo el entorno: cuentas, repositorios, acceso a herramientas y una primera corrida end-to-end para que todos partan de una base común. También introducimos **Accelerate** como marco de referencia para medir y mejorar.

Literatura: qué problema resuelve CD/CI (costo de delay, riesgo, feedback).  
Conceptos: CI ≠ CD, “deployment pipeline” como sistema.  
Práctica: correr el proyecto, primer CI mínimo.  
Lectura: intro de Accelerate + capítulo inicial de Continuous Delivery (pipeline/feedback).

## Sesión 2 — Flujo: batch size, WIP, trunk-based
En esta clase ponemos el foco en qué condiciones mínimas necesita un sistema para soportar despliegues frecuentes. Hablamos de calidad como habilitador (no como “perfeccionismo”): pruebas automatizadas, diseño que facilite cambios, y decisiones de arquitectura que impactan directamente en la capacidad de integrar y desplegar sin drama. La idea es bajar a tierra por qué CI/CD se vuelve frágil cuando el software está acoplado, no es testeable o depende de pasos manuales.

Literatura: principios Lean/flow que soportan performance.  
Conceptos: trunk-based vs GitFlow (tradeoffs reales).  
Práctica: branch protection + PR pequeño + reglas de merge.  
Lectura: sección de flow + continuous integration.

## Sesión 3 — Métricas DORA bien entendidas
Introducimos las 4 métricas de **Accelerate** (DORA) como lenguaje común para evaluar performance de entrega: lead time, frecuencia de despliegue, change failure rate y MTTR. No es una clase “de indicadores” aislada: la usamos para entender qué vamos a optimizar durante el curso y cómo evitar métricas vanidosas. Se deja lectura asignada del libro y se define cómo vamos a observar estas métricas (aunque sea de forma aproximada) sobre el proyecto guía.

Literatura: DORA metrics, qué miden y qué NO.  
Conceptos: lead time por etapas, deploy freq, CFR, MTTR.  
Práctica: instrumentación mínima (marcar eventos en el pipeline).  
Lectura: capítulos de métricas/outcomes.

## Sesión 4 — Calidad: testing como habilitador (no “cultura de tests”)
Nos metemos en testing con criterio de entrega continua: qué tipos de pruebas convienen (unitarias, integración, arquitectura) y por qué el objetivo es **reducir incertidumbre rápido**. Vemos cómo una estrategia de tests mal planteada puede frenar el delivery (tests lentos, frágiles, duplicados) y cómo construir un set mínimo que actúe como red de seguridad real para integrar cambios con frecuencia.

Literatura: calidad como reducción de riesgo y aceleración del feedback.  
Conceptos: pirámide de tests, costo de test lento, confiabilidad.  
Práctica: agregar 1 test de integración determinista + gate.  
Lectura: testing strategy / deployment pipeline confidence.

## Sesión 5 — Arquitectura para despliegue continuo
Analizamos qué características arquitectónicas facilitan CD: bajo acoplamiento, separación de responsabilidades, límites claros entre componentes y evolución segura del sistema. Introducimos el concepto de **compatibilidad hacia atrás** (API/DB) como requisito práctico, no teórico, y cómo pensar la modularidad con una mirada medible (métricas de componentes, dependencias, puntos de fricción). La clase busca que el alumno conecte arquitectura con capacidad de desplegar seguido.

Literatura: acoplamiento, modularidad, deployability.  
Conceptos: cambios backward-compatible, seams, “release ≠ deploy”.  
Práctica: ejemplo de cambio compatible (API/DB).  
Lectura: diseño para deploy, independencia de despliegue.

## Sesión 6 — Deployment Pipeline (diseño serio)
Construimos la idea de “pipeline” como mecanismo de feedback y control de riesgo, no como un script. Vemos buenas prácticas: stages, separación CI/CD, artefactos, promoción, trazabilidad, y gates de calidad. Luego aterrizamos esto en el proyecto guía: cómo se automatiza el despliegue a un entorno (staging) y cómo se valida post-deploy (smoke tests / healthchecks) para evitar “deploy exitoso pero sistema roto”. *(Si querés mantener un ecosistema Blazor/API/SQL/Mobile, acá se presenta como mapa general y se define qué parte es core y qué queda como extensión.)*

Literatura: stages, quality gates, fast feedback, artifact promotion.  
Conceptos: separación CI/CD, ambientes, trazabilidad.  
Práctica: CD a staging + smoke test post-deploy.  
Lectura: deployment pipeline patterns.

## Sesión 7 — DB en CD (el infierno clásico)
Retomamos **Accelerate** con más detalle, pero ahora con contexto: conectamos prácticas concretas (branching, pruebas, automatización, despliegue, observabilidad) con impacto en métricas DORA. La intención es que el alumno entienda que los indicadores no son “reporting”, sino una forma de decidir qué mejorar primero. También discutimos limitaciones típicas al medir (qué se rompe cuando hay procesos manuales, ambientes inestables o releases grandes).

Literatura: deployments de DB, riesgos, estrategias.  
Conceptos: expand/contract, migraciones seguras, rollback vs forward-fix.  
Práctica: migración en 2 pasos + verificación.  
Lectura: database deployment.

## Sesión 8 — Release strategies y feature flags
En esta sesión ampliamos el alcance: CD/CI no termina en “subir binarios”. Introducimos **Infraestructura como Código** para reducir variabilidad y dependencia de configuraciones manuales, y definimos un mínimo de observabilidad para operar: health/readiness, logs, métricas básicas y alertas. El objetivo es que el alumno vea el vínculo directo con MTTR y change failure rate: sin monitoreo, los errores se detectan tarde y se recupera lento.

Literatura: reducir blast radius, experimentación, control de exposición.  
Conceptos: canary/blue-green/rolling, flags y deuda de flags.  
Práctica: flag + “release” sin exponer.  
Lectura: release patterns / progressive delivery.

## Sesión 9 — Operación, observabilidad y MTTR
Vemos qué prácticas de trabajo son coherentes con CI/CD: DevOps como enfoque socio-técnico, XP como origen de muchas prácticas técnicas (CI, TDD, refactoring, small releases) y Agile como marco de gestión. La idea no es “repasar metodologías”, sino entender qué comportamientos y restricciones organizacionales habilitan o bloquean el delivery continuo: tamaño de lote, gestión de WIP, definición de terminado, ownership, y cultura de aprendizaje.

Literatura: feedback de producción como parte del sistema.  
Conceptos: health/readiness, logs/métricas/traces, alertas y SLO básico.  
Práctica: alerta mínima + simulacro de incidente.  
Lectura: incident response / feedback loops.

## Sesión 10 — Capabilities, adopción y roadmap
Cerramos uniendo piezas que suelen quedar sueltas: **feature flags**, estrategias de branching (trunk-based vs variantes), **semantic versioning**, versionado de APIs, y **migraciones** seguras. También armamos un mapa de adopción realista: por dónde empezar en una organización, qué anti-patrones evitar (gates burocráticos, pipelines lentos, “CI siempre rojo”), y cómo sostener una mejora continua usando métricas. Esta clase funciona como síntesis: del concepto al plan aplicable.

Literatura: capabilities de Accelerate (tech + org), cómo priorizar.  
Conceptos: anti-patrones (gates burocráticos, “CI rojo permanente”, ambientes infierno).  
Práctica: tablero DORA aproximado + plan de mejora por equipo.  
Lectura: capítulos finales de Accelerate + cierre Continuous Delivery.

## Cómo se evalúa (criterio técnico)

- El repo **compila** y el CI es reproducible
- Los **gates** están justificados (no burocracia)
- Las decisiones priorizan: cambios pequeños, automatización, feedback rápido
- Los cambios respetan compatibilidad (API/DB) cuando corresponde
- Existe verificación post-deploy (smoke) y una historia de recuperación (rollback/forward-fix)

---

## Notas para el instructor (operación del curso)

- Mantener ramas `solution/session-X` con la solución por sesión
- Preparar PRs “trampa”:
  - cambio que rompe compatibilidad API
  - migración destructiva
  - deploy “exitoso” pero app no responde
- Mantener “incidentes controlados” reproducibles para sesión 9
- Minimizar el trabajo de UI: si hay UI, que sea decorativa y mínima

---

## Licencia / uso

Uso educativo. El objetivo es aprender prácticas de delivery, no proveer un producto final.

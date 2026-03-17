## Estructura del curso

#### Finalidad: ¿Para qué?

- reducir el costo, el tiempo y el riesgo del cambio;
- mantener el software en estado liberable;
- acortar el ciclo entre cambio y feedback;
- aumentar la capacidad de recuperación ante fallas;
- y hacer que la entrega sea una capacidad organizacional estable, no un evento excepcional.

El propósito de estas prácticas es mantener el sistema en un estado permanentemente integrable, verificable y liberable, de modo que la puesta en producción pueda realizarse bajo demanda y no quede condicionada por tareas técnicas pendientes, por deuda operativa acumulada o por procesos de estabilización prolongados. La idea de fondo no es simplemente **automatizar despliegues**, sino transformar la entrega de software en una capacidad estable del sistema. Esto implica que cada cambio, desde etapas tempranas, atraviese mecanismos que permitan integrarlo, validarlo y promoverlo con evidencia suficiente sobre su corrección y su impacto probable.

La mejora del delivery solo es significativa si combina rapidez y estabilidad. Liberar más veces sin reducir la tasa de fallas o sin mejorar la capacidad de recuperación no constituye madurez de delivery, sino aceleración del desorden. Por eso, la finalidad de CI/CD debe formularse en términos más amplios: 
- disminuir el tiempo entre la producción de un cambio y su validación en condiciones reales;
- reducir el riesgo asociado a la integración y al release;
- aumentar la visibilidad del proceso de entrega;
- y fortalecer la capacidad de recuperación cuando un cambio introduce una degradación o un incidente.

La entrega continua, entendida de este modo, no es un mecanismo accesorio del desarrollo, sino una condición para que el software pueda evolucionar sin que cada modificación amenace la estabilidad del sistema completo.

#### Fundamentos: ¿Por qué?

- la integración tardía incrementa el costo del error;
- los lotes grandes acumulan incertidumbre;
- los procesos manuales aumentan variabilidad e imprevisibilidad;
- el feedback tardío vuelve más costosa la corrección;
- la falta de recuperación rápida eleva el impacto de las fallas.

El concepto de tamaño de lote adquiere centralidad. Cuanto mayor es el lote de cambios que se integra o despliega: - - mayor es la complejidad cognitiva para comprenderlo,
- mayor es la dificultad de revisar sus efectos,
- mayor es el costo de localizar la causa de una falla
- y mayor es la incertidumbre acumulada antes de obtener feedback.

La reducción del tamaño de lote no es, por tanto, un principio de estilo, sino:
- una manera de disminuir variabilidad,
- acelerar la detección de errores
- y reducir el costo de corrección.

El flujo de trabajo que favorece CI/CD es, en consecuencia, un flujo con cambios pequeños, integración frecuente y baja acumulación de trabajo parcialmente terminado.

Los errores de integración, compatibilidad, comportamiento funcional o impacto no funcional suelen volverse más costosos cuanto más tarde se detectan. Por eso, la estrategia de entrega continua insiste en construir mecanismos automáticos de validación que permitan detectar rápidamente cuándo un cambio introduce una regresión, viola una restricción o reduce la capacidad operativa del sistema.

#### Mecanismos: ¿Cómo?

La integración y el despliegue continuo no se realizan mediante una única técnica ni por medio de una sola herramienta, sino a través de un conjunto articulado de prácticas, decisiones de arquitectura y mecanismos operativos. Estos mecanismos tienen como finalidad:
- volver posible la integración frecuente,
- la validación temprana,
- la liberación segura
- y la recuperación rápida ante fallas.

Algunos ejemplos:
- integración continua;
- control de versiones;
- estrategias de pruebas automatizadas;
- implementación de pipelines;
- uso de artefactos;
- automatización del despliegue;
- gestión de cambios de base de datos;
- estrategias de release;
- feature flags;
- observabilidad y monitoreo;
- métricas de desempeño de delivery.

#### Material

- [Continuous Delivery](https://martinfowler.com/books/continuousDelivery.html)
- [Accelerate](https://www.amazon.com/Accelerate-Software-Performing-Technology-Organizations/dp/1942788339)
- [Proyecto Liga Libre API](https://github.com/emigallo-edu/liga-libre-api)
- [Proyecto Liga Libre Web](https://github.com/emigallo-edu/liga-libre-web)


#### Conocimiento necesario
- [Master - Diseño OO](https://escuela.it/cursos/curso-de-diseno-orientado-a-objetos/estudiar)
- [Master - Arquitecturas](https://escuela.it/cursos/curso-arquitecturas-software-agiles-pesadas/estudiar)
- [Master - Pruebas](https://escuela.it/cursos/pruebas-software/estudiar)

--------

## Introducción

#### Objetivos de la práctica

>Nuestro objetivo es hacer que la entrega de software desde las manos de los desarrolladores hasta la producción sea un proceso confiable, predecible, visible y en gran medida automatizado con riesgos cuantificables y bien comprendidos.
>
> Continuous Delivery - Jez Humble & David Farley

No se trata de “desplegar más seguido” como fin en sí mismo, sino hacer que la entrega de software sea repetible, confiable y de bajo riesgo.

La estrategia busca que una organización pueda:
- poner cambios en producción en cualquier momento, si el negocio lo decide;
- reducir el riesgo del release, evitando despliegues traumáticos, manuales y llenos de incertidumbre;
- acortar el tiempo entre una idea y su validación real, obteniendo feedback antes;
- mejorar la calidad, porque cada cambio pasa continuamente por build, pruebas y validaciones;
- hacer del release una actividad rutinaria, y no un evento excepcional.

El objetivo de Continuous Delivery es mantener el software siempre en un estado desplegable, de modo que liberarlo a producción sea una decisión de negocio y no una limitación técnica.

No significa que todo se publique automáticamente, sino que el equipo no quede frenado porque “todavía falta estabilizar”, “hay que correr scripts manuales” o “nadie sabe si esto va a romper”.

>La entrega continua es una disciplina de desarrollo de software que consiste en crear software de forma que pueda implementarse en producción en cualquier momento.
>
>Se aplica la entrega continua cuando:
>
>- El software es desplegable durante todo su ciclo de vida.
>- El equipo prioriza la disponibilidad del software sobre el desarrollo de nuevas funcionalidades.
>- Cualquier persona puede obtener retroalimentación rápida y automatizada sobre la preparación > -Para producción de sus sistemas cada vez que se realiza un cambio.
> - Se pueden realizar implementaciones automáticas de cualquier versión del software en cualquier entorno, bajo demanda.
>
> [Martin Fowler](https://martinfowler.com/bliki/ContinuousDelivery.html)

#### ¿Qué problemas resuelve?
CI/CD existe para reducir el costo y el riesgo del cambio. No para “automatizar por automatizar”, no para verse modernos, y tampoco para desplegar más veces porque sí. El problema de fondo es que, cuando los cambios se acumulan durante mucho tiempo, se vuelven más difíciles de integrar, más difíciles de probar, más difíciles de explicar y más costosos de revertir.

Tres conceptos que van a atravesar todo el curso:
- **Lote** de cambio: cuántas modificaciones acumulamos antes de integrar o desplegar.
- **Feedback**: cuánto tarda el sistema en decirnos si lo que hicimos está bien o mal.
- **Riesgo**: cuánta incertidumbre acumulamos antes de enterarnos de que hay un problema.

La relación entre estos tres conceptos es directa. Cuanto más grande el lote, más tarde llega el feedback. Cuanto más tarde llega el feedback, más caro resulta entender qué pasó. Y cuanto más caro es entenderlo, mayor es el riesgo operativo y de negocio.

#### Diferencia entre Integración, Entrega y Despliegue Continuo

Integración continua es la práctica de integrar frecuentemente en una línea principal compartida, validando cada integración con build y pruebas automáticas. Su objetivo no es desplegar, sino evitar que la integración sea un evento tardío, traumático y costoso.

Entrega continua toma esa base y la extiende. No alcanza con integrar seguido: además hay que asegurar que el sistema quede siempre en un estado liberable. Eso significa que cualquier cambio aceptado por el pipeline podría, en principio, llegar a producción de manera rutinaria. La palabra importante es “liberable”. No significa que todo se publique automáticamente, sino que la decisión de release deja de depender de trabajos técnicos pendientes.

Despliegue continuo, es un caso más extremo: todo cambio que pasa satisfactoriamente por el pipeline se despliega automáticamente a producción. Se puede efectuar Entrega Continua sin hacer Despliegue Continuo.

#### El pipeline de despliegue como sistema

No es una cadena de tareas, sino la representación ejecutable del proceso de entrega. Cada etapa del pipeline responde una pregunta distinta sobre el cambio:

1- ¿compila y se integra?
2- ¿rompe comportamiento esperado?
3- ¿cumple restricciones no funcionales?
4- ¿puede desplegarse con seguridad?
5- ¿está listo para ser promovido?

Lo importante es que el pipeline cumple una doble función. Por un lado, da feedback técnico temprano. Por otro, hace visible y trazable el proceso de entrega. El pipeline, en ese sentido, no es solo automatización: es una forma de hacer explícito qué evidencia exigimos antes de confiar en un cambio. *Continuous Delivery* lo presenta como “Anatomy of the Deployment Pipeline”: como el mecanismo central que estructura la entrega de software.

#### Métricas de Accelerate

Accelerate es un libro de síntesis y divulgación académicamente fundamentada que presenta resultados de investigación empírica sobre desempeño en entrega de software y sobre las capacidades técnicas y organizacionales asociadas a equipos de alto rendimiento.

Es un libro que busca responder, con base empírica, una pregunta central de la ingeniería de software moderna: cómo medir el desempeño de entrega de software y qué capacidades organizacionales y técnicas lo explican. Su aporte distintivo es que intenta fundamentar estas prácticas mediante investigación cuantitativa y análisis estadístico.

Su tesis central es que el desempeño en la entrega de software sí puede medirse y que, además, se relaciona con el desempeño global de la organización. Para eso, los autores proponen un marco de medición hoy muy conocido: las cuatro métricas de delivery.

###### 1. Deployment Frequency
Mide con qué frecuencia un equipo despliega cambios a producción.
Alta frecuencia suele indicar capacidad de trabajar en cambios pequeños y liberarlos sin demasiado costo operativo.
No mide valor de negocio por sí sola; mide capacidad de entrega.

###### 2. Lead Time for Changes
Mide cuánto tarda un cambio desde que se integra al sistema hasta que llega a producción.
Captura la velocidad real del flujo de entrega.
Obliga a mirar el proceso completo, no solo cuánto tarda “programar”.

###### 3. Change Failure Rate
Mide qué proporción de los cambios desplegados en producción provoca fallas que requieren intervención, como rollback, hotfix o corrección urgente.
Es una métrica de estabilidad.
No pregunta cuántos bugs existen en abstracto, sino cuántos cambios generan problemas operativos reales.

###### 4. Time to Restore Service (MTTR)
Mide cuánto tarda el equipo en restaurar el servicio cuando ocurre una falla o degradación.
Refleja capacidad de recuperación.
No depende solo de “arreglar rápido”, sino también de observabilidad, trazabilidad, tamaño de los cambios y mecanismos de rollback o forward-fix.

Desde el punto de vista conceptual, Accelerate puede leerse como una obra que traduce ideas provenientes de Lean, DevOps y delivery continuo a un lenguaje de capacidades medibles. El libro sostiene que el alto desempeño no depende principalmente de herramientas aisladas, sino de un conjunto coherente de prácticas técnicas, arquitectónicas, organizacionales y culturales, como integración continua, trabajo en lotes pequeños, versionado adecuado, automatización, buena arquitectura, monitoreo y culturas de aprendizaje más generativas.

Estas métricas nos obligan a mirar el delivery como un sistema y no como una suma de tareas aisladas. Dos miden velocidad, dos estabilidad. El objetivo no es elegir entre rapidez y confiabilidad, sino mejorar ambas en conjunto. Accelerate presenta precisamente esa combinación como núcleo de desempeño de delivery.

#### Propiedades deseables
###### 1. Mantener la aplicación siempre liberable

El software debe diseñarse y desarrollarse de modo tal que pueda liberarse a producción en cualquier momento. Eso obliga a pensar el diseño no solo en términos de funcionalidad, sino también de entregabilidad: cambios pequeños, integración frecuente, validación continua y ausencia de trabajo técnico pendiente para poder liberar.

###### 2. Favorecer cambios pequeños e integración frecuente

Los cambios grandes son más difíciles de entender, probar, integrar y revertir. Por eso, un principio de diseño clave es estructurar el sistema y el trabajo de forma que sea posible introducir incrementos pequeños, integrarlos rápidamente a la línea principal y obtener feedback temprano. Esto se relaciona directamente con que estrategía de **branching** vamos a trabajar y con evitar ramas largas como modo normal de trabajo.

###### 3. Diseñar para testabilidad

La testabilidad no aparece como una virtud secundaria, sino como una condición central de entregabilidad. Un sistema apto para CI/CD debe poder validarse rápida y repetidamente mediante pruebas automatizadas en distintos niveles. Eso implica favorecer diseños con responsabilidades claras, dependencias controladas, facilidad de aislamiento y comportamiento observable. Si un sistema es difícil de probar, también será difícil de integrar y de liberar con confianza.

###### 4. Reducir acoplamiento y gestionar explícitamente dependencias

El acoplamiento excesivo vuelve cada cambio más costoso. Un principio fuerte, entonces, es diseñar sistemas donde las dependencias sean explícitas, trazables y manejables, evitando que un cambio aparentemente local obligue a coordinar múltiples partes del sistema al mismo tiempo. Esto aplica tanto a bibliotecas y componentes como a dependencias entre aplicaciones, servicios y bases de datos.

###### 5. Separar deploy de release

Una aplicación bien diseñada para CI/CD debería permitir desplegar sin necesariamente exponer inmediatamente toda nueva funcionalidad. Esa separación entre movimiento técnico del software y decisión de negocio sobre su exposición reduce riesgo y facilita cambios más frecuentes. De ahí se desprenden después mecanismos como toggles o estrategias progresivas de release, pero el principio previo es de diseño: no obligar a que cada despliegue implique exposición inmediata e irreversible.

###### 6. Diseñar para compatibilidad evolutiva

Los sistemas que soportan CI/CD deben evolucionar de forma compatible, evitando cambios destructivos que exijan sincronización perfecta entre todos los componentes. Esto vale para APIs, contratos entre componentes y, de manera muy marcada, para esquemas de base de datos. El principio general es privilegiar cambios aditivos y reversibles frente a cambios abruptos y destructivos.

###### 7. Tratar la configuración, la infraestructura y los datos como parte del sistema

La capacidad de delivery depende también de configuración, infraestructura, scripts de despliegue y base de datos. Por eso, un diseño compatible con CI/CD debe minimizar dependencias implícitas del entorno, externalizar adecuadamente configuración y hacer que los cambios en esos elementos sean versionables, repetibles y automatizables. En términos de diseño, esto significa evitar aplicaciones que “funcionan solo en un ambiente particular” o que dependen de intervención manual opaca para correr correctamente.

###### 8. Construir binarios/artefactos verdaderamente desplegables

El build debe producir artefactos que puedan copiarse a una máquina correctamente configurada y ejecutarse sin depender de la cadena de desarrollo. Traducido a principio de diseño: el sistema debe empaquetarse de manera que el artefacto producido sea autosuficiente en términos operativos razonables, portable entre ambientes y apto para promoción sin reconstrucciones ad hoc. Esto reduce variabilidad entre entornos y aumenta trazabilidad.

###### 9. Hacer visible el comportamiento del sistema en operación

Un diseño compatible con CI/CD es que la aplicación debe exponer suficientes señales para verificar si está viva, lista y funcionando razonablemente tras un despliegue. En términos modernos, esto implica diseñar pensando en health, readiness, logging y monitoreo, porque un sistema que no puede observarse tampoco puede recuperarse rápido cuando un cambio falla.

###### 10. Automatizar lo repetible, pero sobre un proceso primero entendido

Automatizar un proceso de entrega que antes fue comprendido, simplificado y modelado. Como principio de diseño organizacional y técnico, esto implica evitar pasos manuales opacos, dependencias tácitas y conocimiento tribal en el proceso de build, test y deploy. Un sistema bien diseñado para CI/CD presupone repetibilidad.

![](image1.jpg)

---

## ¿Cómo trabajar para integrar y entregar con frecuencia?

En esta sesión se abordan las condiciones que hacen posible la integración continua como práctica sostenida. Reducir el tamaño de lote, limitar el trabajo en curso y trabajar cerca de trunk mejora el flujo de entrega, pero esas prácticas sólo son viables cuando el diseño del software acompaña. Si el sistema presenta alto acoplamiento, responsabilidades confusas o complejidad innecesaria, incluso cambios pequeños se vuelven costosos de probar, difíciles de integrar y riesgosos de desplegar.

Desde esta perspectiva, la integración continua no depende únicamente de herramientas o de la existencia de un pipeline. También exige determinadas propiedades del software: cambios localizados, dependencias controladas, validación rápida y un costo de cambio razonable.

En particular, se pone en relación la integración continua con criterios de diseño sólidos. La importancia de estos enfoques, en este contexto, no radica en su formulación teórica, sino en el efecto práctico que producen sobre la capacidad de cambiar, probar e integrar con bajo riesgo. Un diseño con responsabilidades bien asignadas, bajo acoplamiento, cohesión adecuada y complejidad controlada favorece la construcción de pruebas automatizadas confiables, reduce el impacto colateral de los cambios y facilita una estrategia de ramas cortas e integración temprana.

Por el contrario, cuando el software concentra demasiadas responsabilidades, depende fuertemente de detalles de infraestructura o incorpora abstracciones innecesarias, el trabajo de integración pierde fluidez. Los cambios requieren más coordinación, las pruebas se vuelven más difíciles de construir o mantener, y el feedback automático deja de ser rápido y confiable. En estas condiciones, la integración continua tiende a degradarse en una práctica nominal: existe pipeline, pero no existe verdadera capacidad de integrar con frecuencia y seguridad.

La clase busca mostrar, entonces, que el flujo de trabajo y el diseño del software no son dimensiones separadas. La reducción del tamaño de lote, la limitación del *trabajo en progreso* y el trabajo cercano a trunk necesitan de un diseño que mantenga bajo el costo de cambio. En este marco, los principios de diseño de software funcionan como referencia para evaluar si el sistema está siendo construido de una manera compatible con una estrategia real de integración continua.

#### Para ponernos en sintonía cuando hablamos de un correcto diseño:

###### Principios de la POO

- Abstracción
- Encapsulamiento
- Herencia
- Polimorfismo.

[Fuente](https://github.com/emigallo-edu/oop/blob/main/Presentaciones/Content.md)

###### Algunos principios de diseño
- abierto-cerrado de Bertrand Meyer (la 'O' de SOLID)
- sustitución de Liskov (la 'L' de SOLID)
- bajo acoplamiento
- alta cohesión (la 'S' de SOLID)
- diseño suficiente
- sencillez

###### Cohesión de paquetes
*Robert C. Martin - Clean Architecture*

**REP — Reuse/Release Equivalence Principle**
El principio de equivalencia entre reutilización y liberación.
La idea es que la unidad que reutilizás debería coincidir con la unidad que liberás/versionás.
Si un conjunto de clases se reutiliza junto, debería formar un mismo paquete/componente publicable como una unidad coherente.

> la unidad que reutilizás debería coincidir con la unidad que liberás/versionás.

**CCP — Common Closure Principle**
El principio de cierre común.
Las clases que cambian por las mismas razones deberían agruparse en el mismo paquete.
Si varias clases suelen modificarse juntas ante un mismo tipo de cambio, conviene que estén cerradas dentro del mismo componente.
Eso reduce el impacto de los cambios y mejora mantenibilidad.
Ejemplo: las clases de un sistema de facturación.
>las clases que cambian por la misma razón deberían agruparse juntas.

**CRP — Common Reuse Principle**
El principio de reutilización común.
Las clases que se reutilizan juntas deberían estar juntas.
Y, en sentido inverso, no deberías depender de clases que no necesitás.
Si un paquete obliga a importar muchas clases que no usás, está mal diseñado.
Esto busca evitar dependencias innecesarias.
> las clases que cambian por la misma razón deberían agruparse juntas.

#### Propiedades deseables del diseño

Entre las propiedades de diseño que favorecen un esquema de integración continua se destacan la claridad en la asignación de responsabilidades, el bajo acoplamiento entre componentes, la alta cohesión dentro de cada unidad, la simplicidad estructural, la explicitud de las dependencias y la ausencia de complejidad anticipada que todavía no responde a una necesidad real. Estas cualidades no garantizan por sí mismas una buena integración continua, pero sí reducen significativamente el costo de cambio y aumentan la capacidad del equipo para verificar e integrar con rapidez.

En este sentido, los principios de diseño no se consideran un fin en sí mismo, sino un medio para producir software más fácil de modificar, más fácil de probar y más seguro de integrar. La integración continua, entendida de forma rigurosa, requiere precisamente esas condiciones.

#### Estrategias de branch

Las estrategias de branch no deben analizarse únicamente como una convención de uso de Git, sino como una consecuencia de la forma en que el software está diseñado y del modo en que el equipo organiza su trabajo. En un esquema de CI/CD, las estrategias que mejor funcionan son aquellas que favorecen integración temprana, ramas de vida corta y cambios pequeños. Sin embargo, esto sólo es viable cuando el sistema permite que distintas personas trabajen en paralelo con un nivel razonable de independencia.

Cuando el software presenta alto acoplamiento, responsabilidades poco claras o una concentración excesiva de lógica en unas pocas clases, el trabajo concurrente se vuelve más difícil. Dos desarrolladores que avanzan sobre tareas conceptualmente distintas terminan modificando los mismos componentes, compitiendo por las mismas clases y generando no sólo conflictos de merge, sino también conflictos semánticos: cambios que técnicamente se integran, pero que alteran o invalidan decisiones tomadas por otra persona. En estas condiciones, las ramas cortas pierden efectividad y la integración frecuente se vuelve costosa.

Por el contrario, un diseño con responsabilidades mejor distribuidas, límites claros entre componentes y dependencias más controladas permite que distintas tareas evolucionen con menor interferencia mutua. Esto hace posible que varios desarrolladores trabajen en paralelo sobre cambios acotados, integren con mayor frecuencia y reduzcan el riesgo asociado a la convergencia tardía. Desde este punto de vista, estrategias como trunk-based development no dependen solamente de disciplina operativa, sino también de un diseño que reduzca el solapamiento innecesario entre cambios.

Así, la discusión sobre estrategias de branch no se limita a elegir entre trunk-based development, ramas por tarea o variantes más cercanas a GitFlow. La cuestión de fondo es si el sistema admite integración frecuente sin que cada cambio arrastre un volumen excesivo de coordinación. Cuando el diseño favorece bajo acoplamiento, cohesión adecuada y cambios localizados, las estrategias de ramas cortas resultan viables y efectivas. Cuando esas condiciones no están presentes, las ramas tienden a alargarse y a funcionar como mecanismo de contención frente a un diseño que dificulta integrar.

En este marco, la estrategia de branch más compatible con CI/CD es aquella que minimiza el tiempo entre desarrollo e integración. Pero para que eso sea sostenible, el software debe ofrecer condiciones que permitan trabajo concurrente, pruebas rápidas y cambios acotados. De lo contrario, la estrategia elegida en el repositorio no resuelve el problema de fondo, sino que apenas compensa, de manera parcial, limitaciones del diseño.

---
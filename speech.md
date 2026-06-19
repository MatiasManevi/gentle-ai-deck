# Apuntes para la presentación

---

### Slide 0
- Gentle AI **NO** es un instalador de agents. Instalar un agente es fácil.
- Es un **configurador de ecosistema**: toma el agente que uses y lo potencias con:
  - Memoria persistente (Engram)
  - Flujos SDD (Spec-Driven Development)
  - Skills curadas
  - Servidores MCP
  - AI provider switcher
  - Persona docente con permisos security-first
  - Asignación de modelo por fase (cada paso de SDD corre en un modelo diferente)

### Slide 1
- Pasamos de "ask and pray" a una línea de ensamblaje de expertos.
- Spec-Driven Development: aplicar ingeniería de software al flujo de IA.
- Cada fase tiene un entregable concreto: spec → design → tasks → code → verify.
- No más prompts mágicos. Es un pipeline estructurado con entradas y salidas definidas.

### Slide 2
- 7 roles especializados en el flujo SDD.
- **Explorer**: lee y analiza el codebase. **Proposer**: define qué y por qué.
- **Spec Writer**: requisitos + escenarios. **Designer**: arquitectura + decisiones.
- **Task Planner**: divide en tareas. **Implementer**: escribe código siguiendo el diseño.
- **Verifier**: valida contra specs. Cada rol es un sub-agente con su propia skill y contexto fresco.

### Slide 3
- Ejemplo real: `/sdd:new create-users-endpoint`.
- Explorer detecta stack (Next.js + Prisma) → Proposer define `POST /api/users` con Zod.
- Spec + Design en paralelo → Tasks divide en 4 tareas (Model, Route, Validation, Test).
- Implementer genera código → Verifier valida contra specs.
- El orquestador nunca escribe código, solo orquesta. Cada sub-agente recibe contexto limpio.

### Slide 4
- Trabajás 2 horas definiendo arquitectura con el agente. El sistema compacta.
- El agente ya no recuerda que decidiste Clean Architecture con DI. Genera código genérico.
- El problema no es solo "olvidar" — es perder decisiones específicas de arquitectura, patrones y convenciones que ya habías resuelto.
- La compactación forza amnesia: el summary reemplaza decisiones concretas por ruido general.

### Slide 5
- Engram no guarda todo (eso es ruido), guarda **señales**: decisiones, errores resueltos, patrones.
- Observaciones estructuradas con What / Why / Where / Learned.
- El agente decide qué es señal y qué es ruido en cada save.
- Un equipo de 3 devs: cada uno pierde sus propias decisiones, y nunca se enteran que las repiten o se contradicen entre sí. Engram rompe ese ciclo.

### Slide 6
- Sesión 1: diseñás → `mem_save`. Sesión 2: implementás → `mem_search` recupera la decisión → código consistente.
- Sin Engram, la sesión 2 ignora la sesión 1. Con Engram hay continuidad real.
- El loop básico: guardar → buscar → reutilizar. No importa cuántas compactaciones ocurran entre medio.

### Slide 7
- Dos formas de sincronizar, ambas funcionan para solo o equipo.
- **Git sync**: cero infra, async, commit-based, usás tu repo existente.
- **Engram Cloud**: servidor self-hosted, dashboard web (templ + htmx), autosync en tiempo real, multi-user con roles.
- Elegís según necesidad: simplicidad o visibilidad.

---

### Slide 8
- Un solo `AGENTS.md` escala linealmente con la complejidad del proyecto → más tokens, más alucinaciones.
- Las skills surgen para alivianar ese peso: descomponemos el monolito en módulos atómicos.
- Ahora el agente solo conoce las rutas a las skills, no el contenido completo.
- Cada skill se carga on-demand mediante triggers → lazy loading puro.
- *pensar*: ¿Qué pasaría si tuvieras skills con las convenciones específicas de tu empresa? ¿Cómo cambiaría el onboarding de un dev nuevo?

### Slide 9
- Aun con skills modulares, un solo agente haciendo todo puede llenar el 80% de su contexto antes de escribir código.
- Si compacta antes de implementar, alucina: "con el contexto que tengo, te puedo responder esto".
- La solución: el **orquestador** nunca trabaja — solo coordina sub-agentes.
- Cada sub-agente nace con contexto liviano, instrucciones específicas, y carga solo la skill que necesita.

### Slide 10
- Gentle AI incluye **21 skills** en tres categorías.
- **SDD Workflow** (10 skills): init → explore → propose → spec → design → tasks → apply → verify → archive → onboard.
- **Code Quality** (5): judgment-day, go-testing, branch-pr, chained-pr, work-unit-commits.
- **Knowledge** (5): cognitive-doc-design, skill-creator, skill-improver, comment-writer, issue-creation.
- Cada skill es un módulo autónomo con sus propios triggers, convenciones e instrucciones.
- Se combinan como LEGO: usás lo que necesitás, ignorás el resto. Crear una skill custom es solo un archivo markdown con frontmatter.

---

### Cierre
- Gentle AI es un potente **configurador de ecosistemas**.
- Nos permite ir más allá del chat estructurando un flujo de trabajo de IA robusto.
- Velocidad por automatización. Consistencia por skills. Calidad por verificación contra specs.
- Eficiencia en el uso de memoria y ventana de contexto.
- Diseñado para que todo un equipo se beneficie del mismo flujo SDD y las mismas skills definidas por las convenciones del proyecto.
- Todo open source, todo combinable.

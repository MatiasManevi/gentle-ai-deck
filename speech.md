# What is an LLM: prediction, not thinking
- Completan patrones estadisticos
- Calidad de resultado depende directamente de la calidad de contexto.

# What an LLM is NOT
- No es una base de datos, no aprende de tus conversaciones, no entiende como un humano, no es determinista
- Si no sabés esto, vas a tener expectativas incorrectas y frustración constante

# Chat vs Agent
- Todos hemos experimentado en un comienzo con chatgpt
- Pero un agente actua, influye en el environment que le das
- Un agente es mas un pair programming. Un agente es un chatbot pero con herramientas para ACTUAR

# Fixed size window
- El contexto es todo lo que el modelo ve. Tamano fijo fisico medido en tokens.

# Compaction forced amnesia
- Habran notado que cuanto mas interactuamos con el mismo agente, el resultado suele desviarse cada vez mas de nuestro intencion inicial. El resultado se desdibuja porque aumenta el ruido. Porque aumenta el ruido? por la compactacion
- Porque se compacta?:
- Se pierden decisiones iniciales tomadas
- Ese summary forma parte de la siguiente prompt del usuario

# Start with Agends.md
- El agente lee todo acerca de la estructura, convenciones, lineamientos y practicas para trabjar en el proyecto.

# Agents.md grow
- Este archivo escala facilmente con la complejidad del pryecto, se vuelve dificil de mantener ademas de que
ocupara demasiados tokens en la ventana de contexto. Mas contexto => mas probabilidad de alucionaciones

# Skills
- Las skills surgen como medida para alivianar el peso del Agents.
- Ahora un agent particionado unicamente conoce las rutas a las skills donde se describen las convenciones, arquitectura, practicas, etc.
- No es lo mismo tener varios agent.md refactorizados? No, porque lo que tienen las skills son triggers.
- Los triggers nos permiten cargar una skill a contexto on-demand, economizando la ventana de contexto (lazy-loading)

pensar: ¿Qué pasaría si tuvieras skills con las convenciones específicas de tu empresa? ¿Cómo cambiaría el onboarding de un dev nuevo que usa agentes?

# God agent
- Aun habiendo partido el agents.md en skills y donde cada skill provee contexto atomico y particular, un unico agente haciendose cargo de todas las tareas aun teniendo una ventana de contexto grande puede llegar a ocuparla al 80% antes de siquiera escribir codigo.
- Con esto corremos el riesgo de compactar mucho contenido antes de implementar -> lo cual lleva la IA a alucinar "con el contexto que tengo, te puedo responder esto". En general se debe a ruido en la ventana de contexto y a las compactaciones del mismo.

# Divide & Conquer
- El orquestador no trabaja, solamente coordina sub agentes
- Cada subagente tiene su propio ctx, hace lo que debe hacer, y retorna los rtdos al orquestrador

# Fresh context
- Con esta arquitectura, cada subagente nace con un ctx muy liviano. Instrucciones especificas y cero ruido.
- Cada agente carga el skill que necesita para su tarea.

# SDD
- Spec-Driven Development: aplicar ingeniería de software al flujo de IA
- En vez de "ask and pray", una línea de ensamblaje de expertos
- Cada fase tiene un entregable concreto: spec → design → tasks → code → verify

# Roles
- 7 roles especializados en el flujo SDD
- Explorer (lee y analiza), Proposer (define qué y por qué), Spec Writer (requisitos + escenarios), Designer (arquitectura + decisiones), Task Planner (divide en tareas), Implementer (escribe código), Verifier (valida contra specs)
- Cada rol es un sub-agente con su propia skill y contexto

# Example
- /sdd:new create-users-endpoint
- Explorer detecta stack (Next.js + Prisma) → Proposer define POST /api/users con Zod → Spec + Design en paralelo → Tasks divide en 4 tareas (Model, Route, Validation, Test) → Implementer genera código → Verifier valida contra specs
- El orquestador nunca escribe código, solo orquesta

# Compaction kills decisions
- Trabajás 2 horas definiendo arquitectura con el agente. El sistema compacta. El agente ya no recuerda que decidiste Clean Architecture con DI. Genera código genérico.
- El problema no es solo "olvidar" — es perder decisiones específicas de arquitectura, patrones y convenciones que ya habías resuelto. El problema es no trabajar con consistencia
- En un equipo de 3 devs cada uno pierde sus propias decisiones, y nunca se enteran que las repiten o se contradicen entre sí

# Save signals, not everything
- Engram no guarda todo (eso es ruido), guarda señales: decisiones, errores resueltos, patrones
- Observaciones estructuradas con What / Why / Where / Learned
- El agente decide qué es señal y qué es ruido

# The Engram Loop
- Sesión 1: diseño → mem_save. Sesión 2: implementación → mem_search recupera la decisión → código consistente
- Sin Engram, la sesión 2 ignora la sesión 1. Con Engram hay continuidad real
- El loop básico: guardar → buscar → reutilizar

# Git or Cloud
- Dos formas de sincronizar, ambas funcionan para solo o equipo
- Git sync: cero infra, async, commit-based, usás tu repo existente
- Engram Cloud: servidor self-hosted, dashboard web (templ + htmx), autosync en tiempo real, multi-user con roles
- Elegís según necesidad: simplicidad o visibilidad

# Gentle-ai Ecosystem
- Engram da persistencia y continuidad, SDD da estructura, Skills da consistencia
- Juntos resuelven los tres problemas del LLM: amnesia, degradación y genericidad
- No es una herramienta mágica — es un ecosistema que se configura

# The Goodies
- Velocidad por automatización. Consistencia por skills. Calidad por verificación contra specs
- Eficiencia en el uso de memoria y ventana de contexto
- Todo open source, todo combinable

# Closing
Creo que gentle ai se destaca como un potente configurador de ecosistemas que nos permite primero que nada
1. ir más allá de simples interacciones de chat y adoptar un uso mas directo de la IA
2. Nos permite estructurar, configurar y especializar un flujo de trabajo de IA robusto y listo para que todo un equipo de desarrollo se beneficie en conjunto del mismo flujo de SDD y skills definidas por las convenciones del proyecto en particular
3. Creo que es una herramienta que vale la pena probar, en conjunto, significativamente la productividad y la fiabilidad de los agentes de IA existentes mientras.

Si bien Gentle-AI ofrece una experiencia única y optimizada, forma parte de un panorama creciente de marcos de orquestación sofisticados, cada uno adaptado a diferentes necesidades arquitectónicas y preferencias de los desarrolladores.

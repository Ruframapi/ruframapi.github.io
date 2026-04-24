# Plan de Presentación
## "Can LLM-Augmented Autonomous Agents Cooperate?"
### Evaluación mediante Melting Pot

---

## Estructura General (12 slides + portada)

---

### Slide 1 — Portada
**Contenido:**
- Título: *Can LLM-Augmented Autonomous Agents Cooperate? An Evaluation of Their Cooperative Capabilities Through Melting Pot*
- Autores: Mosquera, Pinzón, Fonseca, Ríos, Quijano, Giraldo, Manrique
- Universidad de los Andes · Google Research Scholar Program
- Logo institucional (si disponible)

**Qué decir:**
> "Buenas [tardes/días]. Hoy les voy a presentar un trabajo que surge de una pregunta fundamental en IA moderna: ¿pueden los agentes autónomos potenciados por grandes modelos de lenguaje cooperar entre sí? Esto es más difícil de lo que parece, y para responderlo utilizamos Melting Pot, una plataforma de DeepMind diseñada específicamente para evaluar cooperación en sistemas multi-agente."

---

### Slide 2 — Motivación y Problema
**Contenido:**
- La cooperación es esencial en sistemas multi-agente (vehículos autónomos, atención al cliente, etc.)
- LLMs han avanzado enormemente como base de agentes autónomos (LAAs)
- **Pregunta central:** ¿Las LAAs pueden cooperar en entornos sociales complejos?
- Citando Dafoe et al.: la cooperación requiere *Comprensión, Comunicación, Compromiso e Instituciones*

**Qué decir:**
> "El contexto: la IA está cada vez más presente en entornos donde múltiples agentes deben coexistir. Sin embargo, mientras hay mucho trabajo en inteligencia individual, la inteligencia *social* —la capacidad de colaborar— ha sido relativamente poco estudiada. Los LLMs parecen prometedores como base para agentes más sociales. Pero, ¿realmente cooperan? Esa es la pregunta que este paper intenta responder."

---

### Slide 3 — Trabajo Relacionado
**Contenido:**
- **Toolformer** (Schick et al.): LLMs que invocan APIs — pero sin razonamiento contextual
- **ReAct** (Yao et al.): combina razonamiento + acción mediante prompts
- **Reflexion** (Shinn et al.): auto-reflexión sobre intentos fallidos
- **Generative Agents** (Park et al.): arquitectura cognitiva completa con memoria, planificación y reflexión → base de este trabajo
- **Voyager** (Wang et al.): agente autónomo en Minecraft
- **MetaGPT** (Hong et al.): roles y tareas estructuradas entre agentes

**Qué decir:**
> "Para contextualizar, hubo una evolución de arquitecturas de agentes. Se pasó de simples invocaciones de herramientas, a razonamiento más elaborado, y finalmente a arquitecturas cognitivas completas. La más relevante para nosotros es la de Generative Agents de Park et al., que incluye memoria de corto y largo plazo, planificación y reflexión. Esta sirvió de base para nuestros agentes."

---

### Slide 4 — Plataforma: Melting Pot
**Contenido:**
- Herramienta de DeepMind para evaluar IA multi-agente
- Combina un *substrate* (entorno físico 2D) con una *background population* (bots con políticas fijas)
- Diseñado para situaciones de dilemas sociales y alta interdependencia
- Los 3 escenarios usados: **Commons Harvest Open**, **Externality Mushrooms**, **Coins**
- Imagen: `images/cooperacion/environment_commons_harvest.png`, etc.

**Qué decir:**
> "Melting Pot es la plataforma que usamos para evaluar a nuestros agentes. Es un entorno diseñado por DeepMind específicamente para poner a prueba la cooperación: los agentes conviven con bots entrenados con políticas que a veces son disruptivas. Los tres escenarios que seleccionamos representan distintos tipos de dilemas sociales: recursos compartidos, externalidades y competencia directa."

---

### Slide 5 — Los Tres Escenarios
**Contenido:**
- **Commons Harvest Open:** manzanas en un mundo 2D, reaparecen si hay manzanas vecinas. Si se agotan los parches verdes → no hay regeneración. Dilema: cosechar ahora vs. sostenibilidad colectiva.
- **Externality Mushrooms:** hongos con distintos efectos: rojo (solo el recolector), verde (todos), azul (todos menos el recolector), naranja (penalización). Bots prefieren hongos rojos.
- **Coins:** 2 agentes, monedas de colores. Cada moneda = +1 punto. Si el otro recoge una moneda de tu color: -2 puntos para ti. Bot usa política de reciprocidad.
- Imagen: captura de pantalla de los 3 ambientes

**Qué decir:**
> "Vamos a ver cada escenario brevemente. En Commons Harvest, el reto es la sobrexplotación: si los agentes cosechan sin control, los árboles desaparecen para siempre. En Mushrooms, el agente debe aprender a priorizar hongos verdes que benefician a todos, en lugar de los rojos que solo le dan a él. Y en Coins, hay un dilema directo: ¿recoges todas las monedas o respetas las del otro para evitar represalias?"

---

### Slide 6 — Arquitectura LAA: Generative Agents
**Contenido:**
- Basada en Park et al. (2023)
- **Tres memorias:**
  - Corto plazo: estado actual del mundo
  - Largo plazo: observaciones e insights (ChromaDB + embeddings)
  - Espacial: posición y orientación en el grid
- **Cuatro módulos cognitivos:**
  1. **Percepción:** filtra y prioriza observaciones por cercanía; decide si replantear el plan
  2. **Planificación:** genera plan de alto nivel con contexto, reflexiones y observaciones
  3. **Reflexión:** genera insights de alto nivel sobre experiencias pasadas; almacena en memoria larga
  4. **Acción:** selecciona acción con razonamiento SWOT (Oportunidades, Amenazas, Opciones, Consecuencias)
- Imagen: `images/cooperacion/Figure_Coop_AI.pdf`

**Qué decir:**
> "Aquí está el corazón del trabajo: la arquitectura de nuestros agentes. Tiene tres niveles de memoria y cuatro módulos cognitivos que se ejecutan secuencialmente. Lo más interesante es que el módulo de acción no simplemente elige una acción: razona explícitamente sobre oportunidades, amenazas, opciones y consecuencias —algo similar al análisis FODA— antes de decidir. Esto le da al agente una capa de razonamiento estratégico."

---

### Slide 7 — Adaptación del Entorno a LLMs
**Contenido:**
- Melting Pot es visual (grids 2D con símbolos) → difícil de interpretar por LLMs
- Solución: **generador de observaciones en lenguaje natural** con coordenadas [x, y]
- Ejemplo: *"Observed an apple at position [3, 7]. This apple belongs to tree_2"*
- Acciones de alto nivel: `go to position (x,y)`, `explore`, `stay put`, `immobilize player`
- Tabla de descripciones de objetos (Commons Harvest)

**Qué decir:**
> "Un desafío clave fue cómo comunicarle el estado del mundo a un LLM. Una matriz de símbolos como la que usa Melting Pot no es interpretable fácilmente por los modelos. La solución fue construir un generador que traduce cada objeto del grid a una descripción en lenguaje natural con coordenadas. Así el agente 've' el mundo como texto, y ejecuta acciones de alto nivel como 'ir a posición X,Y' en lugar de 'mover arriba'."

---

### Slide 8 — Diseño Experimental
**Contenido:**
- **Baselines:**
  - RL de Melting Pot (entrenados por 10⁹ pasos)
  - CoT (Chain-of-Thought): observaciones directas → LLM → acción, sin memoria ni reflexión
- **Modelos LLM:** GPT-4o y GPT-4o mini (Set 1); GPT-4 y GPT-3.5 (Set 2)
- **Métrica principal:** Focal Per Capita Average Reward (solo LAAs, excluyendo bots)
- **10 repeticiones** por experimento
- **Set 1:** Comparación vs. RL y vs. CoT en los 3 escenarios
- **Set 2:** Impacto de personalidad (cooperativo, egoísta, sin personalidad) en Commons Harvest

**Qué decir:**
> "Para evaluar nuestros agentes usamos dos líneas de comparación: primero, los algoritmos de RL del paper original de Melting Pot, que fueron entrenados por miles de millones de pasos. Segundo, una versión simplificada de agente LAA que solo usa Chain-of-Thought. La métrica es la recompensa promedio per cápita de los agentes focales. Todo se repitió 10 veces para garantizar significancia estadística."

---

### Slide 9 — Resultados Principales (Set 1)
**Contenido:**
- Gráfico comparativo de Focal Per Capita Reward (Figura principal del paper)
- **Generative Agents supera a CoT en los 3 escenarios**
- **Generative Agents supera al baseline RL en 2 de 3 escenarios:** Coins y Externality Mushrooms ✅; Commons Harvest ❌
- GPT-4o y GPT-4o mini muestran tendencias similares
- Imagen: `images/cooperacion/all_focalRewPerCapita_v2.png`

**Qué decir:**
> "Este es el resultado más importante. Generative Agents supera consistentemente al agente CoT en los tres escenarios. Y frente al baseline de RL —que recuérdense fue entrenado por billones de pasos— los Generative Agents ganan en Coins y Mushrooms, y pierden solo en Commons Harvest. Lo llamativo es que nuestros agentes nunca fueron 'entrenados': solo tenían información general del entorno. Eso habla del poder del 'sentido común' que ya tienen los LLMs."

---

### Slide 10 — Análisis por Escenario
**Contenido (3 columnas o tabs):**

**Mushrooms:**
- Gen. Agents eligen más hongos verdes (cooperativos) que CoT
- Exploran activamente cuando no hay hongos buenos visibles
- Raramente consumen hongos azules o naranjas (perjudiciales)
- p-value < 0.1 vs. RL baseline ✅

**Coins:**
- Gen. Agents activan menos la política de reciprocidad del bot
- Toman menos monedas del color incorrecto
- GPT-4o mini sorpresivamente mejor que GPT-4o en algunos indicadores

**Commons Harvest:**
- Gen. Agents son más sostenibles (evitan árboles con pocas manzanas)
- Pero fallan en el caso crítico: consumen la **última manzana** más frecuentemente que CoT
- RL gana aquí por haber visto este caso millones de veces en entrenamiento

**Qué decir:**
> "Yendo al detalle de cada escenario encontramos patrones interesantes. En Mushrooms, los agentes aprendieron a priorizar el bien colectivo. En Coins, mejoraron la cooperación estratégica evitando provocar al bot. Pero en Commons Harvest hay un punto ciego: aunque los agentes fueron más sostenibles en general, fallaron en el momento más crítico — cuando solo queda una manzana. El RL, entrenado por 10⁹ pasos, sí aprendió ese caso límite."

---

### Slide 11 — Impacto de Personalidad y del Conocimiento Social
**Contenido:**
- **Set 2 — Personalidad:** Agentes cooperativos → peor rendimiento (no atacan aunque deberían)
- LLMs equiparan "cooperar" con "no atacar", incluso cuando atacar es la estrategia óptima
- Agentes egoístas ≈ agentes sin personalidad → los LLMs tienden a cooperar de base
- **Experimento: Pedro el egoísta:** agentes informados de que "Pedro" es egoísta → 86% de ataques dirigidos a Pedro
- Imagen: `images/cooperacion/set_personality_rewards_and_attacks_v2.png` y `images/cooperacion/set2_attacks_graph___pedro_is_selfish_v3.png`

**Qué decir:**
> "Dos hallazgos curiosos del segundo set. Primero: cuando instruimos a los agentes a ser cooperativos, su rendimiento fue el peor. ¿Por qué? Porque los LLMs interpretan 'cooperar' como 'no atacar', y en Commons Harvest atacar a los bots destructivos es la única forma de proteger los recursos. Segundo: cuando informamos a los agentes que 'Pedro' es egoísta, el 86% de los ataques fueron dirigidos específicamente a él. Los agentes usaron esa información social para coordinar una respuesta colectiva — un comportamiento emergente fascinante."

---

### Slide 12 — Capacidades Cooperativas y Limitaciones
**Contenido:**
- Marco de Dafoe et al. — 4 capacidades cooperativas:
  1. **Comprensión:** anticipar consecuencias y entender otros agentes
  2. **Comunicación:** intercambio intencional de información
  3. **Compromiso:** mecanismos de promesas y amenazas creíbles
  4. **Instituciones:** estructuras sociales que simplifican la interacción
- LAAs actuales muestran avances en (1), pero carecen de (2), (3) y (4)
- Limitaciones clave: no distinguen bots de agentes LLM, no priorizan bienestar colectivo consistentemente, costo computacional alto

**Qué decir:**
> "Aquí viene la reflexión más profunda del paper. ¿Qué se necesita para cooperar de verdad? Dafoe et al. identifican cuatro capacidades esenciales. Nuestros agentes muestran cierta comprensión del mundo, pero les falta comunicación directa entre agentes, mecanismos de compromiso creíbles e instituciones sociales. En otras palabras: son agentes que *quieren* cooperar, pero no siempre *saben cómo* hacerlo en entornos complejos."

---

### Slide 13 — Conclusiones y Trabajo Futuro
**Contenido:**
- ✅ Arquitecturas LAA avanzadas mejoran significativamente la cooperación frente a baselines simples
- ✅ Generative Agents superan a RL en 2/3 escenarios, sin entrenamiento previo
- ✅ El conocimiento social (saber quién es egoísta) puede guiar comportamientos cooperativos emergentes
- ⚠️ Gap en capacidades cooperativas: comprensión, comunicación, compromiso e instituciones
- **Futuro:** arquitecturas con comunicación explícita entre agentes, mecanismos de compromiso, benchmarks más ricos en Melting Pot
- Repo: [https://github.com/Cooperative-IA/CooperativeGPT](https://github.com/Cooperative-IA/CooperativeGPT)

**Qué decir:**
> "Para cerrar: demostramos que las arquitecturas LAA avanzadas son prometedoras para la cooperación, y que el 'sentido común' de los LLMs puede compensar la falta de entrenamiento en muchos casos. Pero también identificamos un gap importante: las capacidades cooperativas de orden superior — comunicar, comprometerse, construir instituciones — aún no están bien representadas en las arquitecturas actuales. Ese es el camino por explorar. El código está disponible en GitHub para quien quiera explorar o construir sobre este trabajo. Gracias."

---

## Notas de Producción
- **Total de slides:** 13 (portada + 12 de contenido)
- **Duración estimada:** 20–25 minutos
- **Imágenes a incluir:**
  - `images/cooperacion/environment_commons_harvest.png`
  - `images/cooperacion/environment_mushrooms.png`
  - `images/cooperacion/environment_coins.png`
  - `images/cooperacion/Figure_Coop_AI.pdf` (convertir a PNG para web)
  - `images/cooperacion/all_focalRewPerCapita_v2.png`
  - `images/cooperacion/set1_mushrooms_indicators.png`
  - `images/cooperacion/set2_coins1_indicators_comparison_v3.png`
  - `images/cooperacion/set2_commons_harvest_0_indicators_comparison.jpg`
  - `images/cooperacion/set_personality_rewards_and_attacks_v2.png`
  - `images/cooperacion/set2_attacks_graph___pedro_is_selfish_v3.png`

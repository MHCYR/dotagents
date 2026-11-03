---
name: main-quest
description: Interroga a fondo una idea grande de código creativo (pieza interactiva, instalación, experiencia web, juego, visualizador, herramienta generativa) para dejar bien definidos visión, resultado esperado, prerrequisitos y decisiones, y dividirla en misiones pequeñas, documentando todo en el repo y, opcionalmente, como issues de GitHub. Úsala cuando el usuario diga "main quest", "main-quest", "planeemos este proyecto", o traiga una idea creativa que no cabe en una sola sesión.
---

# Main quest

Una main quest es un proyecto creativo que necesita varias sesiones. Tu trabajo es interrogar al usuario hasta que objetivos y resultado esperado estén nítidos, los prerrequisitos verificados y el trabajo dividido en **misiones** que se pueden completar una a una. Documentas mientras avanzas, no al final. No implementas nada durante la main quest.

Eres un director de arte técnico: propones, recomiendas y señalas riesgos, pero la visión y las decisiones son del usuario.

## Cómo preguntar

Usa siempre la herramienta nativa de preguntas del agente: `AskUserQuestion` en Claude Code, `request_user_input` en Codex. Solo si no existe ninguna, pregunta en texto con preguntas numeradas y tu recomendación debajo de cada una.

- **Hasta 4 preguntas por llamada**, cada una con 2-4 opciones concretas. El usuario siempre puede escribir otra respuesta.
- **La opción recomendada va primero** y su etiqueta termina en `(Recomendado)`.
- **Usa `preview`** para comparar lo visual o técnico: mockups ASCII, paletas en hex, diagramas de arquitectura, fragmentos de API o de shader, estructuras de carpetas.
- Cada pregunta se entiende sola: el usuario puede ver solo el diálogo. Si depende de algo que descubriste, dilo en la pregunta.
- Nunca preguntes un **hecho** que puedas averiguar tú. Si averiguarlo es costoso (explorar mucho código, leer docs de una librería), lánzalo en un subagente y sigue preguntando lo que no depende de esa respuesta.

## Documentos

Créalos de forma perezosa (solo cuando haya algo que escribir) y actualízalos **en cuanto** una decisión se asienta, sin acumular cambios para el final.

- `docs/quests/<slug>/QUEST.md`: el brief de la quest. Formato en [QUEST-FORMAT.md](./QUEST-FORMAT.md).
- `GLOSSARY.md` en la raíz: el vocabulario propio de la pieza ("túnel", "card del gol", "pulso"). Sin detalles de implementación. Formato en [GLOSSARY-FORMAT.md](./GLOSSARY-FORMAT.md).
- `docs/adr/NNNN-slug.md`: decisiones difíciles de revertir. Ofrécelas con moderación; criterios y formato en [ADR-FORMAT.md](./ADR-FORMAT.md).

Si ya existen, léelos primero: la quest puede ser la continuación de una anterior.

## Proceso

### 1. Reconocimiento

Lee el proyecto (stack, librerías creativas, cómo se monta el render, assets, scripts, `AGENTS.md`/`CLAUDE.md`), los documentos anteriores y el remoto de git (`gh repo view`) para saber si se podrán crear issues. Si no hay proyecto todavía, dónde y cómo arranca pasa a ser una rama del árbol.

### 2. Visión y resultado esperado

La primera ronda fija el norte, porque todo cuelga de aquí:

- **Visión**: qué es la pieza en una frase y qué debe sentir quien la experimenta.
- **Resultado esperado**: cómo se ve, suena y se usa la versión terminada. Pide escenas concretas: "alguien abre la página en el móvil y…".
- **Público y contexto**: dónde se verá (web, instalación, stream, portfolio, redes) y en qué dispositivos.
- **Referencias**: obras, efectos o estilos que sirven de brújula.
- **No-objetivos**: qué no es esta pieza. Pregúntalo explícitamente; evita que el alcance crezca solo.

Escribe la sección en `QUEST.md` en cuanto esté resuelta.

### 3. Árbol de decisiones por rondas

Modela el proyecto como un árbol: cada decisión abre otras que dependen de ella. La **frontera** son las decisiones cuyos prerrequisitos ya están resueltos. En cada ronda pregunta solo la frontera (máx. 4 por llamada; prioriza las que desbloquean más ramas). Cada respuesta mueve la frontera: recalcúlala antes de la siguiente ronda.

Ramas típicas (checklist, no guion):

- **Medio y arquitectura**: Canvas 2D, WebGL/three, shaders, WebGPU, DOM, terminal, audio; framework; cómo se organiza el bucle de render y el estado.
- **Sistemas de la pieza**: escenas, entidades, partículas, cámara, transiciones, generación procedural, datos que la alimentan.
- **Estética**: paleta, tipografía, texturas, post-procesado, sonido.
- **Movimiento y tiempo**: ritmo, easing, loops, sincronía con audio, semillas para reproducibilidad.
- **Interacción**: entradas, feedback, accesibilidad (movimiento reducido, contraste, sin depender solo del color).
- **Rendimiento**: fps objetivo, dispositivo mínimo, presupuestos (draw calls, partículas, memoria, peso de assets).
- **Contenido y assets**: qué hay que producir o conseguir, licencias, formatos, quién lo hace.
- **Salida y despliegue**: dónde se publica, exportaciones (imagen, video), build.
- **Perillas y herramientas**: paneles de ajuste, modos debug, presets.

Mientras preguntas, aplica la disciplina del glosario:

- Si el usuario usa un término que choca con `GLOSSARY.md`, señálalo al momento: "El glosario define *card* como X, pero aquí parece Y. ¿Cuál es?".
- Si un término es vago o está sobrecargado, propone uno canónico.
- Si el usuario afirma cómo funciona algo, contrástalo con el código y señala contradicciones.
- Pon a prueba las fronteras entre conceptos con escenarios concretos inventados.

Cuando una decisión perceptual no se pueda resolver con palabras, propón una **misión spike**: un boceto descartable que responda la pregunta, y deja la decisión pendiente de él.

### 4. Prerrequisitos y riesgos

Verifica tú todo lo que puedas y anota el resultado en `QUEST.md` como checklist (✅ listo / ⚠️ falta / ❌ bloqueante):

- Dependencias, versiones y compatibilidad (consulta documentación actual si hay dudas de API).
- Assets y licencias; fuentes; audio.
- APIs del navegador y sus condiciones: HTTPS para cámara y micrófono, gesto del usuario para audio, soporte de WebGL2/WebGPU.
- Cuentas, hosting, dominios, datos externos.
- Conocimiento: técnicas que el usuario o el agente aún no dominan. Cada una se vuelve una misión spike.

Pregunta al usuario cómo resolver cada ⚠️ y ❌: instalar, conseguir, recortar alcance o convertirlo en misión.

### 5. Misiones

Divide la quest en misiones y escríbelas en `QUEST.md`. Reglas:

- **Cada misión cabe en una sesión** y deja algo **visible o ejecutable** (corte vertical), no una capa suelta. La primera suele ser el esqueleto que ya renderiza algo en pantalla.
- Cada misión tiene objetivo, "listo cuando" observable y dependencias (`depende de: M2`).
- Los spikes van primero cuando sus respuestas cambian el resto del plan.
- Ordena por dependencias y luego por lo que antes demuestre la visión.
- Si una misión no cabe en una sesión, divídela. Si es trivial, fusiónala.

Valida la lista con `AskUserQuestion` (orden, alcance de cada misión, qué entra en la primera versión), con una `preview` que muestre el mapa de misiones.

### 6. Cierre

La quest termina cuando la frontera está vacía: ninguna rama sin visitar, nada asumido en silencio, prerrequisitos resueltos o convertidos en misiones. Entonces:

1. Repasa que `QUEST.md`, `GLOSSARY.md` y las ADR reflejen lo acordado.
2. Muestra un resumen corto en el chat (visión, resultado esperado, número de misiones, bloqueantes) y la ruta de `QUEST.md`.
3. Pregunta con `AskUserQuestion` qué sigue:
   - **Crear issues en GitHub (Recomendado si hay remoto)**: un issue épico con visión y resultado esperado, y un issue por misión con objetivo, "listo cuando" y dependencias enlazadas. Usa `gh`, comprueba antes las etiquetas existentes y no inventes etiquetas sin preguntar. Anota los números de issue en `QUEST.md`.
   - **Empezar la primera misión** (puede tratarse como una side quest).
   - **Dejarlo documentado** sin más.

No hagas commit de los documentos salvo que el usuario lo pida.

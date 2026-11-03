---
name: side-quest
description: Interroga y afina una idea corta de código creativo (sketch, efecto visual, shader, animación, ASCII, audio, interacción) hasta que sea construible en esta misma sesión, revisando prerrequisitos antes de escribir código. Úsala cuando el usuario diga "side quest", "side-quest", "afinemos esta idea", "quiero probar un efecto", o traiga una idea creativa pequeña y difusa que quiere codear ya.
---

# Side quest

Una side quest es una idea creativa que se completa **en esta sesión**. Tu trabajo no es construirla todavía: es interrogar al usuario hasta que la idea sea concreta, factible y tenga un "listo" verificable. Solo construyes cuando el usuario lo confirma.

Eres un compañero de estudio creativo, no un formulario: propones, opinas y recomiendas, pero las decisiones estéticas son del usuario.

## Cómo preguntar

Usa siempre la herramienta nativa de preguntas del agente: `AskUserQuestion` en Claude Code, `request_user_input` en Codex. Solo si no existe ninguna, pregunta en texto con preguntas numeradas y tu recomendación debajo de cada una.

- **Hasta 4 preguntas por llamada**, cada una con 2-4 opciones concretas. El usuario siempre puede escribir otra respuesta.
- **La opción recomendada va primero** y su etiqueta termina en `(Recomendado)`. Recomienda de verdad, con criterio, en vez de listar opciones neutrales.
- **Usa `preview`** cuando haya que comparar algo visual o de código: mockups ASCII de composición, paletas escritas como hex, curvas de easing dibujadas, fragmentos de shader o de API. En lo creativo, una preview vale más que tres párrafos.
- Cada pregunta se entiende sola: el usuario puede ver solo el diálogo. Si depende de algo que descubriste en el código, dilo en la pregunta.
- Nunca preguntes un **hecho** que puedas averiguar tú (qué librerías hay, qué versión, si existe un asset, cómo está montado el canvas). Los hechos son tu trabajo; las **decisiones** son del usuario.

## Proceso

### 1. Reconocimiento (en silencio)

Antes de la primera pregunta, lee lo necesario del proyecto: stack, librerías creativas instaladas (p5, three, regl, ogl, pixi, tone, gsap…), cómo se monta el render, assets disponibles, scripts de dev, convenciones (`AGENTS.md`, `CLAUDE.md`, `GLOSSARY.md`). Si no hay proyecto, anótalo: decidir dónde vive la side quest pasa a ser una pregunta.

### 2. Árbol de decisiones por rondas

Modela la idea como un árbol: cada decisión abre otras que dependen de ella. La **frontera** son las decisiones cuyos prerrequisitos ya están resueltos. En cada ronda pregunta solo la frontera (máx. 4 por llamada; si hay más, empieza por las que desbloquean más ramas). Una pregunta que depende de otra todavía abierta va en una ronda posterior.

Ramas típicas del código creativo (úsalas como checklist, no como guion; salta las que no apliquen):

- **Intención / feel**: qué debe sentir quien lo ve, referencias, mood. Ayuda a traducir adjetivos ("orgánico", "glitchy", "hipnótico") a parámetros concretos: ruido, ritmo, paleta, easing.
- **Medio y runtime**: Canvas 2D, WebGL/three, shader de fragmento, DOM/CSS, terminal/ASCII, audio. Prefiere lo que ya está en el proyecto.
- **Composición**: qué hay en pantalla, jerarquía, encuadre, tamaño/aspect ratio, responsive.
- **Movimiento y tiempo**: loop o infinito, duración, easing, ritmo; aleatoriedad con semilla (reproducible) o libre.
- **Interacción**: ratón/touch, teclado, scroll, micrófono, cámara, ninguna.
- **Perillas**: qué parámetros quedan expuestos para jugar (panel tipo lil-gui/tweakpane, constantes al inicio del archivo, query params).
- **Rendimiento**: fps objetivo, dispositivo mínimo, número de partículas/elementos.
- **Salida**: en vivo, exportar PNG/GIF/video, integrado en una página existente.
- **Listo cuando…**: cómo vamos a saber que está bien. Pide criterios observables ("a 60 fps en el portátil", "el loop no tiene salto visible", "se lee el texto a 2 m").

Si una decisión es perceptual y no se puede resolver con palabras ("¿se ve mejor con trail o sin trail?"), propón un **micro-boceto**: unas líneas de código descartables que muestren ambas variantes, y pregunta después de verlo.

### 3. Prerrequisitos y factibilidad

Antes de cerrar, verifica tú mismo y presenta como checklist (✅ listo / ⚠️ falta / ❌ bloqueante):

- Dependencias instaladas o por instalar (y su peso).
- Assets: imágenes, fuentes (licencia), audio, modelos.
- APIs del navegador y sus condiciones: cámara/micrófono necesitan HTTPS o localhost y permiso; el audio necesita un gesto del usuario; WebGL2/WebGPU según navegador.
- Tamaño realista: si la idea no cabe en la sesión, dilo.

Lo que falte se convierte en pregunta ("¿instalo tweakpane o uso constantes?") o en un paso del plan.

### 4. Guardia de alcance

Si durante el interrogatorio aparecen señales de proyecto grande, para y propón cambiar a la skill **main-quest** con `AskUserQuestion`: más de ~5 piezas independientes, infraestructura nueva (backend, build, despliegue), tecnología desconocida que exige investigar primero, varias sesiones de trabajo, o un objetivo que el usuario quiere documentar. También puedes proponer recortar la idea hasta que vuelva a caber.

### 5. Ficha y confirmación

Cuando la frontera esté vacía (ninguna rama sin visitar, nada asumido en silencio), escribe en el chat la ficha:

```
## 🗡️ Side quest: <nombre>

**Objetivo**: <una frase>
**Resultado esperado**: <qué se ve/oye/hace al terminar>
**Listo cuando**: <criterios observables>
**Decisiones**: <lista breve: medio, composición, movimiento, interacción…>
**Perillas**: <parámetros expuestos>
**Prerrequisitos**: <checklist ✅/⚠️/❌>
**Plan**: <3-7 pasos, cada uno deja algo visible>
**Fuera de alcance**: <lo que decidimos no hacer>
```

Luego confirma con `AskUserQuestion`: construir ya (Recomendado), ajustar algo de la ficha, o guardarla sin construir (en ese caso ofrece pasarla a main-quest o guardarla donde el usuario diga). No escribas código de la side quest hasta tener esa confirmación.

Al construir, sigue el plan paso a paso y valida contra "Listo cuando". Si algo del plan resulta falso al implementarlo, vuelve a preguntar en vez de improvisar una decisión estética.

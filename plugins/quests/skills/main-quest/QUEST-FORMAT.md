# QUEST.md

Vive en `docs/quests/<slug>/QUEST.md`. El slug es corto y en kebab-case (`tunel-de-goles`). Se escribe sección por sección a medida que cada parte se decide; las secciones aún abiertas llevan `_Pendiente_`.

## Plantilla

```md
# <Nombre de la quest>

> <La visión en una frase.>

## Resultado esperado

<Qué se ve, suena y se puede hacer cuando la quest está completa. Escenas concretas desde quien la experimenta.>

**Público y contexto**: <dónde y en qué dispositivos se verá>
**Referencias**: <obras, efectos, estilos que sirven de brújula>

## No-objetivos

- <Lo que esta pieza deliberadamente no es o no hace.>

## Decisiones

- **<Tema>**: <decisión> — <por qué, en una línea>. <Enlace a ADR si existe.>

## Prerrequisitos

- ✅ <listo>
- ⚠️ <falta> → <cómo se resuelve / misión que lo cubre>
- ❌ <bloqueante> → <qué hace falta para desbloquearlo>

## Riesgos

- <Riesgo> → <mitigación o spike que lo responde>

## Misiones

### M1 — <nombre>
**Objetivo**: <una frase>
**Listo cuando**: <criterio observable>
**Depende de**: —
**Issue**: <#123, si se creó>

### M2 — <nombre>
...

## Preguntas abiertas

- <Lo que quedó pendiente de un spike o de información externa.>
```

## Reglas

- Sin detalles de implementación que pertenezcan al código: el brief dice **qué** y **por qué**; el **cómo** fino se decide en cada misión.
- Las decisiones van en una línea cada una. Las que cumplen los criterios de ADR enlazan a su ADR.
- "Listo cuando" siempre es observable: algo que se puede ver, medir o probar.
- Mantén "Preguntas abiertas" vacía al cerrar la quest, salvo lo que dependa de un spike.

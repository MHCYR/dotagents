# dotagents

Mis skills y plugins personales para agentes de código (Claude Code, Codex y cualquier agente compatible con [Agent Skills](https://agentskills.io)). Como unos dotfiles, pero para agentes: versionados y listos para instalar en una máquina nueva.

## Plugins

| Plugin | Skills | Para qué |
| --- | --- | --- |
| [`quests`](./plugins/quests) | `side-quest`, `main-quest`, `interview`, `quest-log` | Afinar cualquier idea (código, negocio, marketing…) con preguntas antes de actuar |

### quests

Mismo patrón que grill-me / grill-with-docs: dos atajos que tú invocas y que solo cargan piezas reutilizables.

```
/quests:side-quest ──► interview
/quests:main-quest ──► interview + quest-log
```

- **side-quest**: una idea que se resuelve en la misma sesión. Al terminar la entrevista deja una ficha con "done when" y plan, y actúa solo cuando confirmas.
- **main-quest**: una idea que no cabe en una sesión. No hace el trabajo: deja el registro de la quest.
- **interview** (pieza): el método de preguntar. Rondas sobre un árbol de decisiones, opción recomendada primero, los hechos los averigua el agente y las decisiones son tuyas, checklist de prerrequisitos.
- **quest-log** (pieza): el registro en `docs/quests/<slug>/QUEST.md` (visión, resultado esperado, no-objetivos, decisiones, prerrequisitos, riesgos, misiones), ADRs en `docs/adr/` para decisiones difíciles de revertir, e issues de GitHub opcionales (un épico y uno por misión).

Inspiradas en [`grill-me`](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me) y [`grill-with-docs`](https://github.com/mattpocock/skills/tree/main/skills/engineering/grill-with-docs) de Matt Pocock.

## Instalación

### Claude Code

```bash
claude plugin marketplace add MHCYR/dotagents
claude plugin install quests@dotagents
```

`/quests:side-quest` y `/quests:main-quest` se invocan solo a mano (`disable-model-invocation: true`). `interview` y `quest-log` también las puede activar el agente por su cuenta.

### Codex

```bash
codex plugin marketplace add MHCYR/dotagents
codex plugin add quests@dotagents
```

### Otros agentes

```bash
npx skills add MHCYR/dotagents
```

## Estructura

```
.claude-plugin/marketplace.json     # el repo es un marketplace (Claude Code y Codex lo leen)
plugins/<plugin>/
  .claude-plugin/plugin.json        # manifiesto del plugin
  skills/<skill>/
    SKILL.md                        # la skill (formato Agent Skills)
    agents/openai.yaml              # metadatos de presentación para Codex
```

## Desarrollo

```bash
claude plugin validate . --strict
claude plugin validate ./plugins/<plugin> --strict
```

Al cambiar un plugin, sube `version` en su `plugin.json`: es lo que hace que las instalaciones vean la actualización.

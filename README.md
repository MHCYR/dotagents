# dotagents

Mis skills y plugins personales para agentes de código (Claude Code, Codex y cualquier agente compatible con [Agent Skills](https://agentskills.io)). Como unos dotfiles, pero para agentes: versionados y listos para instalar en una máquina nueva.

## Plugins

| Plugin | Skills | Para qué |
| --- | --- | --- |
| [`quests`](./plugins/quests) | `side-quest`, `main-quest` | Afinar ideas de código creativo con preguntas antes de codear |

### quests

- **side-quest**: interroga una idea creativa corta (efecto, shader, animación, ASCII, interacción) hasta que sea construible en la misma sesión. Revisa prerrequisitos, deja una ficha con "listo cuando" y construye solo cuando confirmas.
- **main-quest**: para proyectos creativos que no caben en una sesión. Fija visión, resultado esperado y no-objetivos, verifica prerrequisitos, divide el trabajo en misiones y lo documenta en `docs/quests/<slug>/QUEST.md`, `GLOSSARY.md` y `docs/adr/`. Al final ofrece crear un issue épico y uno por misión en GitHub.

Inspiradas en [`grill-me`](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me) y [`grill-with-docs`](https://github.com/mattpocock/skills/tree/main/skills/engineering/grill-with-docs) de Matt Pocock.

## Instalación

### Claude Code

```bash
claude plugin marketplace add MHCYR/dotagents
claude plugin install quests@dotagents
```

Se invocan con `/quests:side-quest` y `/quests:main-quest`, o diciendo "side quest" / "main quest".

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

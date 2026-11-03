# dotagents

Repo personal de skills y plugins para agentes. Es un marketplace: `.claude-plugin/marketplace.json` lista cada plugin de `plugins/`.

## Reglas

- Cada plugin vive en `plugins/<plugin>/` con su `.claude-plugin/plugin.json`.
- Cada skill vive en `plugins/<plugin>/skills/<skill>/SKILL.md` y se lista en el array `skills` del `plugin.json`.
- Cada skill lleva `agents/openai.yaml` con `display_name` y `short_description` para Codex.
- Las skills son autocontenidas: no referencian archivos de otras skills (Codex copia cada plugin a su caché y no conserva symlinks).
- Un plugin nuevo se añade también a `marketplace.json` y a la tabla del `README.md`.
- Cualquier cambio en un plugin sube su `version` (semver).
- Antes de hacer commit: `claude plugin validate . --strict` y `claude plugin validate ./plugins/<plugin> --strict`.
- Skill text (SKILL.md, reference files, openai.yaml) is written in English. Descriptions stay one short sentence, grill-style.

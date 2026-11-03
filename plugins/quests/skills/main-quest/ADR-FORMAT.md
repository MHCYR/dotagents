# ADR

Las ADR viven en `docs/adr/` con numeración secuencial: `0001-slug.md`, `0002-slug.md`. Busca el número más alto existente y suma uno. Crea la carpeta solo cuando haga falta la primera.

## Cuándo ofrecer una

Solo si se cumplen las tres:

1. **Difícil de revertir**: cambiar de opinión después cuesta de verdad.
2. **Sorprendente sin contexto**: alguien que lea el código se preguntará "¿por qué así?".
3. **Fruto de un trade-off real**: hubo alternativas genuinas y se eligió una por razones concretas.

Si falta alguna, no hay ADR: basta con la línea en "Decisiones" de `QUEST.md`.

En código creativo suelen calificar: elegir motor de render (three vs regl vs Canvas 2D), WebGPU frente a WebGL, renderizar en un worker, una arquitectura de escenas, sacrificar fidelidad por fps en móvil, procedural frente a assets pre-renderizados, o una restricción externa (la pieza debe correr offline en una instalación).

## Plantilla

```md
# <Título corto de la decisión>

<1-3 frases: contexto, qué se decidió y por qué.>
```

Una ADR puede ser un solo párrafo. Añade secciones solo si aportan:

- **Estado** (`propuesta | aceptada | obsoleta | reemplazada por ADR-NNNN`), cuando la decisión se revisa.
- **Opciones consideradas**, cuando vale la pena recordar las descartadas.
- **Consecuencias**, cuando hay efectos no obvios.

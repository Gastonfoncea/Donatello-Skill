# Donatello

Skill de Claude Code que evalúa el taste visual de una landing page aplicando una rúbrica personal, en castellano, en primera persona, con opinión fuerte. Detecta AI slop, clichés de template y falta de criterio editorial. Devuelve una crítica estructurada con síndromes detectados, señales negativas y positivas, análisis por sección y fixes sugeridos.

No es un analizador de performance ni un auditor de accesibilidad. Es un juicio de taste — el tipo de crítica que daría un diseñador senior mirando la landing sin anestesia.

## Qué devuelve

Cada crítica sigue la misma estructura:

1. **Primera impresión** — reacción visceral a los 2 segundos.
2. **Categoría y público objetivo** — contra qué se mide la landing.
3. **Veredicto** — uno de `excelente`, `bueno`, `decente`, `mediocre`, `slop`, con justificación.
4. **Síndromes detectados** — clusters reconocibles (AI Tool slop, SaaS template slop, Framer template slop, Web3/Crypto slop, Agency/studio slop).
5. **Señales negativas** ordenadas por severidad, con ubicación concreta y cita textual cuando aplique.
6. **Señales positivas** cuando las hay — sin forzar positivos si no los hay.
7. **Análisis por sección** (hero, features, pricing, testimonios, footer).
8. **Fixes sugeridos** — uno por problema, una línea cada uno.

## Requisito duro: necesita pixels

Esta skill **no funciona con solo HTML**. El 70% de la rúbrica vive en color, tipografía, spacing, jerarquía visual y tratamiento de componentes — cosas que no se pueden evaluar desde el markup. Juzgar taste leyendo HTML es como criticar un cuadro leyendo la lista de materiales.

Para que la skill funcione necesitás una de estas dos fuentes de pixels:

1. **Un screenshot** pegado en el chat (ideal: desktop + mobile).
2. **Un MCP de browser** instalado en Claude Code. El más directo es Playwright de Microsoft:

   ```sh
   claude mcp add playwright npx '@playwright/mcp@latest'
   ```

   Con Playwright disponible, la skill navega la URL por su cuenta y toma los screenshots antes de aplicar la rúbrica.

Si solo tenés una URL y no hay browser MCP instalado, la skill va a parar y pedirte una de las dos opciones arriba. No improvisa crítica desde WebFetch.

## Instalación

La skill es un único archivo `SKILL.md`. Claude Code la carga desde `~/.claude/skills/donatello/`.

```sh
git clone git@github.com:Gastonfoncea/Donatello.git ~/.claude/skills/donatello
```

Reiniciá Claude Code y la skill queda disponible globalmente.

Si preferís mantener el repo en otro lado y simbolicarlo:

```sh
git clone git@github.com:Gastonfoncea/Donatello.git /ruta/donde/quieras
ln -s /ruta/donde/quieras ~/.claude/skills/donatello
```

## Cómo se activa

La skill se dispara cuando le pedís a Claude una crítica de landing con frases como:

- "critica esta landing"
- "qué opinás de esta página"
- "analizá esta landing page"
- "is this AI slop?"
- "review this landing"

O simplemente pegando un screenshot o una URL de una landing y pidiendo un juicio visual.

## Lenguaje y tono

La skill responde siempre en **castellano**, en **primera persona**, con humor seco y sin relleno. No usa palabras vacías ("moderno", "limpio", "elegante", "pulido", "impecable"): si necesita una de esas, reformula con algo concreto. Si ve slop, lo dice. Si ve buen criterio, también — sin tibieza.

## La rúbrica

El corazón de la skill es la rúbrica completa dentro de `SKILL.md`: categorías, síndromes, reglas duras, criterios por sección, y el principio central detrás de todo — *¿se nota que alguien decidió esto, o parece que vino por default?*

## Licencia

MIT — ver [LICENSE](LICENSE).

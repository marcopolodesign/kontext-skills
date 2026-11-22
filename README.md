# Kontext skills

Agent skills from **Kontext by Marco Polo**, the design agent built by [Marco Polo](https://marcopolo.agency), a design and technology studio in Buenos Aires. Kontext checks how templated or AI-made a website looks, proposes redesign directions on the real brand, and gives coding agents a studio's design judgment.

> Not to be confused with FLUX.1 Kontext, Black Forest Labs' image-editing model. Different product.

## Install

```bash
npx skills add marcopolodesign/kontext-skills
```

Works with Claude Code, Cursor, Codex, Gemini CLI and any agent that reads `SKILL.md` files. To install by hand, copy `skills/kontext-review/` into your agent's skills folder (for Claude Code: `~/.claude/skills/`).

## Skills

| Skill | What it does |
|---|---|
| [`kontext-review`](skills/kontext-review/SKILL.md) | Strict design review of a page, landing or component. Blocks the patterns that make a site look AI-made (violet gradients, gradient text, a pill above the headline, emoji icons, invented social proof, template copy), gives every fix as Before / After / Why with the exact value, and ends with **Approve** or **Block**. Free, runs locally, no account. |

## Example

Ask your agent:

```
/kontext-review the landing page in app/page.tsx
```

You get one table, most serious first, and a verdict:

| Where | Before | After | Why |
|---|---|---|---|
| Hero headline | `bg-gradient-to-r from-violet-500 to-blue-500 bg-clip-text` | Solid `#111`, `text-7xl font-semibold leading-[1.05]` | Gradient text is the clearest sign of a template; hierarchy comes from size and weight |
| Above the headline | `<Badge>New · Launching 2026</Badge>` | Removed | A pill above the headline adds nothing; the headline opens the page |
| Feature cards | Three identical cards, icon on top, `shadow-lg border` | Show the real product; separate by fill (`bg-neutral-100`) | Three icon cards is the default AI layout |

**Verdict: Block**: remove the gradient text and the pill to approve.

## Going further: Kontext

The skill checks a page against fixed rules. [Kontext](https://kontext.marcopolo.agency/en?utm_source=github&utm_medium=readme&utm_campaign=kontext-skills) checks your site against **its own brand**:

- **Free check**: paste a URL and in about a minute get a 0–100 score of how templated or AI-made it looks, category by category (type, color, layout, components, copy, images), the brand kit it found, font pairings and a ready-to-paste prompt for every fix. No sign-up.
- **Kontext MCP**: the same design judgment inside Claude Code, Cursor or Gemini CLI: `analizar_sitio`, `revisar_pieza`, `verificar_marca`, `recomendar_tipografia`, `proponer_paleta`, `extraer_sistema`, `buscar_referencias`, `disenar_pieza` and more.

### Connect the Kontext MCP

Remote MCP server (Streamable HTTP) at `https://kontext.marcopolo.agency/api/mcp`. Get a key at [kontext.marcopolo.agency/conectar](https://kontext.marcopolo.agency/conectar?utm_source=github&utm_medium=readme&utm_campaign=kontext-skills), then:

```bash
claude mcp add --transport http kontext https://kontext.marcopolo.agency/api/mcp \
  --header "Authorization: Bearer <your-key>"
```

Cursor, or any client with a JSON config:

```json
{
  "mcpServers": {
    "kontext": {
      "url": "https://kontext.marcopolo.agency/api/mcp",
      "headers": { "Authorization": "Bearer <your-key>" }
    }
  }
}
```

Plans and pricing: [kontext.marcopolo.agency/precios](https://kontext.marcopolo.agency/precios?utm_source=github&utm_medium=readme&utm_campaign=kontext-skills).

## License

[MIT](LICENSE) © Marco Polo

# slidev-theme-pimskie-dev

Dark [Slidev](https://sli.dev) theme. Black & stinger yellow, bold condensed type (Anton), honeycomb details, hazard-tape dividers. Protect ya deck.

## Gebruik

In de frontmatter van je `slides.md`:

```yaml
---
theme: ../slidev-theme-pimskie-dev
---
```

(relatief pad vanaf je presentatiemap, of publiceer het als npm package en gebruik `theme: pimskie-dev`)

## Palet

| Token | Hex | Rol |
| --- | --- | --- |
| `--kb-black` | `#0e0d0b` | achtergrond (warm zwart) |
| `--kb-ink` | `#1a1814` | codeblokken, cards |
| `--kb-honey` | `#ffc91f` | primair: titels, links, markers |
| `--kb-amber` | `#e8940a` | secundair: h3, link-underline |
| `--kb-blood` | `#e33b2e` | nadruk: kickers, warnings, hover |
| `--kb-bone` | `#f2ede0` | bodytekst |
| `--kb-smoke` | `#96907f` | captions, attributies |

## Layouts

- `cover` — honingraat-achtergrond, XL titel, hazard-tape onderrand
- `section` — geïnverteerd: zwart op geel, voor hoofdstuk-overgangen
- `quote` — groot aanhalingsteken, laatste paragraaf = attributie

## Extra's

- `<div class="kicker">…</div>` — rode eyebrow boven een titel
- `---` in markdown (`<hr>`) — hazard-tape divider
- Hexagon-badge rechtsonder toont het slidenummer
- Code-highlighting: gruvbox-dark-hard (past bij het palet)

## Development

```bash
npm install
npm run dev
```

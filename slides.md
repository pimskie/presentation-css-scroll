---
theme: ./
title: Scroll? Snap!
transition: slide-left
mdc: true
layout: cover
---

# Scroll? Snap!

CSS-only carousels met: <br /> `::scroll-button`, `::scroll-marker-group`, `::scroll-marker` en `scroll-state()`


<!--
Native carousels in de browser. Vijf demo's, van basis snap tot scroll-state containers. Nul regels JavaScript.
-->

---

# Waarom

- Omdat het cool is en omdat het (bijna) kan
- Geen **~40 kB** JavaScript voor iets dat scrollt
- A11Y out of the box
- Keyboard en focus navigatie
- Geen resize observers, re-inits of gekke dingen nodig

<!--
Herkenbaar: elke library lost hetzelfde op — scroll-positie bijhouden, knoppen, dots, active state. Dat is precies wat de browser nu native doet.
-->

---

# De onderdelen

1. `scroll-snap`: "snappen" naar een element
2. `::scroll-button()`: de vorige / volgende _buttons_
3. `::scroll-marker-group`: waar de "dots" in geplaatst worden
4. `::scroll-marker`: slide "dots" met active state
5. `scroll-state()`: reageren op wat de scroll status is

Alle demo's staan in m'n [experiments repo](https://github.com/pimskie/experiments/tree/main/css-stuff/carousel).

---
layout: section
---

<div class="kicker">Deel 01</div>

# Snap

De basis: werkt al jaren, in elke browser

---

# Make it snappy

```css {2-3|5|10|all}
.carousel {
  display: flex;
  overflow-x: scroll;

  scroll-snap-type: x mandatory;
}

.slide {
  flex: 0 0 90%;
  scroll-snap-align: start;
}
```

**Dat is alles.**  <br />
Container: bepaalt manier (`mandatory` vs `proximity`) <br /> Slides: bepalen wáár ze snappen (`start`, `center`, `end`).

<!--
Klik 1: gewoon een flexbox met overflow. Klik 2: snap-type op de container. Klik 3: snap-align op de kinderen. Meer is het niet.
-->

---
layout: iframe-unscaled
url: /demos/10-snap/index.html
---

<!--
DEMO: sleep/scroll — hij snapt altijd netjes op de rand van een slide. Trackpad, touch, muiswiel: alles werkt, physics van de browser zelf.
-->

---
layout: section
---

<div class="kicker">Deel 02</div>

# `::scroll-button()`

Vorige / vorige, zonder event listeners en werkt out of the box

---

# Knoppen uit het niets

```css 
.carousel::scroll-button(inline-start) {
  content: '⬅️';
}

.carousel::scroll-button(inline-end) {
  content: '➡️';
}

.carousel::scroll-button(*) {
  width: 3rem;
  aspect-ratio: 1;
  border-radius: 100%;
}

.carousel::scroll-button(*):enabled:hover {
  scale: 1.05;
}
```

<!--
Pseudo-elementen op de scroller, met content erin. Het zijn ECHTE buttons: klik scrollt ~85% van de viewport, en aan de randen worden ze vanzelf :disabled. Je positioneert ze gewoon met grid-area.
-->

---

# Gratis, G..R..A..

- Het zijn **echte `<button>`-elementen** in de accessibility tree
- Automatisch `:disabled` aan het begin en einde, te stylen met `:enabled` / `:disabled`
- Positioneren? `grid` of fancy met [Anchor Position](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/position-anchor) / [Position Area](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/position-area) 

```css
.carousel {
  display: grid;
  grid-template-areas: "prev slides next";
  grid-template-columns: 5rem 1fr 5rem;
}
```

```css
.carousel::scroll-button(inline-start) {
 position-anchor: --carousel;
 position-area: inline-start;
}

```


---
layout: iframe-unscaled
url: /demos/20-buttons/index.html
---

<!--
DEMO: klik de knoppen — smooth scroll per pagina. Scroll helemaal naar het einde: de next-knop disabled zichzelf. Tab er eens naartoe: gewoon focusbaar.
-->

---
layout: section
---

<div class="kicker">Deel 03</div>

# `::scroll-marker`

Dots met active state

---

# Eén property, één pseudo

```css {1-3|5-10|12-14|all}
.carousel {
  scroll-marker-group: after;
}

.slide::scroll-marker {
  content: '';
  aspect-ratio: 1;
  border: 2px solid var(--blue-5);
  border-radius: 50%;
}

.slide::scroll-marker:target-current {
  background: var(--blue-6);
}
```

`scroll-marker-group: after` maakt de container, elke slide levert z'n eigen marker en `:target-current` matcht de dot van de slide die nu in beeld is.

<!--
Markers gedragen zich als anchor-links naar hun slide. :target-current is de "active dot" waar je normaal een IntersectionObserver voor schrijft.
-->

---
layout: iframe-unscaled
url: /demos/30-markers/index.html
---

<!--
DEMO: klik een dot — scrollt ernaartoe. Scroll met de hand — active dot loopt mee. A11y: de hele group is één tab-stop, daarbinnen navigeer je met pijltjestoetsen (zoals een radiogroup).
-->

---
layout: section
---

<div class="kicker">Deel 04</div>

# One pager carousel

---

# Fullpage-navigatie van je section-titels

```css {1-3|5-9|11-13|15-17|all}
.section::scroll-marker {
  content: attr(data-title);
}

.sections::scroll-marker-group {
  position: fixed;
  position-anchor: --scroll-container;
  position-area: block-start;
}

.section::scroll-marker:target-current {
  background: var(--accent);
}

.section::scroll-marker:target-before:not(:hover) {
  scale: 0.88;
}
```

`content: attr(data-title)` maakt van elke marker een tekstlabel, **anchor positioning** pint de group bovenaan de scroller, `:target-current` markeert waar je bent en `:target-before` weet welke secties je al voorbij bent.

<!--
Zelfde primitieven, totaal andere UI: een fullpage-scroller met sticky navigatie. :target-before/:target-after — je weet in CSS waar je bent in het verhaal.
-->

---
layout: iframe-unscaled
url: /demos/40-vertical/index.html
---

<!--
DEMO: scroll door de secties — de nav bovenaan loopt mee, gepasseerde labels krimpen. Klik op een label: smooth scroll ernaartoe. En na het scrollen dimt de hele nav (dat is al scroll-state — bruggetje naar deel 05).
-->

---
layout: section
---

<div class="kicker">Deel 05</div>

# `scroll-state()`

Container queries voor je scroll-status

---

# Reageren op snappen

```css {1-3|5-10|all}
.section {
  container-type: scroll-state;
  container-name: carousel;
}

@container carousel not scroll-state(snapped: inline) {
  .section-content {
    translate: 0 6rem;
    opacity: 0.4;
  }
}
```

Elke slide is z'n eigen container en **weet of hij gesnapt is**. Niet-actieve slides zakken weg en dimmen .
Naast `snapped`: ook `scrollable` (kan ik nog ergens heen?) en `stuck` (is m'n sticky element vastgeplakt?).

<!--
Dit verving vroeger een IntersectionObserver + class toggle. Nu: container query op scroll-status. snapped / scrollable / stuck zijn de drie smaken.
-->

---
layout: iframe-unscaled
url: /demos/50-scroll/index.html
---

<!--
DEMO: scroll — content van de gesnapte slide komt omhoog, de rest ligt verzonken. Knoppen zweven naast de carousel via anchor positioning. Alles wat we zagen komt hier samen: snap + buttons + markers + scroll-state.
-->

---

# Browser support

| Feature | Chrome / Edge | Firefox | Safari |
| --- | --- | --- | --- |
| `scroll-snap-type` | ✅ | ✅ | ✅ |
| `::scroll-button()` | 135+ | ❌ | ❌ |
| `::scroll-marker` / `:target-current` | 135+ | ❌ | ❌ |
| `scroll-state()` | 133+ | ❌ | ❌ |

<hr>

**Progressive enhancement by design**

<!--
Firefox en Safari hebben publiekelijk interesse getoond; het zit in de CSS Overflow spec. Voor productie: prima als enhancement, JS-fallback alleen als knoppen/dots kritisch zijn.
-->

---

# Bronnen

- [MDN - CSS carousels guide](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Overflow/Carousels)
- [Chrome blog - Carousels with CSS](https://developer.chrome.com/blog/carousels-with-css)
- [chrome.dev - carousel gallery](https://chrome.dev/carousel/horizontal/curved/)
- [utilitybend - Love at first slide](https://utilitybend.com/blog/love-at-first-slide-creating-a-carousel-purely-out-of-css/)
- [MDN - `::scroll-button()`](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/::scroll-button) · [`::scroll-marker`](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/::scroll-marker) · [`:target-current`](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/:target-current)

---

# What's next?

 - View Transition API?
 - De kracht van native elements?
 - CSS if/else?


---
layout: section
---

# Bedankt!

Vragen?

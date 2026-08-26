# 2026 Portfolio Design Research Log

## Research objective
Identify niche-forward, high-tech portfolio styles and interaction patterns suitable for:

1. A distinctive, professional photography portfolio for **Ettilapse Photography**.
2. A technical portfolio presenting ESP32 hardware work, AI-driven applications, scripts, tools, business websites, and blog/case-study writing.

## Evaluation criteria
- Feels current for 2026 without copying saturated "AI gradient + glass cards" aesthetics.
- Works elegantly on desktop and mobile.
- Uses motion or visual interaction purposefully, without damaging speed, readability, accessibility, or conversion.
- Supports high-quality photography and clear technical storytelling.
- Provides a real, buildable differentiator rather than novelty alone.

## Parallel research tracks
1. Emerging visual systems: palettes, typography, materials, and layouts.
2. Motion and interaction patterns with strong perceived polish.
3. Photography portfolio, gallery, viewing, and lightbox innovations.
4. Technical portfolio, project-detail, and blog/case-study patterns.
5. Responsive implementation and performance/accessibility practices.

## Context note
The provided historical Ettilapse Photography session URL presently resolves to a completed replay and then an unavailable-region page in this environment. Recommendations will therefore respect the stated brand name but avoid claiming specific business positioning that could not be retrieved.

## Evidence notes from first research pass

### Broad 2026 web direction
Figma's 2026 web-trends overview identifies **3D and immersive elements**, **experimental navigation**, **vibrant color palettes**, **bold typography**, **motion design**, **gamified design**, **retrofuturism**, **maximalism**, **collage**, **neo-brutalism**, and **sustainable web design** as active directions. The useful takeaway is not to copy every trend, but to combine a small number into a coherent system: for example, raw grid structure plus rich color accents for tech, or editorial minimalism plus unexpected gallery motion for photography.

### More selective UI direction
Tubik's 2026 UI perspective is especially relevant because it argues for **purposeful motion rather than decorative animation**, **raw aesthetics using visible grids, monospaced type, and wireframe logic**, **fluid typography using clamp()**, **motion controls**, and **crafted/authored identity**. This supports a portfolio that feels advanced through structure, responsiveness, and intent rather than generic glow effects.

### Photography portfolio evidence
Framer's photography portfolio survey emphasizes image quality, intuitive navigation, and a site style aligned with the photographer's point of view. Specific useful patterns include S/M/L gallery viewing modes, book-like image paging, fixed typographic branding under moving images, color-organized indexes, horizontal gallery movement, hover-triggered campaign previews, parallax album unfolding, and video/self-portrait elements for trust.

### Technical portfolio evidence
Developer-portfolio references consistently support portfolios as proof of skill, not just resumes. Strong patterns include live demos, GitHub links, screenshots, short videos, clear project summaries, case studies with problem/approach/result, visible personality, and creative interaction. Embedded-systems project references reinforce that hardware work should be documented with runtime measurements, drivers, buses, test suites, bootloaders, peripherals, UI controls, diagrams, and real-world constraints.

### Performance and accessibility guardrails
W3C's WCAG material states that motion animation triggered by interaction should be disableable unless essential. MDN documents the `prefers-reduced-motion` media feature as a way to detect reduced-motion preferences. web.dev emphasizes responsive images through `srcset`, `sizes`, modern formats such as WebP/AVIF, compression, and lazy loading, which matters heavily for photography portfolios.

### Niche-forward style signals worth selectively adopting
- Adobe's 2026 outlook reinforces tactile/sensory experiences, exaggerated type, saturated-yet-controlled color, surreal scale shifts, imperfect/organic details, and freeform editorial layouts.
- Kittl identifies more niche visual languages that are suitable as **ingredients**, not complete skins: blueprint design, grainy blur, signal graphics, surveillance-style systems, type collage, retro-futurist optimism, and human/handmade texture.
- Sessions similarly frames the durable tension as **high-tech clarity plus human texture**, rather than one dominant aesthetic.

### Motion implementation opportunity
MDN documents native CSS scroll-driven animations (scroll and view timelines) and the View Transition API. These enable lightweight image reveals, reading-progress indicators, gallery expansion, and continuity between project index and detail page. Treat them as progressive enhancement with ordinary, instant navigation as the baseline.

### Live-source checks
Browser review confirmed the design trends and photography references are current and consistent with extracted findings. The photography reference visibly emphasizes a dark, editorial presentation and its examples validate S/M/L gallery modes, color organization, horizontal exploration, campaign hover previews, and restrained but expressive motion.

### Recommendation boundary
Avoid a generic all-in-one visual direction. The user has two different audiences: photography clients need confidence, emotion, and a frictionless inquiry path; technical clients, employers, and collaborators need evidence, legibility, and a quickly scannable record of capability. The strongest approach is shared personal identity with two clearly differentiated visual operating systems.

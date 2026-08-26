# CLAUDE.md — Ettilapse Photography / Chromatic Monograph

## Mission

You are building and maintaining the public-facing portfolio for **Ettilapse Photography**. Treat this as a client-facing photography experience, not a generic creator template, a SaaS marketing page, or a coding exercise.

> **North star:** create a living editorial monograph where the photography does the emotional work, the interface gives visitors confidence and orientation, and inquiry feels like the natural next frame.

The intended visual direction is **Chromatic Monograph**: warm, editorial, cinematic, restrained, and distinctive. The site must feel like a carefully printed photography book translated for the web—not a masonry gallery with a dark overlay.

## Instruction hierarchy

1. Follow explicit user directions first.
2. Follow this `CLAUDE.md` for product, design, content, and quality decisions.
3. Use `SKILLS.md` for task-specific implementation checklists.
4. Use `AGENTS.md` as the extended cross-tool source of truth when detail is needed.
5. Inspect the repository's actual framework, content model, scripts, and conventions before assuming an implementation approach.

If instruction files disagree, prefer the more specific, safety-preserving direction. Never silently trade image integrity, accessibility, privacy, or inquiry reliability for visual novelty.

---

## Product goals

The portfolio has four jobs:

1. Help visitors discover the right body of work.
2. Make each project feel like a coherent photographic story, not an image dump.
3. Establish a distinctive point of view while remaining easy to use and professional.
4. Give interested clients a frictionless, approved way to inquire.

The photography is the product. The interface is successful only when it strengthens image pacing, navigation confidence, and client trust.

## Do not invent business facts

Never fabricate, infer, or publish any of the following without an approved content source:

- Contact email, phone number, address, location, or booking availability.
- Service packages, prices, client names, testimonials, awards, publications, or audience claims.
- Image captions, locations, dates, project categories, or consent-sensitive details.
- Performance metrics, analytics, conversion claims, or social proof.

Use approved CMS content or clearly marked non-production placeholders. Never write placeholders that could be mistaken for a real client statement.

---

## The design system

### Visual principles

| Principle | Required expression |
| --- | --- |
| **Images lead** | A photograph is the most visually important object in any image-led viewport. |
| **Editorial contrast** | Warm paper, deep ink typography, restrained rules, and deliberate asymmetry create the structure. |
| **Color is functional** | Vermilion and ultramarine signal state, navigation, or collection; they are not background decoration. |
| **Texture is peripheral** | Grain, crop marks, and print details may live on empty canvas areas, never obscure final images. |
| **Motion is explanatory** | Movement only orients, reveals, or confirms. It is not a spectacle. |
| **Restraint builds luxury** | Use one memorable gallery interaction rather than many superficial effects. |

### Starting design tokens

Centralize design values as CSS variables, a theme object, or an equivalent token system. These are adjustable defaults, not immutable brand facts.

```css
:root {
  --paper: #F4F0E8;
  --ink: #111216;
  --body: #3A3D45;
  --vermillion: #E64B2D;
  --ultramarine: #2754E8;
  --rule: color-mix(in srgb, var(--ink) 15%, var(--paper));
  --muted-ink: color-mix(in srgb, var(--ink) 62%, var(--paper));
  --radius-minimal: 2px;
}
```

Use a display serif and a practical grotesk. Example direction: a variable editorial serif such as `Fraunces` paired with a sober UI face such as `Geist`. Keep the active font system to two families unless a deliberate, approved brand decision requires more.

### Avoid

Do not introduce glassmorphism, generic dark panels, rounded-card dashboards, aurora gradients, parallax scenes, custom cursors, AI-generated decorative copy, code-like backgrounds, or visual effects that require visitors to wait before seeing the work.

---

## Required information architecture

Keep the top-level navigation compact and intentional.

| Route | Purpose |
| --- | --- |
| **Work** | The primary Chromatic Index and gallery discovery experience. |
| **Stories** | Curated project sequences that reveal full photographic worlds. |
| **About** | An approved introduction, working approach, and approved credibility elements. |
| **Inquire** | The single clear approved contact path. |

Do not add pages because a starter template includes them. A newsletter, login, chatbot, pricing page, shop, booking embed, or elaborate navigation requires explicit user approval.

---

## Experience requirements

### 1. The home page

The home page should move visitors through a simple sequence:

`Arrive` → `feel the point of view` → `choose Work / Stories / Inquire` → `see proof` → `act when ready`

The hero must be visually calm, image-led, and quick to load. It may use one image, a small editorial selection, or a subtle approved transition. It must not autoplay a heavy video, hide the navigation, or force a scroll effect before showing the work.

### 2. The Chromatic Index

The gallery is the signature experience. It should be organized using real, approved project collections or an intentional visual taxonomy such as light, color, mood, or story type. It is **not** an algorithmic "dominant color" filter.

Required behaviors:

- Support an **Index** view for fast visual scanning.
- Support a **Story** view for immersive project reading.
- Make project title and image count available on pointer hover **and** keyboard focus.
- Preserve logical DOM and keyboard order even if the visible grid is asymmetric.
- Return visitors to the same gallery position after closing a story.
- Keep filters limited, clear, URL-addressable when appropriate, and useful without JavaScript.

A third density switcher such as `S / M / L` is optional. Do not add it unless it clarifies gallery browsing rather than creating a novelty control.

### 3. The Story Reader

Every project should read as a photographic essay:

`Project cover` → `opening image` → `deliberate pacing` → `optional field note` → `story close` → `inquire`

A story generally contains a curated sequence of 12–24 images. The exact number must serve the story, not a fixed template.

The reader must provide:

- Title and a concise approved description or field note.
- Clear current-image context when the sequence has discrete steps.
- Previous/next controls that work with pointer, keyboard, and touch.
- Escape or close behavior where an overlay/reader is used.
- A visible return to the index and focus restoration to the originating tile.
- An inquiry invitation at the story conclusion, not aggressively throughout the sequence.

### 4. Inquiry

Inquiry must be always reachable but never visually dominant.

- Keep the approved inquiry route in persistent navigation.
- Add a quiet invitation at relevant story endings.
- Keep the form short; only collect approved, necessary information.
- Implement visible submit, success, validation, and error states.
- Do not imply booking, response times, privacy policy, pricing, or availability without approved copy.
- Do not add pop-ups, forced email capture, or intrusive scheduler widgets.

---

## Image, content, and privacy rules

### Image integrity

- Never substitute stock photography for approved portfolio work in production.
- Do not crop, color-treat, blur, or overlay a photographer's final image without approval.
- Preserve the intended aspect ratio and focal point.
- Use explicit image dimensions to prevent layout shift.
- Serve responsive image sources, preferably AVIF/WebP with an appropriate fallback where supported.
- Eager-load only the first meaningful viewport images; lazy-load deeper gallery content.
- Strip or protect sensitive metadata where content pipelines expose it.

### Structured content

Build projects from structured data or CMS content rather than hard-coded page fragments. The source should be able to express a title, summary, category, image sequence, focal point, alt text, optional field note, published state, and sort order.

```ts
type PhotographyProject = {
  slug: string;
  title: string;
  summary?: string;
  categories: string[];
  moodTags?: string[];
  coverImage: ImageAsset;
  images: ImageAsset[];
  fieldNote?: string;
  featured?: boolean;
  published?: boolean;
  order?: number;
};

type ImageAsset = {
  src: string;
  alt: string;
  width: number;
  height: number;
  caption?: string;
  focalPoint?: { x: number; y: number };
};
```

Do not expose private galleries, client-sensitive project data, hidden route metadata, raw image filenames, EXIF data, or unpublished images in client bundles, feeds, site maps, or public routes.

---

## Accessibility and motion requirements

Accessibility is part of the premium experience.

- Use semantic landmarks, headings, lists, buttons, and links.
- All interactive gallery controls need accessible names and visible keyboard focus.
- Hover cannot be the only way to learn a project title or activate a control.
- Preserve a logical reading order beneath visual grid placement.
- Do not make swipe the only way to change images.
- Keep text readable over images; use an approved contrast treatment rather than hoping the photo is dark enough.
- Test at narrow mobile width and 200% browser zoom.

Motion requirements:

- Use motion only to orient, reveal, or confirm.
- Prefer opacity, transform, and color changes; avoid layout-thrashing animations.
- Typical UI transitions should feel short and quiet—around 160–280 ms.
- Native View Transitions may be used as a progressive enhancement for gallery-to-story continuity.
- Provide a complete `prefers-reduced-motion: reduce` mode. It must remove nonessential transforms, auto-cycling media, parallax, and scroll-linked decoration while retaining all functions.
- Never use scroll hijacking, cursor trails, blocking preloaders, or autoplay hero video as a visual substitute for art direction.

---

## Claude Code working protocol

When implementing any change:

1. **Inspect first.** Read the existing routing, components, data model, scripts, and visual conventions. Run the existing project checks before making broad claims about baseline behavior.
2. **State a bounded plan.** Identify likely files, expected user-facing behavior, and any content or asset assumptions.
3. **Make the smallest coherent change.** Do not redesign unrelated pages while adding a single gallery or inquiry behavior.
4. **Build the semantic/static path first.** Page content, navigation, and inquiry must work without decorative animation or fragile client-only logic.
5. **Add the enhancement.** Layer refined motion, image transitions, and gallery behavior only after the basic experience is correct.
6. **Test the visual and functional path.** Check desktop, narrow mobile, keyboard navigation, focus restoration, reduced motion, image layout stability, and error states.
7. **Report honestly.** Summarize changed files and behavior, then explicitly flag any unverified content, image, contact, or analytics detail still needed from the owner.

Never modify deployment secrets, analytics, legal text, third-party form configuration, DNS, payment, or publish settings without explicit authorization.

---

## Definition of done

A change is complete only when it:

- Reinforces the **Chromatic Monograph** direction.
- Uses approved content or unmistakable development placeholders.
- Works on desktop, mobile, keyboard, touch, and reduced-motion settings.
- Preserves image quality, layout stability, and focal intent.
- Has no required interaction that depends only on hover, swipe, animation, or JavaScript.
- Keeps inquiry reachable and reliable.
- Passes the repository's configured lint, type, build, and test commands.

Before shipping, ask:

> **Would a visitor remember the images and the feeling of the story—or only remember the interface?**

If the answer is the interface, remove or soften the effect.

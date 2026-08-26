# AGENTS.md — Ettilapse Photography / Chromatic Monograph

## Purpose and portability

This file is the source of truth for any coding agent, editor, or contributor working on the **Ettilapse Photography** portfolio website. It is intentionally written as plain Markdown so it can be used in GitHub-based workflows, Cursor, Claude Code, and other agentic coding environments.

Keep this file in the repository root as `AGENTS.md`. If a platform needs its own instruction file, copy or reference this source rather than maintaining divergent rules. Typical adapters may include `CLAUDE.md`, `.github/copilot-instructions.md`, or a Cursor project rule that points contributors back to this document.

> **North star:** build an art-directed, client-ready photography experience that feels like a living monograph—not a generic masonry grid with a dark overlay.

---

## 1. Product intent

The site represents **Ettilapse Photography**. Its primary job is to make prospective clients feel two things at once: **this photographer has a distinctive visual point of view**, and **this is a professional who will make it easy to inquire and work together**.

Photography is the product. The interface should choreograph attention around the images, not compete with them. Every addition must improve one of these outcomes:

1. Help visitors discover the right body of work.
2. Help them feel the quality, pacing, and perspective of a full story.
3. Help them understand what the photographer offers.
4. Make it easy and comfortable to inquire.

Never invent or publish a phone number, email address, service list, client testimonial, award, publication, availability statement, price, or location. Use the approved content source or clearly marked local placeholders until verified content is supplied.

---

## 2. The chosen design direction

### Concept: **Chromatic Monograph**

The visual system combines editorial restraint with a memorable gallery mechanic. It should feel like a carefully printed photography monograph that happens to be responsive and alive.

| Layer | Direction |
| --- | --- |
| **Mood** | Editorial, cinematic, warm, confident, intimate, composed. |
| **Layout** | Generous white or warm-paper space; disciplined asymmetry; images have room to breathe. |
| **Signature interaction** | A color- or mood-led image index, with clear `Index` and `Story` viewing modes. |
| **Typography** | High-contrast editorial serif for display moments; clean grotesk for navigation, metadata, and body copy. |
| **Motion** | Soft, spatial, and short. Motion preserves context when an image opens or a story changes. |
| **Conversion** | Inquiry is consistently available but never loud or salesy. |

### Baseline tokens

These are design defaults, not inviolable brand facts. Prefer CSS custom properties and make them easy to adjust.

```css
:root {
  --paper: #F4F0E8;
  --ink: #111216;
  --vermillion: #E64B2D;
  --ultramarine: #2754E8;
  --muted-ink: color-mix(in srgb, var(--ink) 62%, var(--paper));
  --rule: color-mix(in srgb, var(--ink) 15%, var(--paper));
  --radius-minimal: 2px;
}
```

Use color to orient the gallery and identify interaction states. Do **not** apply saturated color washes or heavy texture on top of final photographs.

### Typography behavior

Use a distinctive, licensed or open-source variable serif for display type and a highly legible grotesk for UI/body text. Example pairing: `Fraunces` for display and `Geist` for UI. Do not load more than two font families unless a deliberate brand decision is made.

- Titles can be large and editorial, but remain readable on a 320 px viewport.
- Interface labels should be concise, calm, and not all-caps by default.
- Body copy should be at least 16 px, with comfortable line length and contrast.
- Prefer fluid type scales with `clamp()` over breakpoint-only jumps.

---

## 3. Required experience and information architecture

### Top-level navigation

Keep navigation intentionally small. The exact labels may evolve, but the expected information architecture is:

- **Work**: primary gallery/index.
- **Stories**: curated project sequences or collections.
- **About**: short positioning, working style, and approved credentials.
- **Inquire**: clear, direct contact path.

Do not add a page merely because a template includes it. Do not bury inquiry at the end of a long page.

### Gallery modes

The gallery must support two clear views:

| Mode | Intent | Desktop behavior | Mobile behavior |
| --- | --- | --- | --- |
| **Index** | Fast visual discovery. | Editorial grid with varied but deterministic image spans; optional color/mood organization. | One-column or two-column visual index with large tap targets. |
| **Story** | Immersive project viewing. | One image or carefully paired images at a time; contextual project rail and keyboard navigation. | Vertical reader with a simple project header and visible image count. |

A third `S / M / L` density control is allowed only if it stays understandable and does not become a design toy. On mobile, avoid presenting three competing layout choices.

### Project story requirements

Each project story should support:

1. Project title and a short, human description.
2. A deliberate sequence of 12–24 images by default, not an unfiltered image dump.
3. Optional small notes such as location, project type, or a short field note, only when approved.
4. A non-disruptive image counter and previous/next controls.
5. A clear way back to the index.
6. A gentle inquiry prompt near the story conclusion.

A story page must be useful with JavaScript disabled or failed: images, captions, navigation, and inquiry access must remain present in normal document order.

---

## 4. Signature interactions

### Chromatic Index

The principal interaction is a visual index organized around color, light, mood, or an approved collection taxonomy. It must enhance discovery rather than look like a filter demo.

- An image tile reveals a project title and an image count on hover/focus.
- The focus state must work with keyboard navigation; hover is never the only way to reveal a title.
- Prefer actual content tags or a transparent editorial curation step. Do not fabricate dominant-color classifications that create misleading project groupings.
- Keep source order and keyboard order logical even if CSS grid placement varies.

### Context-preserving image reader

When a visitor opens an image from the index, preserve a sense of where it came from:

- Use native View Transitions as a progressive enhancement where supported.
- Otherwise, use a quick opacity/scale transition or an immediate open.
- Always provide a visible close/back action, keyboard escape behavior, and focus restoration to the originating tile.
- Do not trap users in a modal without logical screen-reader labels and a robust close path.

### Motion rules

Use motion only to orient, reveal, or confirm.

- Default transition duration: approximately 160–280 ms for UI states; up to 500 ms for a rare, intentional story transition.
- Prefer opacity, transform, and color changes over layout-thrashing animation.
- Honor `prefers-reduced-motion: reduce` by removing transforms, parallax, auto-cycling media, and nonessential scroll animation.
- Never use scroll hijacking, cursor trails, page-load delays, or an autoplay hero video that blocks the work.

---

## 5. Image, accessibility, and performance rules

### Image handling

The portfolio cannot feel premium if it is slow or visibly soft.

- Use responsive image sources with explicit width and height.
- Prefer AVIF or WebP with a JPEG fallback when tooling supports it.
- Eager-load only the hero and the first visible work images. Lazy-load the remaining images.
- Reserve layout space to prevent layout shift.
- Preserve image aspect ratios. Do not crop or apply a visual treatment that changes the photographer's intended composition without approval.
- Use meaningful alt text appropriate to the image's role. Do not generate decorative alt text for purely decorative images.

### Accessibility baseline

- All interactive gallery elements must be keyboard reachable and visibly focused.
- Gallery controls need names that screen readers can understand.
- Use semantic landmarks and headings.
- Keep text contrast high enough on every background; do not rely on text over busy photos without a readable treatment.
- Do not make swipe the sole mechanism for navigating images.
- Respect reduced motion and test at 200% browser zoom.

### Performance budget mindset

Choose the smallest technical approach that delivers the experience. No large 3D library, animation framework, or custom cursor is justified unless it solves a defined experience problem. Measure before adding more motion or media.

---

## 6. Content model

Treat content as structured data, not hard-coded JSX fragments.

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

Keep unpublished, private, or client-sensitive galleries out of public static routes. Never expose client metadata accidentally through page source, generated feeds, filenames, or image EXIF data.

---

## 7. Agent implementation protocol

When asked to implement or change this site, follow this order:

1. **Inspect first.** Identify the framework, routing, existing content source, component conventions, and build/test commands before editing.
2. **State a short plan.** Name the files or components likely to change and call out any visual or data assumptions.
3. **Build the smallest coherent slice.** Do not redesign unrelated pages while adding one gallery feature.
4. **Preserve content and image integrity.** Do not replace approved photos, crop them casually, or write fictional client copy.
5. **Test desktop and mobile behavior.** Check keyboard movement, focus restoration, narrow viewport layouts, and reduced motion.
6. **Report what changed.** Summarize behavior, content assumptions, and anything still awaiting approved material.

### Do not

- Do not substitute generic stock photography for supplied work in a production build.
- Do not fabricate reviews, project details, packages, booking availability, awards, or press.
- Do not add a chatbot, pop-up, newsletter gate, or account system unless explicitly requested.
- Do not turn the gallery into a template-like masonry wall.
- Do not make visual effects more important than image quality or inquiry conversion.
- Do not remove existing analytics, legal text, accessibility features, or SEO metadata without explicit approval.

---

## 8. Definition of done

A feature is not complete until:

- It reinforces the **Chromatic Monograph** visual direction.
- It behaves correctly on mobile, desktop, keyboard, and reduced-motion settings.
- It retains a functional no-animation fallback.
- It does not degrade image loading or layout stability.
- It uses real approved content or plainly marked placeholders.
- It includes accessible names, focus states, and semantic structure.
- It leaves a clear route to the approved inquiry/contact destination.
- It passes the project's existing lint, type-check, build, and test commands.

---

## 9. Short design test

Before shipping, ask:

> **Would a visitor remember the images and the feeling of the stories—or only remember the interface?**

If the answer is the interface, simplify the interface.

# SKILLS.md — Ettilapse Photography / Chromatic Monograph

## How to use this guide

This guide turns the project direction in `CLAUDE.md` into task-oriented skills. Use it whenever you are asked to create, revise, test, or review a part of the **Ettilapse Photography** site.

Read `CLAUDE.md` before acting. Use the relevant skill below as a checklist; do not blindly apply a skill if it conflicts with the actual repository architecture or an explicit user direction.

| Skill | Use when working on |
| --- | --- |
| `01-art-direction` | Typography, color, layout, visual polish, or design-system components. |
| `02-home-experience` | Homepage, navigation, hero, featured stories, or the first-visit flow. |
| `03-chromatic-index` | Gallery/grid browsing, filtering, project previews, and index state. |
| `04-story-reader` | Project pages, image sequencing, lightbox/reader behavior, and captions. |
| `05-inquiry-experience` | Contact routes, inquiry forms, validation, success/error states, and trust copy. |
| `06-media-performance` | Image processing, responsive sources, loading, layout shift, and metadata safety. |
| `07-accessibility-motion` | Keyboard behavior, focus handling, responsive interaction, motion, and reduced-motion mode. |
| `08-content-governance` | CMS/data model, approved copy, privacy, publishing controls, and client-sensitive work. |
| `09-release-review` | Before merging, deploying, or declaring a feature complete. |

---

## 01 — Art direction

### Objective

Preserve the **Chromatic Monograph** visual language: editorial restraint, warm materiality, confident typography, intentional asymmetry, and image-first hierarchy.

### Build rules

- Start from a warm-paper base, deep ink text, understated divider rules, and restrained accent signals.
- Use a display serif for exhibition-scale titles and a practical grotesk for reading and interface controls.
- Keep surface geometry mostly square or minimally rounded. Avoid generic rounded SaaS cards.
- Let whitespace function as pacing. Do not fill every interval with labels, chips, or decoration.
- Use vermilion or ultramarine sparingly for focus, active collection, progress, and small editorial marks.
- Ensure the photograph—not type, grain, or decoration—wins the hierarchy wherever media is visible.

### Reject these patterns

| Do not use | Reason |
| --- | --- |
| Glass cards, thick shadows, glow effects | They make the site feel generic and distract from photography. |
| Full-screen gradients or AI-style aurora backdrops | They age quickly and reduce image contrast. |
| A UI chrome-heavy dashboard layout | The site is an exhibition, not a productivity tool. |
| Decorative fake film frames or overlays on every image | They alter the photograph and become repetitive. |
| Multiple competing display fonts | They weaken the brand's editorial voice. |

### Review questions

- Is the primary photo more visually important than its surrounding interface?
- Could a visitor describe the layout as "deliberate" rather than "busy"?
- Does the accent color explain state, or is it only decoration?
- Would removing one visual element improve the frame? If yes, remove it.

---

## 02 — Home experience

### Objective

Move a first-time visitor from point of view to exploration without an onboarding sequence or a sales funnel feeling.

### Required path

`Arrive` → `feel the image world` → `choose Work / Stories / Inquire` → `see proof` → `act when ready`

### Build checklist

- [ ] The main navigation is visible or reachable immediately.
- [ ] The hero includes a visible next step without competing calls to action.
- [ ] The first image(s) establish photographic voice before long explanatory copy.
- [ ] Featured work links to actual curated stories—not placeholder cards.
- [ ] About, Work, Stories, and Inquire remain easy to reach.
- [ ] Approved credibility elements appear only when they are real and current.
- [ ] The page remains useful when motion is disabled or the hero media fails to load.

### Hero constraints

Use one strong frame, a small curated set, or an intentional quiet transition. Never ship a large autoplay video just to make the homepage feel premium. If video is approved, provide a poster image, no sound, a reduced-motion fallback, a pause path if it runs continuously, and a performance budget.

---

## 03 — Chromatic Index

### Objective

Make exploration feel curated and memorable while retaining the speed and clarity of a conventional gallery.

### Functional model

`Open Work` → `scan visual families` → `focus a tile` → `preview project` → `enter Story Reader` → `return to the same place`

### Visual families

Groups may be based on approved collection names, image worlds, light, color, emotional temperature, or project type. They must be intentional editorial decisions—not a guessed automatic color classification.

### Required behaviors

- [ ] Each tile links to a project or a clearly defined image set.
- [ ] Project title and image count are available on hover **and** focus.
- [ ] A thumbnail's DOM order matches a logical reading and keyboard order.
- [ ] Visible grid asymmetry does not break Tab movement or screen-reader sequence.
- [ ] The current collection/filter state can be represented in the URL where the application supports it.
- [ ] Closing a Story Reader restores scroll position and focus to the selected tile.
- [ ] `Index` and `Story` are distinct, understandable modes; do not add density controls unless they make real browsing easier.

### Implementation notes

Use CSS Grid with authored tile spans or a CMS-driven layout map rather than a random masonry algorithm. Avoid a client-only gallery that renders blank without JavaScript. If a gallery uses client-side filtering, server/static content should retain a meaningful default order.

### Test cases

| Test | Expected result |
| --- | --- |
| Tab through a dense index | Every tile is reachable in a logical order and has a visible focus state. |
| Open a project, then close | The originating tile receives focus and the scroll position is preserved. |
| Turn off motion | Opening is immediate but clear; no function is removed. |
| Narrow viewport | The index becomes easier to tap without hiding title or project context. |

---

## 04 — Story Reader

### Objective

Turn a project sequence into a photographic essay with rhythm, context, and a natural way forward.

### Required structure

`Project cover` → `opening frame` → `image pacing` → `optional note` → `story close` → `inquire`

### Reader checklist

- [ ] The project title and a concise approved description appear before or alongside the story.
- [ ] The image sequence is curated; it is not a raw upload gallery.
- [ ] The reader has clear previous, next, and return-to-index actions.
- [ ] The image count or progress indicator provides orientation without stealing attention.
- [ ] Keyboard users can move, close/return, and recover focus.
- [ ] Touch users have explicit controls; swipe can supplement but never replace them.
- [ ] Field notes are optional, succinct, and approved.
- [ ] The final state suggests another story or the inquiry path at the right moment.

### Image pacing patterns

Choose the sequence pattern based on the actual work.

| Pattern | Use when | Example pacing |
| --- | --- | --- |
| **Cinematic arc** | A narrative, event, or travel story has a clear beginning and release. | Establishing frame → intimate detail → high-energy moment → quiet final image. |
| **Portrait study** | The power comes from subtle shifts in subject, gesture, and light. | Full portrait → crop/detail → environmental scene → return to subject. |
| **Editorial pairings** | Two images become stronger in conversation. | Wide frame + close detail, or shadow + color response. |
| **Minimal series** | Each selected frame needs room to breathe. | One full image at a time with generous empty space. |

Do not impose pairings or full-bleed imagery merely to create a visual pattern. The project sequence decides the layout.

### Context-preserving expansion

When an image/project opens from the index, the interaction should imply continuity:

- Use the View Transition API only as an enhancement where it behaves reliably.
- Otherwise, use an immediate state change or a short opacity/transform shift.
- Retain a visible back/close route and preserve focus.
- Never trap keyboard focus in a reader without an obvious exit.
- Never turn reader navigation into automatic playback without explicit visitor control.

---

## 05 — Inquiry experience

### Objective

Support a high-intent visitor without disrupting the image experience or inventing a sales process.

### Entry points

- Persistent navigation link.
- Contextual link within approved About content.
- Quiet story-end invitation.

### Form checklist

- [ ] Only necessary, approved fields are shown.
- [ ] Labels are visible; placeholders are not the only labels.
- [ ] Required fields and validation errors are explained in text.
- [ ] Submit state is clear and prevents accidental duplicate submission.
- [ ] Success state confirms receipt using approved copy.
- [ ] Errors preserve typed content where feasible and explain the recovery path.
- [ ] Spam mitigation does not create a hostile client experience.
- [ ] Contact routing, email delivery, privacy wording, and response-time claims are verified—not guessed.

### Never add without approval

Pop-ups, timed conversion banners, forced newsletter signup, fake scarcity, complicated calendars, payment fields, or automatic SMS integrations.

---

## 06 — Media performance

### Objective

Keep portfolio images rich and true to the photographer's work while making the site feel immediate on a normal mobile connection.

### Image delivery checklist

- [ ] Record width, height, alt text, and optional focal point for every content image.
- [ ] Use responsive image sources (`srcset`/`sizes` or framework equivalent).
- [ ] Prefer modern formats such as AVIF/WebP where the toolchain supports them; maintain a compatible fallback.
- [ ] Set intrinsic dimensions or aspect-ratio containers to avoid layout shift.
- [ ] Eager-load only genuinely above-the-fold media.
- [ ] Lazy-load lower-priority content without delaying a user's next intentional image.
- [ ] Use a subtle placeholder only if it improves perceived continuity; do not use flashy blur effects that distort final image color.
- [ ] Do not recompress approved final images without confirming the export and quality requirements.

### Metadata and privacy

Before publishing, confirm that public delivery does not expose unwanted EXIF metadata, private client names, private folder paths, location coordinates, or unpublished image derivatives.

### Performance triage

If the gallery is slow, first inspect image size, responsive source choice, loading priority, layout shift, and embedded third-party scripts. Do **not** remove accessibility, flatten the gallery, or lower image quality indiscriminately as a first reaction.

---

## 07 — Accessibility and motion

### Objective

Make the gallery feel refined for all visitors, including keyboard users, touch users, people who prefer less motion, and visitors on constrained devices.

### Interaction checklist

- [ ] All interactive elements are actual buttons or links, not clickable `div`s.
- [ ] Focus order matches the intended reading order.
- [ ] Focus is visible on the paper and ink palette.
- [ ] Text that appears on image hover also appears on focus and touch interaction.
- [ ] Image controls have meaningful accessible names.
- [ ] Escape/close behavior is predictable and restores focus where appropriate.
- [ ] Screen-reader users can understand gallery structure, project titles, counts, and reader position.
- [ ] Swipe is optional; buttons remain visible and usable.

### Motion checklist

- [ ] Decorative motion is removed or minimized under `prefers-reduced-motion: reduce`.
- [ ] Story and gallery functionality remains unchanged under reduced motion.
- [ ] No parallax, scroll hijacking, cursor trail, or long preloader is required.
- [ ] A motion sequence only conveys location, progress, or feedback.
- [ ] The frame rate and loading path remain stable without a huge animation library.

### Responsive review targets

Review at minimum on a narrow phone width, a common tablet width, a laptop/desktop width, and at 200% browser zoom. Do not rely on fixed viewport breakpoints alone; use fluid layout and typography where sensible.

---

## 08 — Content governance

### Objective

Protect photography, clients, and brand credibility while making the portfolio straightforward to update.

### Content rules

- Use structured content entries for projects, images, categories, notes, publication state, and sort order.
- Treat `published: false` or equivalent as a strict public-route boundary.
- Keep credentials, testimonials, and awards in an approval-controlled content source.
- Keep gallery labels short and meaningful.
- Use alt text that matches the image's function. Decorative visuals can use empty alt text; featured images need a useful description.
- Do not write fictional field notes, editorial copy, client quotes, project names, or titles.

### Content intake template

When adding a new story, collect the following from the owner before publishing:

| Field | Requirement |
| --- | --- |
| Project title | Approved public title. |
| URL slug | Stable, readable, and unique. |
| Cover image | Approved, appropriately sized, and correctly focused. |
| Image sequence | Curated order, not raw upload order. |
| Categories / visual family | Approved label(s). |
| Short description | Approved public language. |
| Field note | Optional; confirm it is safe to publish. |
| Alt text | Provided or reviewed for meaningful images. |
| Visibility | Public, scheduled, private, or excluded. |
| Inquiry context | Optional approved project-specific prompt. |

---

## 09 — Release review

### Objective

Catch the mistakes that make photography portfolios look unprofessional: broken image positioning, lost context, nonfunctional mobile controls, slow load paths, accidental privacy exposure, and overdesigned interaction.

### Pre-merge / pre-deploy checklist

#### Visual

- [ ] The page remains editorial and calm rather than card-like or app-like.
- [ ] Text does not overpower photography.
- [ ] Accent color is restrained and purposeful.
- [ ] Images retain correct aspect ratio, crop, and focal intent.
- [ ] Blank space and rules create rhythm rather than wasted area.

#### Functional

- [ ] Work → project → back to Work retains visitor context.
- [ ] Index, Story, About, and Inquire routes all work from direct URLs.
- [ ] Contact form has validated submit, success, and error states.
- [ ] The site does not depend on hover, swipe, or animation for essential actions.
- [ ] Keyboard and screen-reader paths are coherent.

#### Responsive and performance

- [ ] The first viewport loads a meaningful image and navigation quickly.
- [ ] Lower gallery images are deferred appropriately.
- [ ] No layout shifts occur as images arrive.
- [ ] The mobile version looks composed, not shrunken.
- [ ] Reduced-motion mode is complete.

#### Content and safety

- [ ] All public claims, labels, testimonials, images, and contact details are approved.
- [ ] No secrets, raw private file paths, unwanted metadata, unpublished work, or client-sensitive data are public.
- [ ] The project's configured lint, type, test, and build commands pass.

> **Final standard:** the interface should disappear behind the quality of the work—while still making visitors feel guided, confident, and ready to inquire.

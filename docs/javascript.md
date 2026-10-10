# JavaScript

All JavaScript on this site is vanilla: no frameworks, no external
libraries. There are no separate `.js` files. Most interactions live in a
`<script>` block before `</body>` on the page they belong to. The
documentation health check is the exception: it is rendered from
`_includes/partials/health-check.njk`, which both the homepage and the
audit page include.

## Homepage interactions

The interactions below live in the script block in `index.html`, listed in
the order they appear, except the documentation health check, which comes
from the shared include.

### Particle network

Renders an animated gold particle field on the hero section using the
HTML5 Canvas API.

| Property | Value |
| --- | --- |
| Element | `<canvas id="heroCanvas">` |
| Particle count | Calculated from canvas area (maximum 80) |
| Particle colour | `rgba(184,150,46, variable opacity)` |
| Connection distance | 120px. Particles within range are connected by a line |
| Mouse interaction | Particles repel from the cursor within a 150px radius |
| Performance | Pauses via `IntersectionObserver` when the hero is out of view |

### Cursor trail

Renders small gold particles that follow the cursor across the page.

| Property | Value |
| --- | --- |
| Element | Particles are appended directly to `document.body` |
| z-index | `9997`, below the command palette overlay (`9998`) and noise overlay (`9998`) |
| Particle size | 4px circle |
| Particle colour | `rgba(184,150,46, 0.6)` |
| Maximum particles | 15 active at once |
| Throttle | One particle every 30ms |
| Pointer events | `none`, so particles never block clicks |

### Scrolling gold strip

The strip below the hero is a pure CSS animation. There is no JavaScript
involved. It is documented here to prevent a maintainer from looking for
JavaScript that does not exist.

The animation works by duplicating the `strip-track` element in HTML so
the second copy begins exactly where the first ends. The CSS `stripScroll`
keyframe moves both copies left by 50% simultaneously, creating a seamless
loop. See `styles.css` for the `.strip-track` and `@keyframes stripScroll`
rules.

### Scroll progress bar

A gold bar at the top of the viewport that tracks scroll depth.

| Property | Value |
| --- | --- |
| Element | `<div id="progressBar">` |
| Trigger | `window scroll` event, passive listener |
| Calculation | `scrollTop / (scrollHeight - clientHeight) * 100` |

### Nav scroll state

The nav gains a `scrolled` class when the user scrolls more than 40px
from the top. This triggers a background and shadow change defined in
`styles.css`.

| Property | Value |
| --- | --- |
| Element | `<nav id="nav">` |
| Threshold | 40px from top |
| Class added | `scrolled` |

### Ambient orb animation

Three blurred circular gradients behind the social proof and CTA sections
animate on a continuous sine-wave path.

| Property | Value |
| --- | --- |
| Elements | `.ambient-orb` |
| Animation | `Math.sin` / `Math.cos` path, updates every frame via `requestAnimationFrame` |
| Performance | Runs continuously, not paused when out of view. Acceptable at current orb count (three per section). If orb count increases significantly, add `IntersectionObserver` pause logic matching the pattern used in the particle network. |

### Scroll reveal

Elements with the class `reveal` fade up into view as they enter the
viewport.

| Property | Value |
| --- | --- |
| Trigger class | `reveal` |
| Active class | `visible` |
| Mechanism | `IntersectionObserver`, threshold `0.1`, rootMargin `-40px` |
| Delay variants | `reveal-d1`, `reveal-d2`, `reveal-d3` (CSS animation delays) |
| Unobserves | Yes. Each element is unobserved after it becomes visible |

### Animated counters

Stat numbers count up from zero when they enter the viewport. Triggered
by the scroll reveal `IntersectionObserver`.

| Property | Value |
| --- | --- |
| Trigger attribute | `data-count` (target number) |
| Suffix attribute | `data-suffix`, appended after the number (e.g. `+`) |
| Duration | 900ms |
| Easing | Cubic ease-out |
| Runs once | Yes. The `data-animated` flag prevents re-triggering |

### Typewriter effect

Cycles through three documentation snippets in the hero code panel.

| Property | Value |
| --- | --- |
| Element | `<span id="twCode">` |
| Snippets | Three: docs strategy, audit dimensions, deliverables |
| Typing speed | 45ms per character |
| Delete speed | 20ms per character |
| Pause at end | 2800ms before deleting |
| Pause between | 400ms before typing the next snippet |

### Social proof carousel

Rotates three items in the hero side panel automatically.

| Property | Value |
| --- | --- |
| Elements | `.side-carousel-item` |
| Interval | 4000ms |
| Active class | `active` |
| Controls | Dot buttons. Clicking a dot pauses the timer and jumps to that item |

### Documentation health check widget

The most complex component on the site. A six-question scoring engine
that produces a personalised health report.

The widget's markup and script live in `_includes/partials/health-check.njk`.
The homepage and the audit page both include it, so they score identically.
The include takes one parameter, `bookingBlock`. The audit page sets it to
`true`: a booking block appears after the result, and the widget's own
**Book the audit** button is left out. The homepage sets it to `false`.

**States:**

| State | Description |
| --- | --- |
| Questions | Six questions displayed one at a time with a step indicator |
| Results | Score ring, category label, three dimension health bars, per-answer findings, weakest dimension summary |
| Reset | All state clears and returns to question one |

**Scoring:**

| Dimension | Questions |
| --- | --- |
| Accuracy | Q1, Q5 |
| Ownership | Q2, Q6 |
| Findability | Q3, Q4 |

Each answer carries a score of 0, 1, 2, 3, or 5. The total is expressed
as a percentage of the maximum possible score. Dimension scores are
averaged independently and displayed as health bars.

**Score categories:**

| Range | Label |
| --- | --- |
| 80–100% | Strong foundation |
| 60–79% | Room to improve |
| 40–59% | At risk |
| 0–39% | Needs urgent attention |

### Command palette

Opens with `⌘K` on Mac or `Ctrl+K` on Windows. Searches portfolio
pieces and navigation destinations.

| Property | Value |
| --- | --- |
| Trigger | `⌘K` / `Ctrl+K` or the search button in the nav |
| Close | `Escape` or clicking outside the panel |
| Items | Six: audit booking, health check, four portfolio pieces, email |
| Filter | Live text match on label and description |

### Hamburger navigation

Controls the mobile nav menu on all pages.

| Property | Value |
| --- | --- |
| Trigger element | `<button id="navHamburger">` |
| Toggle class | `open` on `#navLinks` and `#navHamburger` |
| Auto-close | On nav link click (50ms delay) and on outside click |
| Accessibility | `aria-expanded` toggled on the button |

### Smooth scroll

Intercepts all anchor clicks (`href` starting with `#`) and replaces
default browser scroll with a custom eased animation.

| Property | Value |
| --- | --- |
| Selector | `document.querySelectorAll('a[href^="#"]')` |
| Duration | 800ms |
| Easing | Quartic ease-out: `1 - Math.pow(1 - progress, 4)` |

### Writing samples tab switcher

Controls the four tabbed panels in the writing samples section.

| Property | Value |
| --- | --- |
| Trigger | `switchTab(btn, id)` called via `onclick` on each tab button |
| Active class | `active`, toggled on both the selected button and its panel |
| Transition | Controlled by CSS on `.sample-panel`. Panels without `active` are hidden |
| Default active | First tab (`panel-api`) has `active` class set in HTML on page load |
| Current panels | `panel-api`, `panel-start`, `panel-arch`, `panel-git` |

**To add a new tab:**

1. Add a button in the `.samples-tabs` div:
```html
<button class="samples-tab" onclick="switchTab(this,'your-id')">Tab Label</button>
```

2. Add the corresponding panel div after the last `.sample-panel`:
```html
<div class="sample-panel" id="panel-your-id">
  <!-- panel content here -->
</div>
```

3. Do not add `active` to the new button or panel. The default active
   state is set in HTML on the first tab only. The switcher handles
   everything else.

4. Add a row to the panels table above with the new panel ID.

## Adding a new interaction

1. Write the interaction as a self-contained function in the `<script>`
   block before `</body>` in `index.html`
2. Do not import external libraries. Keep all interactions in vanilla JS
3. Use `IntersectionObserver` for any animation that should pause when
   out of view
4. Add a row to the relevant table in this document describing the new
   interaction
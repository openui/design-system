# Open UI Global Design System Code Style Guidelines

This document outlines the Code Style guidelines for the components that are part of the Open UI Global Design System (OUI). 

- This is a living document and meant to reflect reality. When a question arises that is not covered, the guidelines should be updated with the new guidance.
- Code guidelines should make it *easier* to contribute, by reducing the number of arbitrary decisions a developer needs to make, while not being onerous to follow. This document tries to find that balance.
- When possible, these guidelines should be enforced through tooling. Otherwise, they are enforced through the PR approval process.

Additional guidelines will be needed for the tooling and apps that support the components, as well as for any
framework-specific implementations of OUI.

In addition to the criteria for inclusion outlined elsewhere, OUI follows these coding principles and conventions.

## OUI Implementations

### OUI Patterns
The primary implementation of the global design system will be HTML, CSS, and JavaScript code patterns that can be referenced (by humans and AI models), copied-and-pasted, and included in projects.

- **HTML** is surfaced as code snippets on an easy-to-browse website
- **CSS** are available as a consumable asset (akin to `https://cdn/bootstrap.min.css`) as well as surfaced on the website
- **Design tokens** are available as a customizable starter file, and the website showcases different themes (akin to CSS Zen Garden)

### Web Components implementations
An accompanying Web Component library is also in the works, which delivers the OUI pattern code as a consumable package that can be directly imported and used by web applications and libraries.

### Framework-specific implementations
OUI patterns can also be implemented in any other web-based framework. Framework-specific implementations can:
- **Reference/re-implement** the OUI pattern HTML, CSS, JS and marry that code with framework-specific conventions
- **Wrap Web Components** with adjustments needed to make the component usable in the specific framework.

These implementations are expected to have an API, naming, and output that aligns with the primary implementations.

## Design Principles
- **Accessibility is paramount** - People (and machines!) will copy-and-paste (as well as import through components) these patterns.
	- Therefore, any source code needs to embody accessibility best practices
	- There is a recognition that accessible patterns/components won't solve all problems
		- Components can be misused by consumers. The library can provide guidance but ultimately can't prevent people from misusing them.
		- The design token architecture provides for a lot of flexibility, which can also be misused by consumers (e.g. defining colors that don't have sufficient contrast). Again, the library can provide guidance but ultimately can't prevent people from misusing them.
- **Internationalization** - 
	- This is a global initiative
	- Accommodating different writing modes, translations, number/date/time formats, is critical
	- The library embodies best practices (e.g. using logical properties) to accommodate internationalized experiences
	- The library will consider various quirks (such as attributes, text nodes, and generated-content)
- **Privacy & security** - It is critical that any code associated with the OUI Global Design System to be private and secure.
- Pragmatism over idealism
	W3C standards work vs "this is a solid component library that serves 80/20 rule"
- **Rigor** - While this effort as rigorous as the full-blown W3C standards process, it still has wide/deep review by domain experts.
- Baseline Support
Technology choices (e.g. @layer) used by the pattern library should be
Sturdy, well-adopted, etc
- **A living source** - The library can provide sturdy foundations for today’s technology, and enhance the experience over time when emerging browser features become available
- **Curate, not invent** - This library curates and normalizes  _existing_ best practices established in existing design systems rather than inventing new solutions
- **Quality and Durability** - OUI code should be well-architected, intuitive, legible, readable, understandable, maintainable, and extensible.
	- **Legibility over succinctness** - 
	- **Avoid clever code & hacks** - 
	- **Extensibility** -

## Code style guidelines
The ambition of this effort in addition to the multi-dimensional delivery means that getting names

### Namespace

*TODO: Document namespace*

### Variants

*TODO: Add guidelines for color, size and other variants*

## HTML

### HTML principles

- **Use semantic markup.** That means using the `<button>` tag rather than `<div
  onclick="toggle()">` when a button is required, an `<a>` tag when a link is
  required, and so on.
- **Use native HTML elements** (e.g. `<input>`, `<select>`) should be preferred
  over custom elements whenever possible. Native elements provide a slew of
  functionality and accessibility best practices out of the box.

### HTML conventions

*TODO: Add HTML conventions*

## CSS

### CSS principles

- **Modular** - Modular CSS architecture is a best practice, is great for DX, is more matinainable, and helps avoid style collisions
  tightly scoped and to avoid unintended style bleeding.
- **Clarity over brevity** - CSS class naming conventions prioritize clarity, legibility, and resilience over succinctness and saving bytes
- **Limit specificity** - Overly-specific styles should be avoided for manageability, maintainability, and DX. 








------


## HTML Naming Conventions
- Using appropriate HTML tags is a given.
- TODO: populate HTML-specific naming conventions

## CSS Naming Conventions

### 1. Determine CSS selectors

Options: classes, data attributes, IDs (#yolo), other
Propose: CSS classes
Rationale: Standard convention

### 2. Determine CSS style/methodology

Options: BEM, BEMIT, OOCSS, SMACSS, ITCSS, SUIT CSS, CUBE CSS, RSCSS, Utility-first (Tailwind, Atomic)
Propose: Some BEM-style syntax
Rationale: Clarity over brevity. Hierarchical. At-a-glance. 
Example:

```
.alert

.alert--success

.alert--error

.alert__icon

.alert__body

```


### 3. Determine a global namespace

Options: `oui-` `www-` `web-` `w3c-`

Propose: 
Rationale: 

(note: It would be amazing to have something that hints at its global nature! `www`, `web` or `w3c` would be badass, but I also acknowledge those might be a more challenging sell)

###4. Determine component naming standard

Options: `oui-alert`, `oui-button-group`, `oui-c-alert`,
Propose: `oui-[component-name]`
Rationale: Feels generally clean

### 5. Determine variant names

#### 5a. Determine component state-based names
Code will use native pseudoselectors (e.g. `:hover`, `:focus-visible`, etc). However, there are other states to account for, in addition to artificially triggering a specific state of a component

Options:
- Modifier class: `button--hover`, `focus`, `active`, `disabled`  
- Modifier class with `is-`: `is-hovered`, `is-active`, `is-disabled`  
- Use attributes: `[disabled]`, `[aria-expanded="true"]` 

Propose:
Rationale:

#### 5b. Determine status variant names

Options: 
- BAD: `error`, `danger`, `critical`, `destructive`, `blocked`, `negative`
- GOOD: `success`, `valid`, `positive`, `complete`
- CAUTION: `caution`, `warning`, `
- INFO: `info`, `neutral`, `default`

Propose: `error`, `success`, `warning`, `info`
Rationale: Common convention across many design systems


5c: Sizing names

Options:
- `small`, `medium`, `large`, `extra-large`
- `sm`, `md`, `lg`, `xl`
- more

Propose:
Rationale:

5d: Spacing names

Options:
- `small`, `medium`, `large`, `extra-large`
- `sm`, `md`, `lg`, `xl`
- `4`, `8`, `12`, `16`, etc

Propose:
Rationale:

### 6. Component states
Options: 
- Pseudo-class names: hover, focus, active, disabled
- Boolean prefix: is-hovered, is-active
- ARIA/data attributes: [data-state="open"], [aria-invalid="true"]


### 6: Media query names/units

Note: this is weird as media queries don't support CSS custom properties. But it's probably good to have them as quasi-variables or potentially think about how to use Sass with them.

Options: 
- raw values `30rem`, `56rem`
- `desktop`, `tablet`, `mobile`
- `small`, `medium`, `large`, `extra-large`
- `sm`, `md`, `lg`, `xl`
- `bp-1`, `bp-2`, `bp-3`

Propose:
Rationale: 



### 7. Determine CSS declaration structure

Options: 

Structural

```
.oui-alert {
  /* Structural (hard-coded) styles */
  [positioning]
  [box model]
  [other]

  /* Themeable styles */
  [color]
  [typography]
  [border]
  [shadow]
  [animation]
  [other]
}
```

Alphabetical 

```
.oui-alert {
  align-content:
  ...
  z-index
}
```

Proposal:
Rationale:












## Credits

- https://vanilla-full.netlify.app/?path=/docs/documentation-guidelines--docs
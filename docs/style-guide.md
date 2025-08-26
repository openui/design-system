# Open UI Global Design System Component Code Style Guidelines

This document outlines the Code Style guidelines for the components that are
part of the Open UI Global Design System (OUI). Additional guidelines will be
needed for the tooling and apps that support the components, as well as for any
framework-specific implementations of OUI.

- This is a living document and meant to reflect reality. When a question arises
  that is not covered, the guidelines should be updated with the new guidance.
- Code guidelines should make it *easier* to contribute, by reducing the number
  of arbitrary decisions a developer needs to make, while not being onerous to
  follow. This document tries to find that balance.
- When possible, these guidelines should be enforced through tooling. Otherwise,
  they are enforced through the PR approval process.

In addition to the criteria for inclusion outlined elsewhere, OUI follows these
coding principles and conventions.

## OUI Implementations

The primary implementation of the global design system will be copyable
HTML/CSS/JS snippets that show a variety of states 

In the future, there will also be web component implementations, as well as
framework-specific implementations that either wrap or emulate a component, with
adjustments needed to make the component usable in React, Svelte, Vue, etc.
These implementations are expected to have an API and output that aligns with
the primary implementations.

## Code style guidelines

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

- **Portable** - The CSS architecture uses CSS classes for styling in order to
  ensure the CSS is portable across frameworks and web technologies.
- **Clarity over brevity** - CSS class naming conventions are verbose, but they
  deliver clarity, legibility, and resilience in exchange.
- **Modular** - Component styles are fully modular in order to keep things
  tightly scoped and to avoid unintended style bleeding.
- **Limit chaining and multiple selectors** - Chaining and descendant selectors
  should be avoided wherever possible in order to keep CSS as DOM-independent
  and modular as possible.

### CSS conventions

*TODO: Add class naming rules*

*TODO: Add property usage rules, for instance preference for logical properties*

## JavaScript

*TODO: Add JavaScript principles and conventions*

## Credits

- https://vanilla-full.netlify.app/?path=/docs/documentation-guidelines--docs
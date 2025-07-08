# Open UI Global Design System Component API Guidelines

This document outlines the API guidelines for the components that are part of
the Open UI Global Design System (OUI). Additional guidelines will be needed for
the tooling and apps that support the components, as well as for any
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

## OUI principles

The primary implementation of the global design system are built as web
components. There will also be secondary implementations of the components.

There will be copyable HTML/CSS/JS snippets that represent a component's output
with predefined attributes, for instance a "Success Badge" or "Primary Button". 

There will also be framework-specific implementations that either wrap or
emulate a component, with adjustments needed to make the component usable in
React, Svelte, Vue, etc. These implementations are expected to have an API and
output that aligns with the primary implementations.

The OUI components follow these guidelines:

- **Agnostic** - OUI components are free of any framework, CMS, or
  implementation-specific conventions. These are standalone presentational UI
  components that aim to share an interface across frameworks. Any framework,
  CMS, or implementation-specific requirements should be minimized and scoped to
  that implementation.
  - For example, a Svelte implementation will have `onclick`, React will have
    `onClick`, and Vue will have `@click`, but they all include `click`. This
    would also be true for a custom event name and for attribute names.
- **Predictable APIs** - OUI provides consistent, clear component APIs in order to
  provide a smooth user developer experience.
- **Composition over inheritance** - OUI adheres to the composition over
  inheritance principle in order to create clean, extensible components that
  aren't tied to specific contexts or content.

## API guidelines

### Component API naming conventions

OUI provides attributes that serve as the API for user developers to interface
with OUI components. For example:

```html
<oui-button text="Click me" iconName="arrow-right" iconPosition="after"></oui-button>
```

In the above example, `text`, `iconName`, and `iconPosition` are attributes that
can accept certain values in order to render the desired UI element.

Authoring a consistent API language provides many benefits:

- **More efficient development** - Because the API language is consistent across
  components, user developers can spend more time coding rather than reading API
  documentation. Library contributors don't have to think as much about
  component API naming either.
-  **Shared vocuabulary between designers and developers** - When the code
   library and design library use the same language, designers and developers
   can spend more time collaborating rather than futzing over what things are
   named. This improves team velocity and product quality. It also positions the
   team to benefit from future tooling that can bring design and code closer
   together (something many startups and plugins are trying to solve right now!)
- **Future changes** - Utilizing a consistent language means that future changes
  and improvements are as easy as find-and-replace.

The library adhreres to the following API naming conventions:

#### Component names

The component names are prefixed with `oui-`, followed by the component name,
e.g. `oui-badge`.

#### Variants

- `variant` should be used for primary *stylistic* variations of a component,
  such as (e.g. `variant="primary"` or `variant="success"`). variant should be
  used as the primary variable used to manipulate the component style.
- `inverted` should be used consistently for stylistic variations that "invert"
  the color schemes (e.g. <oui-heading inverted=true>) to work on a darker
  background. Note: this is different than dark/light mode support, which is
  handled elsewhere.
- `size` should be used for adjusting size attributes (e.g. `size="sm"` or
  `size="lg"`). Default to `sm`, `lg`, `xl` with `md` being the undeclared
  default. Note: use abbreviated t-shirt sizes:
  - `sm` = Small
  - `xs` = Extra small
  - `md` = Medium
  - `md2` = Another Medium Value
  - `lg` = Large
  - `xl` = Extra large
  - `xxl` = Extra, extra large

- `spacing` should be used for adjusting spacing between elements (e.g.
  `spacing="condensed"`).
- `behavior` should be used for functional variations of a pattern, such as
  <oui-alert behavior="dismissible">. behavior should be used as the default for
  introducing a functional variant to a component, and should be used for
  mutually exclusive behaviors.
- `is[Behavior]` should be used in conjunction with behavior to add additional
  behavioral variants to a component (e.g. `<oui-alert behavior="dismissible"
  isDraggable="true" isFadable="true">`). `is[Behavior]` should be the default
  convention, but sometimes deviating from the is language is necessary (for
  instance, `<oui-accordion allowMultipleOpen="true">`). Whatever the language,
  the name should be clear to the user whether they're toggling something on or
  off.
- `align` should be used for aligning content, and should include `left`,
  `center`, `right` if needed.
- `verticalAlign` should be used for aligning content vertically, and should
  include `top`, `center`, `bottom`.

### Text, Labels, Titles

- Default to text for strings of text (e.g. `<oui-badge text="Badge Text">`).
- Default to title for headings, such as `<oui-hero title="Hero Title">`.
- Use description for non-heading text that accompanies a component, such as
  `<oui-hero title="Hero Title" description="This is accompanying text for the
  hero">`.
- For form-related components, use the semantic label or legend, such as
  `<oui-text-field label="First Name">`.

### Tag name

If a component can be rendered as different html elements (e.g. `h1`, `h2`,
`h3`, etc), name the prop `tagName`.

### Media

- `imgSrc` for passing in an image source (e.g. `<oui-hero
  imgSrc="path/to/image.jpg">`)
- `imgAlt` for image alt text (e.g. `<oui-hero imgSrc="path/to/image.jpg"
  imgAlt="A smiling stock broker looking at a laptop computer">`)
- `iconName` for icon name (e.g. `<oui-button iconName="arrow-right">`)
- `iconPosition` for controling the position of an icon (e.g. `<oui-button
  iconName="search" iconPosition="before" text="Search">`)

### Composability

#### Compound components

Certain components (such as an accordion are card) are composed of multiple
smaller subcomponents. Compound components either require multiple components to
function correctly (e.g. an accordion and accordion itmem), or require multiple
components to be composible and flexible (such as a card with a card header, a
card body, and card footer subcomponents).

An example of a compound component:

```html
<oui-tabs>
  <oui-tab href="tab-1" title="Tab 1">
    <!-- Tab 1 content -->
  </oui-tab>
  <oui-tab href="tab-2" title="Tab 2">
    <!-- Tab 2 content -->
  </oui-tab>
</oui-tabs>
```

- Compound components are composed of a parent component (e.g. card) and
  children component (e.g. card header and card footer).
- Compound component children names must always begin with the parent name. A
  parent component `oui-table` means that all child components related to it
  must begin with `oui-table` (such as `oui-table-body` and `oui-table-cell`).
- Compound components should generally follow a component and component-item
  pattern (e.g. `oui-accordion` and `oui-accordion-item` or `oui-breadcrumbs`
  and `oui-breadcrumbs-item`).
- Some composable compound components (like modal or card) should use a header,
  body, footer convention (e.g. `oui-card` would have `oui-card-header`,
  `oui-card-body`, and `oui-card-footer`) to serve as discrete sections.
- Compound component children are not usable outside their parent.

#### Slots

Content that is displayed to users can be passed as an attribute or in a slot.

- A default slot should only be used for the primary content displayed by a
  component.
- Use slots when rich text is supported.
- Don't support both an attribute and a slot for the same content.
- Avoid having some content in an attribute, and some content in a slot.

## HTML

### HTML principles and conventions

- **Use semantic markup.** That means using the `<button>` tag rather than `<div
  onclick="toggle()">` when a button is required, an `<a>` tag when a link is
  required, and so on.
- **Clarity over brevity.** Developers should be able to understand what's going
  on with markup at a glance. Avoid cryptic abbreviations and nicknames, add
  proper indenting & spacing, and use clear comments.
- **Native HTML elements** (e.g. `<input>`, `<select>`) should be preferred over
  custom elements whenever possible. Native elements provide a slew of
  functionality and accessibility best practices out of the box.

## CSS

### CSS design principles

- **Portable** - The CSS architecture uses CSS classes for styling (versus CSS-in-JS
  tooling) in order to ensure the CSS is portable across frameworks and web
  technologies.
- **Clarity over brevity** - CSS class naming conventions are verbose, but they
  deliver clarity, legibility, and resilience in exchange.
- **Modular** - Component styles are fully modular in order to keep things tightly
  scoped and to avoid unintended style bleeding.
- **Limit chaining and multiple selectors** - Chaining and descendant selectors
  should be avoided wherever possible in order to keep CSS as DOM-independent
  and modular as possible.

### CSS conventions

OUI follows a [BEM](http://getbem.com/introduction/)-like syntax, extending it
further to follow more of
[BEMIT](http://csswizardry.com/2015/08/bemit-taking-the-bem-naming-convention-a-step-further/)-like
conventions.


#### BEM syntax

BEM stands for "Block Element Modifier". Here's a breakdown of what that means:

- **Block** is the primary component block (e.g. .oui-c-button)
- **Element** is a child of the primary block (e.g. .oui-c-button__text)
- **Modifier** is a variation of a component style (e.g. .oui-c-button--secondary)

OUI extends BEM's conventions to create even more explicit, encapsulated class
names.

#### Global namespace

OUI uses a global namespace of `oui-` prefix to all styles that come from the
design system. This is done to:

  - Avoid naming collisions with code coming from other sources
  - Clarify the source of the code, distinguishing OUI markup/styles from code
    coming from other codebases and libraries.

### Class prefixes

In addition to the global `oui-` namespace, OUI uses class prefixes to provide
additional clarity to the job a given class plays. OUI uses the following class
prefix conventions:

- **c** - for UI components, such as `.oui-c-button`
- **l** - for layout-specific component styles, such as `.oui-l-container`
- **u** - for utilities, such as `.oui-u-margin-bottom-none`
- **is** - and has- for specific states, such as `.oui-is-active`

### Logical properties

Use logical properties (`inset-block-start`, `margin-inline`) over physical
properties (`top`, `margin-left`), to allow the components to be used in
different writing systems.

## JavaScript

### Events and methods

Native events and methods (and events and methods with native equivalents), like
`click`, `input` or `change`, are emitted as-is. 

```js
const dateInput = document.querySelector('oui-date-input');
dateInput.addEventListener('input', (event)=>{
  console.log(event.target.value);
});
dateInput.showPicker();
```

Events that are novel, such as a "tab change" event, bubble up, and are named in
the format `oui-[action]`. Methods do not have a prefix.

```js
const tabElement = document.querySelector('oui-tabs');
tabElement.addEventListener('oui-change', (event)=>{
  console.log(event.target.value)
});
tabElement.show('#tab-1')
```

## Credits

- https://vanilla-full.netlify.app/?path=/docs/documentation-guidelines--docs
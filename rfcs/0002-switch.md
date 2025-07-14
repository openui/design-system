- Start Date: 2025-03-25
- RFC PR: (Leave empty till PR Created)

# Summary

A control used to switch between two states: often on or off.[^1]

# Basic Example

A very basic web component implementation could look something like in this codepen https://codepen.io/tuelsch/pen/wBvmvVB.

```html
<!-- Basic -->
<oui-switch></oui-switch>

<!-- With label -->
<label for="wifi">Wifi</label>
<oui-switch id="wifi"></oui-switch>

<!-- Initially checked -->
<oui-switch checked></oui-switch>

<!-- Disabled -->
<oui-switch disabled></oui-switch>

<!-- Readonly -->
<oui-switch readonly></oui-switch>

<!-- Participating in form validation -->
<oui-switch required></oui-switch>

<!-- With content on the thumb -->
<oui-switch>🚀</oui-switch>

<!-- With content on the track -->
<oui-switch>
  <span slot="inactive-track" aria-label="off">❌</span>
  <span slot="active-track" aria-label="on">✔️</span>
</oui-switch>
```

# Motivation

The switch or toggle component is widely used and implemented in Design Systems. There is a [switch explainer](https://open-ui.org/components/switch.explainer/) on Open UI, a [switch proposal at WHATWG](https://github.com/whatwg/html/pull/9546) ([original switch issue at WHATWG](https://github.com/whatwg/html/issues/4180)) and an implementation thereof in Safari ([article by Dave Rupert on Frontend Masters about input type switch](https://frontendmasters.com/blog/safari-gets-a-toggle-switch-input/)).

While Safari is implementing the backwards compatible `<input type="checkbox" switch />` attribute, other browsers are lacking support. The explainer on Open UI is also differing in the anatomy of the switch implementation. While the explainer allows nesting of elements for track and thumb with the possibility to add custom content to these elements, the switch proposal at WHATWG uses pseudo-elements for styling thumb and track, limiting the addition of custom content to CSS.

Implementing a switch web component for the Open UI Design System allows an implementation that does not need to be backwards compatible and works consistently across browsers until the WHATWG proposal (or something else) is safe to use.

<!--Why are you proposing this? What use cases does it support? What are your expected outcomes.

Please focus on explaining the motivation so that if this RFC is not accepted, the motivation could be used to develop an alternative solution. In other words, enumerate the constraints you are trying to solve without coupling them too closely to the solution you have in mind.-->

# Detailed Proposal

<!-- This is the bulk of the RFC. Explain the component and the design in enough detail for someone familiar with design systems and web components can understand, and someone familiar with the implementation help to implement it. This should get into as many specifics as possible, outline any edge cases or extra consideration, and include examples of how it can be used. Any new terminology should also be defined here.

It's important to ensure your proposal address the key goals of the OpenUI Design System to create a component that is:

- User Friendly
- Accessible
- Maintainable
- Internationalization ready -->

The `oui-switch` component will provide a fully styleable switch component accepting content through various slots.

## Anatomy

A switch consists of a wrapper element, a two sided track and a thumb. Each track side and the thumb can have optional content, usually an icon helping users understand the current state of the switch.

![Switch Anatomy](https://open-ui.org/images/switch-moving-track-anatomy.png)

## API

### Properties

| Property Name | Attribute Name | Type      | Default Value | Description                                                                  |
| ------------- | -------------- | --------- | ------------- | ---------------------------------------------------------------------------- |
| `checked`     | `checked`      | `boolean` | `false`       | Indicates if the initial state should be "on" initially.                     |
| `value`       | `value`        | `string`  | `"off"`       | The current value of the switch.                                             |
| `name`        | `name`         | `string`  | `""`          | The name of the component.                                                   |
| `id`          | `id`           | `string`  | `""`          | The unique identifier of the component.                                      |
| `disabled`    | `disabled`     | `boolean` | `false`       | Indicates that the switch is in a disabled state.                            |
| `autofocus`   | `autofocus`    | `boolean` | `false`       | Get focus by default.                                                        |
| `required`    | `required`     | `boolean` | `false`       | Indicates that the switch is invalid unless on.                              |
| `form`        | `form`         | `string`  | `""`          | Associates the element with a form in the document whose `id` is this value. |

### Slots

| Slot             | Description                                             |
| ---------------- | ------------------------------------------------------- |
| `default`        | The content of the thumb (text or markup)               |
| `active-track`   | The content of the active track side (text or markup)   |
| `inactive-track` | The content of the inactive track side (text or markup) |

### Events

| Event Name | Detail Type | Bubbles | Composed | Cancellable | Dispatch Behavior                                      |
| ---------- | ----------- | ------- | -------- | ----------- | ------------------------------------------------------ |
| `change`   | none        | `true`  | `true`   | `false`     | Fired when the switch `value` changes.                 |
| `input`    | none        | `true`  | `true`   | `false`     | Fired when the switch `value` is commited by the user. |

### CSS Parts

| Part    | Description                                              |
| ------- | -------------------------------------------------------- |
| `track` | Used to style the track as a whole, e.g. for animations. |
| `thumb` | Easy access to overriding thumb styles.                  |

### CSS Custom Properties

Assigned values are exemplary and should ideally reference core or semantic tokens.

```css
:root {
  /* Size and spacing */
  --oui-switch-height: 1em;
  --oui-switch-width: 2em; /* or calc(var(--oui-switch-height) * 2) ? */
  --oui-switch-border-radius: 9999px;
  --oui-switch-border: 1px solid black;
  --oui-switch-overflow: hidden;

  /* Thumb */
  --oui-switch-thumb-width: 1em;
  --oui-switch-thumb-height: 1em;
  --oui-switch-thumb-offset: 0px; /* If thumb is bigger/smaller than the switch */
  --oui-switch-thumb-border-radius: 9999px;
  --oui-switch-thumb-background-color: gray;
  --oui-switch-thumb-foreground-coolor: black;
  --oui-switch-thumb-border: 1px solid black;

  /* Track */
  --oui-switch-track-background-inactive: lightgray;
  --oui-switch-track-foreground-inactive: black;
  --oui-switch-track-background-active: limegreen;
  --oui-switch-track-foreground-inactive: black;
  --oui-switch-track-border: none; /* If switch overflow is not hidden */
  --oui-switch-track-border-radius: 0;
}
```

### Behavior

A switch is used to toggle a binary state, e.g. turn light mode, autosave or Wifi on or off. A switch should not be used to toggle between opposing states, e.g. either activating light mode or activating dark mode. [^2]

A switch is a form associated component and can participate in form validation. It is focusable and shares common states like `disabled`, `readonly` and `autofocus` with other form controls. Users should be able to use the switch with existing knowledge of form elements.

#### Keyboard navigation

| Key              | Description                            |
| ---------------- | -------------------------------------- |
| Space            | Should toggle the switch when focused. |
| Enter (optional) | Should toggle the switch when focused. |

More info: https://open-ui.org/components/switch.explainer/#behavior

### Accessibility considerations

The switch can be associated with the existing `role="switch"`.

More detailed info: https://open-ui.org/components/switch.explainer/#accessibility

### Internationalisation

The default active state thumb position changes based on writing mode and direction.

## Use cases

1. **Settings page**: popularised by Android and iOS, switches can be used to toggle a setting
2. **Autosave**: Switches are a popular way of turning autosave on or off in Office 365
3. **Dark mode**: Switches can be used to toggle dark mode

## Edge cases

Some edge case examples are highlighted in the [Open UI switch explainer](https://open-ui.org/components/switch.explainer/#anatomy).

1. **Long slotted content**: All switch slots usually just fit one icon or character. Slotting whole words could create overflow issues or deform the switch to make it harder to recognise for users.
2. **Small thumb**: Depending on track size and slotted content, the thumb could be too small to cover the currently hidden track side.

# Drawbacks

There already is a proposal and an existing implementation by Safari. By the time this proposal is implemented and adopted, `<input type="checkbox" switch />` might be available across browsers.

Most Design Systems already have a switch and using the Open UI one might be more work than just continue to use what's already there. However, the implementation details vary greatly (sometimes switches are built on top of buttons, sometimes on checkboxes, sometimes on divs) and accessibility is not guaranteed.

A web components API cannot come close enough to what browsers can do in terms of providing fallbacks, using existing elements, pseudo-elements, pseudo-states or capabilities of new HTML elements. An implementation by Open UI will differ from a standards implementation and a migration will not be straight forward.

# Alternatives

<!-- What other designs or features have been considered? What is the impact of this not being included? Does this solution already exist within OpenUI, if so what makes this solution different? -->

A checkbox offers almost the same functionality as a switch.

# Adoption Strategy

<!-- If we implement this proposal or feature, how will existing users of OpenUI's Design System adopt it? Is it a breaking change to an existing component? Should there be any coordination with other libraries or communities?-->

This is a new feature.

# How we teach this

<!-- What names and terminology work best for these concepts and why? How is this idea best presented? As a continuation of existing OpenUI Design System patterns?

Would the acceptance of this proposal mean the OpenUI Design System documentation must be re-organized or altered? Does it change how the OpenUI Design System is taught to new developers at any level?

How should this feature be taught to existing OpenUI Design System developers? -->

To be defined.

# Unresolved questions

<!--Optional, but suggested for first drafts. What parts of the design are still TBD? -->

- Should the implementation be aligned closer with the explainer from Open UI by providing slots for declarative content or with the proposal from WHATWG and focus on providing parts (as a replacement for pseudo-elements)?
- Should switch dimensions be calculated based on the height and a height/width ratio or should each property be set individually?
- There are mainly two different ways switches are animated. The first moves the track along with the thumb to reveal the active/inactive side, the second just moves the thumb over a static track while the background color of the track changes. Thumb size is a relevant property to make the first animation work. The first option is closer to a physical switch, the second easier to implement and more flexible. Which should be the default?

[^1]: https://component.gallery/components/toggle/
[^2]: https://open-ui.org/components/switch.explainer/#non-goals

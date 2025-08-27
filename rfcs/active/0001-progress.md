* Start Date: 2025-02-24
* RFC PR: (Leave empty till PR Created)

## Summary

This RFC proposes the addition of a Progress component to the Open UI Design System. Progress components are used to represent the completion status of a task or process.

# Basic Example

```html
<!-- Determinate Example -->
<label for="progress">Example Label:</label>
<oui-progress id="progress" value="20" max="100"></oui-progress>

<!-- Indeterminate Example -->
<label for="indeterminate-progress">Example Label:</label>
<oui-progress id="indeterminate-progress"></oui-progress>
```

# Motivation

Progress indicators are a common UI pattern used to communicate the status of a task or process to users. By providing a Progress component in the Open UI Design System, we can ensure a consistent and accessible implementation across applications.

# Detailed Proposal

The `oui-progress` component will provide a versatile, accessible, and themable implementation of progress indicators. The component will support both determinate and indeterminate modes.

## API

This component will be form associated so it can be labeled by a `<label>` element.

### CSS States

| State | Description |
|-------|-------------|
| `indeterminate` | The progress bar is in an indeterminate state. |

### CSS Parts

| Part    | Description                                |
|---------|--------------------------------------------|
| `track` | The track for the progress bar.            |
| `fill`  | The filled in portion of the progress bar. |

### Properties

| Property | Type | Default | Readonly | Description |
|----------|------|---------|-------------|
| `value`  | Number | `0` | false | The current progress value. |
| `max`    | Number | `100` | false |The maximum progress value. |
| `position` | Number | `-1` | true | The current position of the progress bar. |

### Attributes

| Property | Description |
|----------|------|---------|-------------|
| `value`  | The current progress value. |
| `max`    | The maximum progress value. |

### Slots

| Slot | Description                                                       |
|------|-------------------------------------------------------------------|
| `default` | Fallback text to render if the component otherwise fails to load. |

### Events

None

## Accessibility

The `oui-progress` component will be exposed using the `progressbar` role.

The min (always 0) and max values will be exposed via `aria-valuemin` and `aria-valuemax` values (respectively).
The current value will be exposed via `aria-valuenow`.
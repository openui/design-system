* Start Date: 2025-02-24
* RFC PR: (Leave empty till PR Created)

# Summary

This RFC proposes the addition of a Badge component to the OpenUI Design System. Badges are small, visually distinct elements used to display counts, status indicators, or short labels. They're commonly used in interfaces to highlight new content, show notification counts, indicate status, and provide visual cues for users. Badges typically appear in proximity to notifications or user avatars with eye-catching appeal, helping users quickly identify important information.

# Basic Example

```html
<!-- Basic badge -->
<oui-badge>New</oui-badge>

<!-- Badge with variant -->
<oui-badge variant="primary">4</oui-badge>

<!-- Pill badge -->
<oui-badge shape="pill">New</oui-badge>

<!-- Badge in context with another element -->
<h2>Product Features <oui-badge>New</oui-badge></h2>

<!-- Badge as a counter -->
<oui-button>
  Notifications
  <oui-badge variant="secondary">4</oui-badge>
</oui-button>

<!-- Positioned badge (for notification indicators) -->
<oui-button>
  Inbox
  <oui-badge position="top-end" variant="danger">99+</oui-badge>
</oui-button>

<!-- Dot badge (for status indicators) -->
<oui-badge dot aria-label="New notifications"></oui-badge>

<!-- Status badge -->
<oui-badge status="success">Success</oui-badge>

<!-- Badge with custom color -->
<oui-badge color="#52c41a">Custom</oui-badge>

<!-- Badge with overflow count -->
<oui-badge count="125" overflow-count="99"></oui-badge>

<!-- Standalone ribbon badge -->
<oui-badge.ribbon text="Ribbon" placement="end">
  <div style="width: 300px; height: 100px; background: #f0f0f0;"></div>
</oui-badge.ribbon>
```

# Motivation

Badges are a fundamental UI pattern found in many digital interfaces across various platforms. They serve several key purposes:

1. **Information density** - Badges allow developers to display additional information (counts, status, labels) in a compact space.
2. **Visual indication** - They provide immediate visual cues to users about state, notifications, or important updates.
3. **Context enhancement** - They enhance other components by providing supplementary information (counters, status indicators).

The OpenUI Design System aims to provide a comprehensive set of common UI components, and badges represent a widely-used pattern that fits within this mission. Adding a standardized badge component would reduce duplicative effort in rebuilding this common UI pattern across different applications and frameworks.

# Detailed Proposal

The `oui-badge` component will provide a versatile, accessible, and themeable implementation of the badge pattern.

## API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `variant` | `'primary' \| 'secondary' \| 'success' \| 'danger' \| 'warning' \| 'info'` | `'primary'` | Determines the visual style of the badge |
| `shape` | `'default' \| 'pill'` | `'default'` | Controls the border-radius of the badge |
| `position` | `null \| 'top-start' \| 'top-end' \| 'bottom-start' \| 'bottom-end'` | `null` | When used with a parent element, positions the badge accordingly |
| `visible` | `boolean` | `true` | Controls whether the badge is displayed |
| `aria-label` | `string` | `null` | Accessible label (required when badge only contains numbers or non-descriptive content) |
| `color` | `string` | `null` | Custom color for the badge (hex, rgb, or named color) |
| `count` | `number \| string` | `null` | Number or content to show in the badge |
| `overflow-count` | `number` | `99` | Maximum count to show before using the overflow indicator (e.g., "99+") |
| `dot` | `boolean` | `false` | Whether to display a small dot instead of content |
| `offset` | `[number, number]` | `[0, 0]` | Offset of the badge [x, y] in pixels |
| `size` | `'default' \| 'small'` | `'default'` | Size of the badge |
| `status` | `'success' \| 'processing' \| 'default' \| 'error' \| 'warning'` | `null` | Status indicator type |
| `show-zero` | `boolean` | `false` | Whether to show the badge when count is zero |
| `clickable` | `boolean` | `false` | Whether the badge is clickable |
| `title` | `string` | `null` | Text to show when hovering over the badge |

### Slots

| Slot | Description |
|------|-------------|
| `default` | The content of the badge (text or markup) |
| `count` | Alternative slot for badge content/count |

### Events

| Event | Description |
|-------|-------------|
| `click` | Fired when the badge is clicked (if `clickable` is true) |

### Composition

The Badge component will include a subcomponent called `oui-badge.ribbon` for the ribbon variant:

#### oui-badge.ribbon Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `text` | `string` | `null` | Content inside the ribbon |
| `color` | `string` | `null` | Custom color for the ribbon |
| `placement` | `'start' \| 'end'` | `'end'` | Placement of the ribbon (follows text direction) |

### CSS Custom Properties

The badge component will expose the following CSS custom properties for theming:

```css
:host {
  /* Size and spacing */
  --oui-badge-font-size: 0.75em;
  --oui-badge-font-weight: 700;
  --oui-badge-line-height: 1;
  --oui-badge-padding-x: 0.65em;
  --oui-badge-padding-y: 0.35em;
  --oui-badge-border-radius: 0.25rem;
  --oui-badge-pill-border-radius: 50rem; /* Used when shape="pill" */
  --oui-badge-dot-size: 0.5rem;
  --oui-badge-z-index: 10;
  --oui-badge-offset-x: 0;
  --oui-badge-offset-y: 0;

  /* Color tokens - should use design system global tokens */
  --oui-badge-color-primary-bg: var(--oui-color-primary, #0066cc);
  --oui-badge-color-primary-text: var(--oui-color-primary-contrast, #ffffff);
  --oui-badge-color-secondary-bg: var(--oui-color-secondary, #6c757d);
  --oui-badge-color-secondary-text: var(--oui-color-secondary-contrast, #ffffff);
  --oui-badge-color-success-bg: var(--oui-color-success, #198754);
  --oui-badge-color-success-text: var(--oui-color-success-contrast, #ffffff);
  --oui-badge-color-danger-bg: var(--oui-color-danger, #dc3545);
  --oui-badge-color-danger-text: var(--oui-color-danger-contrast, #ffffff);
  --oui-badge-color-warning-bg: var(--oui-color-warning, #ffc107);
  --oui-badge-color-warning-text: var(--oui-color-warning-contrast, #000000);
  --oui-badge-color-info-bg: var(--oui-color-info, #0dcaf0);
  --oui-badge-color-info-text: var(--oui-color-info-contrast, #000000);

  /* Status indicators */
  --oui-badge-color-status-success: var(--oui-color-success, #52c41a);
  --oui-badge-color-status-processing: var(--oui-color-info, #1890ff);
  --oui-badge-color-status-default: var(--oui-color-secondary, #d9d9d9);
  --oui-badge-color-status-error: var(--oui-color-danger, #ff4d4f);
  --oui-badge-color-status-warning: var(--oui-color-warning, #faad14);

  /* Ribbon specific */
  --oui-badge-ribbon-height: 1.5rem;
  --oui-badge-ribbon-padding-x: 0.5rem;
  --oui-badge-ribbon-corner-size: 0.5rem;
}
```

## Behavior

### Sizing and Positioning

Badges should automatically scale to match the size of the parent element when used inline (e.g., with headings or buttons). This will be achieved through using relative font sizes (`em` units).

When the `position` attribute is used, the badge will be absolutely positioned relative to its parent container, which should have `position: relative` applied.

### Accessibility Considerations

1. **Color contrast**: All badge color variants must meet WCAG 2.1 AA contrast requirements.
2. **Screen readers**:
   - When a badge contains only a number (e.g., "4" for notifications), an `aria-label` should be provided to give context (e.g., "4 unread messages").
   - When positioned badges are used as status indicators without text, `aria-label` must be provided.
3. **Focus**: Badges themselves are not focusable elements unless they function as interactive elements.
4. **Internationalization**:
   - Badge text should be translatable
   - The component should support RTL languages, which affects positioning variants

## Use Cases

1. **Notification indicators**: Showing counts of unread messages, notifications, etc.
2. **Status indicators**: Displaying the state of an item (new, updated, deprecated, success, error)
3. **Categorization**: Labeling content with categories or tags
4. **Highlighting**: Drawing attention to new features or content
5. **Numeric counters**: Displaying metrics, scores, or numerical values
6. **Progress indicators**: Showing steps in a multi-step process (e.g., "1 of 3")
7. **Dot indicators**: Small visual cues to indicate status without textual content
8. **Ribbons**: Corner labels or banners to highlight special status or promotions
9. **Standalone badges**: Used independently of other components to convey information
10. **Interactive badges**: Clickable elements that trigger actions or reveal additional information

## Edge Cases

1. **Long text**: The badge should truncate or wrap text that is too long
2. **Empty badges**: Badges with no content should not be rendered (unless `dot` is true)
3. **Badges with icons**: Should support icons with proper alignment and spacing
4. **Parent context**: When positioned, badges should be aware of parent boundaries
5. **Overflow handling**: For numeric counters, implement proper overflow handling with `overflow-count` property
6. **Zero value handling**: Provide option to show or hide zero values with `show-zero` property
7. **Automatic text color calculation**: Automatically calculate appropriate text color based on background color for optimal contrast
8. **RTL language support**: Badge positioning and ribbon placement should respect text direction
9. **Multiple badges**: Define spacing and alignment behavior when multiple badges are used together
10. **Animated badges**: Support for smooth transitions when badge content changes
11. **Processing/loading state**: Support for badges that indicate a processing state
12. **Badge inside other components**: Ensure badges work consistently when nested inside buttons, headers, navigation items, etc.

# Drawbacks

1. **Implementation complexity**:
   - Ensuring proper positioning relative to various parent elements can be challenging
   - Supporting different content types (text, numbers, icons) while maintaining consistent visual appearance

2. **Accessibility concerns**:
   - Badges that are purely visual indicators may need additional context for screen reader users
   - Color-based status indicators must provide alternative means of conveying status

3. **Potential for misuse**:
   - Overuse of badges can lead to visual clutter and overwhelm users
   - If too many badges use attention-grabbing colors (e.g., red), they may lose their impact

4. **Styling challenges**:
   - Ensuring badges look appropriate with different parent components
   - Maintaining consistent appearance across frameworks and styling approaches

# Alternatives

1. **Use existing HTML elements**: Developers could use `<span>` elements with custom CSS classes to create badges. However, this approach lacks standardization, accessibility features, and would require duplicate implementation efforts.

2. **Framework-specific solutions**: Many UI frameworks already provide badge components, but they're not interoperable and often tied to specific styling systems.

3. **CSS-only approach**: A set of CSS utilities could be provided instead of a component, but this would place more burden on developers to ensure proper markup and accessibility.

4. **More specialized components**: Instead of a general badge component, we could create more specific components (NotificationCounter, StatusIndicator, etc.). However, this would increase the complexity of the design system and potentially lead to redundant code.

# Adoption Strategy

The badge component is not a breaking change, as it introduces a new component rather than modifying existing ones. Adoption should be straightforward for new projects.

For existing OpenUI Design System users, we should:

1. Provide comprehensive documentation with examples
2. Ensure the badge component works well with other OpenUI components
3. Show clear migration paths from common badge implementations in popular frameworks

Coordination with other libraries or communities:
- Engage with existing design systems (like Bootstrap, Material, Ant Design) to understand their badge implementations
- Consider the patterns used in popular frameworks to ensure our API feels familiar to developers

# How we teach this

The badge component should be taught as a simple but versatile UI element that enhances information display throughout an application.

## Terminology

- "Badge" is the most widely recognized term for this component across frameworks and design systems, making it the natural choice for naming.
- We should distinguish between different use cases in our documentation:
  - "Counter badges" for numeric indicators
  - "Status badges" for state indicators
  - "Dot badges" for minimal visual indicators
  - "Pill badges" for the rounded visual variant
  - "Ribbon badges" for the corner/edge style variants

## Documentation Organization

The documentation should be organized to show:

1. Basic usage
2. Variants and styling options
   - Color variants
   - Size variants
   - Shape variants (default, pill)
   - Status indicators
   - Dot indicators
   - Ribbon badges
3. Positioning options
   - Standalone badges
   - Badges with headings
   - Badges with buttons/inputs
   - Positioned badges (top-end, etc.)
   - Offset customization
4. Content handling
   - Text content
   - Numeric content
   - Overflow handling
   - Zero handling
5. Accessibility considerations
   - Proper labeling
   - Color contrast
   - Screen reader support
6. Customization
   - Theming with CSS custom properties
   - Custom colors
   - Integration with design tokens
7. Advanced usage
   - Interactive badges
   - Badge groups
   - Internationalization
   - RTL support

## Best Practices Guidelines

1. **Context is key**: Always provide meaningful context for badges, especially when used as numerical indicators
2. **Consistent placement**: Maintain consistent badge placement across similar components
3. **Color meaning**: Use colors consistently to convey specific meanings (e.g., red for alerts/errors)
4. **Limit quantity**: Avoid overwhelming users with too many badges on screen
5. **Appropriate contrast**: Ensure sufficient contrast between badge and its background
6. **Accessibility first**: Always include proper aria-labels, especially for dot badges or numeric indicators

## Teaching Developers

For new developers:
- Present badges as a standard UI pattern with clear use cases
- Provide visual examples showing appropriate and inappropriate uses
- Emphasize accessibility requirements for different badge types

For existing OpenUI Design System developers:
- Emphasize how badges complement and enhance existing components
- Show examples of common patterns (e.g., notification counters, status indicators)
- Provide migration guidance from common badge implementations in other frameworks

## Code Examples

Our documentation should include examples showing:
- Basic usage
- Each variant type
- Usage with headings, buttons, and other components
- Positioned badges
- Interactive badges
- Dot indicators
- Ribbon badges
- Internationalization examples
- Accessibility examples with proper labeling
- Custom theming examples
- RTL language support examples
- Overflow handling examples

# Unresolved questions

1. **Animation support**: Should the badge component support animations for appearing/disappearing or value changes? What animation properties and timing should be standardized?

2. **Max value handling**: We've proposed the `overflow-count` property, but should we provide additional formatting options for large numbers (e.g., "1K+" for 1000+)?

3. **Interaction behavior**: We've proposed a `clickable` property, but should we extend this with additional interactive behaviors like hover effects or tooltips?

4. **Container context awareness**: How much should the badge respond to or be aware of its container context? Should it auto-adjust position based on container size?

5. **Badge groups**: Should we provide a dedicated container or grouping mechanism for multiple badges to control spacing and alignment?

6. **Custom shapes**: Beyond default and pill shapes, should we allow for custom shapes through CSS or specific shape properties?

7. **Animation customization**: If animations are supported, how customizable should they be?

8. **Accessibility for color variants**: How should we handle cases where users prefer reduced motion or have specific color perception needs?

9. **Badge persistence**: Should we provide built-in options for badge persistence (e.g., badges that remain visible until explicitly dismissed)?

10. **Standalone vs. attached badges**: Should we formalize different behaviors for standalone badges versus those attached to other elements?

11. **Responsive behavior**: How should badges adapt to different screen sizes and viewports?

12. **Badge alignment API**: Should we provide more granular control over badge alignment beyond the basic position property?
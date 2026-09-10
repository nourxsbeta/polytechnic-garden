# Polytechnic Community Garden - CSS Architecture Notes

## CSS organization
The package is divided into reset, base, layout, components, utilities, states, overrides, and print files. `css/main.css` is the single stylesheet that HTML pages should link to.

## Cascade strategy
The project declares this layer order: `reset -> base -> layout -> components -> utilities -> states -> overrides`. Selectors are intentionally low-specificity and primarily class-based. The overrides layer is reserved for genuine exceptions.

## Custom properties
Global tokens in `base.css` cover color, typography, spacing, shape, layout widths, and keyboard focus. Card-specific properties (`--card-background`, `--card-border`, `--card-radius`, and `--card-padding`) demonstrate component-level tokens.

## Naming
Components use descriptive names such as `.site-nav`, `.card`, `.button`, `.callout`, `.form-field`, and `.data-table`. Component elements use `__`, variants use `--`, and utilities use the `u-` prefix.

## Responsive approach
The CSS is mobile-first. Content starts as one column, becomes two columns at 48rem, and card grids can become three columns at 64rem. Images remain responsive through the reset.

## Browser checks
Before submission, test current Chrome, Firefox, and Edge. Resize through narrow, medium, and wide widths; test keyboard focus; inspect the Garden Hours table on a narrow viewport; test form labels/fields; check print preview for Visit & Accessibility; run HTML/CSS validation and Lighthouse.

## Project constraint note
The planning package specifies HTML/CSS only and no JavaScript. For this first architecture package, navigation wraps on narrow screens rather than relying on a JavaScript hamburger. If a collapsible mobile navigation is required later, use an accessible HTML-native pattern such as `details/summary` and verify it against course requirements.

## Refactoring evidence
| Before | After | Improvement |
| --- | --- | --- |
| Repeated `#276044` | `var(--color-primary-700)` | Centralized color |
| Repeated `1.5rem` spacing | `var(--space-5)` | Consistent spacing |
| `header nav ul li a:hover` | `.site-nav__link:hover` | Lower specificity |
| Separate hours/volunteer/workshop card CSS | `.card` | Removes duplication |
| Separate focus declarations | Shared `:focus-visible` rule | Consistent keyboard focus |
| Page-specific widths | `.container` / `.container--narrow` | Reusable layout |
| Repeated responsive grids | `.content-grid` / `.card-grid` | Centralized responsive behavior |
| Hard-coded card values | `--card-*` tokens | Easier component extension |
| Visual `.active` class | `[aria-current="page"]` | Semantic current-page state |

### Example before
```css
.hours-card { padding: 24px; border-radius: 16px; background: #f5f7f4; }
.volunteer-card { padding: 24px; border-radius: 16px; background: #f5f7f4; }
.workshop-card { padding: 24px; border-radius: 16px; background: #f5f7f4; }
```

### Example after
```css
.card {
  padding: var(--card-padding);
  border-radius: var(--card-radius);
  background: var(--card-background);
}
```

## AI disclosure
I used ChatGPT to assist with developing and reviewing the first CSS architecture package for the Polytechnic Community Garden website. AI was used to analyze the requirements in my existing planning package and propose a maintainable CSS organization, cascade strategy, custom-property system, reusable component patterns, utilities, interaction states, responsive rules, print styles, and refactoring examples. I considered the generated CSS against my project brief, sitemap, wireframes, behavior annotations, content inventory, and acceptance criteria. I reviewed the proposed architecture for consistency with the HTML/CSS-only project constraint and adjusted the approach so that it does not depend on JavaScript. The final implementation will be tested in the required browsers, checked for responsive behavior and accessibility, and validated before submission.

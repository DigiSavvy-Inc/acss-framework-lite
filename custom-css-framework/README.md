# Custom ACSS Framework Lite

A lightweight, variable-driven CSS framework inspired by [Automatic.css](https://automaticcss.com) philosophy, focusing on consistency, mathematical precision, and contextual design patterns.

> **Inspiration & Attribution**: This framework is built upon the foundational principles and architectural concepts pioneered by [Kevin Geary](https://geary.co/) and the [Automatic.css team](https://automaticcss.com/). Their tedious attention-detailed approach to systematic CSS architecture, T-shirt sizing methodology, and mathematical design principles serves as the inspiration for this implementation.

## Core Principles

- **Consistency over flexibility**: Limited, predictable options using T-shirt sizing (xs, s, m, l, xl, xxl)
- **Variable-first architecture**: CSS custom properties as foundation
- **Contextual design**: Purpose-built utilities for specific contexts
- **Mathematical relationships**: Proportional scales using calc()
- **Zero dependencies**: Works anywhere CSS works

## Quick Start

### 1. Drop-in CSS (Simplest)

```html
<!-- Add to your HTML head -->
<link rel="stylesheet" href="path/to/framework.min.css">
```

### 2. WordPress Integration (No Plugin Required)

```php
// In your theme's functions.php
function enqueue_custom_acss_framework_lite() {
    wp_enqueue_style(
        'custom-acss-framework-lite',
        get_template_directory_uri() . '/assets/css/framework.min.css',
        array(),
        '1.0.0'
    );
}
add_action('wp_enqueue_scripts', 'enqueue_custom_acss_framework_lite');
```

### 3. SCSS Customization

```scss
// Override default settings before importing
$framework-config: (
  'colors': (
    'primary': #e74c3c,
    'secondary': #3498db,
  ),
  'content-width': 1200px,
);

// Import framework
@import 'path/to/framework/src/main';
```

## File Structure

```
dist/
├── framework.css           # Complete framework (expanded)
├── framework.min.css       # Complete framework (minified)
├── framework-vars.css      # CSS variables only
└── framework-utilities.css # Utility classes only
```

## Key Features

### Color System
- Automatic color variations (light, dark, hover)
- HSL-based for calc() operations
- Transparency variants
- Contextual colors (success, warning, danger, info)

### Typography System
- Fluid, responsive sizing without media queries
- Mathematical type scale
- T-shirt sizing for consistency

### Spacing System
- Golden ratio-based scale
- Contextual gaps (content-gap, grid-gap, container-gap)
- Section spacing utilities

### Layout System
- CSS Grid templates
- Auto-responsive grids
- Container width management
- Flexbox utilities

## Variable Naming Convention

```css
/* Colors */
--primary, --primary-light, --primary-hover

/* Typography */
--h1, --text-m, --text-line-height

/* Spacing */
--space-m, --section-space-l, --grid-gap

/* Layout */
--grid-3, --content-width
```

## Utility Class Convention

```css
/* Double-dash syntax */
.text--xl
.padding--m
.grid--3

/* T-shirt sizes only */
.{property}--{xs|s|m|l|xl|xxl}
```

## Development

```bash
# Install dependencies
npm install

# Build all files
npm run build

# Watch for changes
npm run watch

# Development mode
npm run dev
```

## Browser Support

- Chrome (last 2 versions)
- Firefox (last 2 versions)
- Safari (last 2 versions)
- Edge (last 2 versions)

## Documentation

- **[Getting Started Guide](../docs/GETTING-STARTED.md)** - Learn the core concepts and see examples
- **[Build Instructions](../docs/BUILD.md)** - How to build, watch, and develop the framework
- **[Interactive Style Guide](examples/style-guide.html)** - Live demos of all components and utilities
- **[Examples](examples/)** - Real-world implementation examples

## Project Structure

```
├── src/                    # Source SCSS files
│   ├── config/            # Framework configuration
│   ├── foundation/        # Core functions, mixins, variables
│   ├── systems/           # Color, typography, spacing systems
│   ├── utilities/         # Utility classes
│   └── patterns/          # Component patterns (buttons, cards, etc.)
├── dist/                  # Compiled CSS files
├── examples/              # Usage examples and style guide
└── docs/                  # Additional documentation
```

## Attribution & Inspiration

This framework is deeply inspired by and built upon the architectural principles pioneered by:

- **[Kevin Geary](https://geary.co)** - Visionary behind systematic CSS architecture
- **[Automatic.css Team](https://automaticcss.com)** - Revolutionary CSS framework and methodology

Their work in developing:
- T-shirt sizing methodology
- Mathematical design systems
- Variable-first architecture
- Contextual utility design
- "Consistency over flexibility" philosophy

...serves as the foundation for this implementation. This project aims to honor their principles while providing a standalone, framework-agnostic solution.

## Community & Support

- **Issues**: Report bugs and request features via GitHub Issues
- **Discussions**: Join community discussions for tips and best practices
- **Contributing**: See CONTRIBUTING.md for development guidelines

## Acknowledgments

Special thanks to the Automatic.css community for their continued innovation in systematic CSS design and for inspiring developers to think differently about CSS architecture.

## License

MIT License - feel free to use in personal and commercial projects.

See [LICENSE](LICENSE) for full license text.

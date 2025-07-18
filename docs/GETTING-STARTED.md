# Getting Started

Welcome to the Custom CSS Framework! This guide will help you understand the core concepts and get up and running quickly.

## Philosophy

This framework is inspired by [Automatic.css](https://automaticcss.com) and follows the principle of **"Consistency over Flexibility"**. Instead of infinite options, we provide a carefully curated set of utilities that work harmoniously together.

## Key Concepts

### 1. T-Shirt Sizing
Everything uses the same 6 sizes: `xs`, `s`, `m`, `l`, `xl`, `xxl`

```html
<div class="padding--m text--l margin-bottom--xl">
  <h2 class="text--h2">Consistent sizing across all utilities</h2>
</div>
```

### 2. Double-Dash Syntax
All utility classes use the double-dash convention:

```html
<!-- Typography -->
<h1 class="text--h1">Main Heading</h1>
<p class="text--m text--base-light">Body text</p>

<!-- Layout -->
<div class="grid--3 gap--l">
  <!-- 3-column grid with large gap -->
</div>

<!-- Spacing -->
<section class="padding--xl margin-bottom--l">
  <!-- Large padding, large bottom margin -->
</section>
```

### 3. Mathematical Relationships
Spacing follows the Golden Ratio (1.618) for natural visual harmony:

- `xs`: 0.5rem (8px)
- `s`: 0.75rem (12px) 
- `m`: 1rem (16px)
- `l`: 1.5rem (24px)
- `xl`: 2.25rem (36px)
- `xxl`: 3.5rem (56px)

## Quick Start Examples

### Basic Layout
```html
<div class="container">
  <header class="padding--l margin-bottom--xl">
    <h1 class="text--h1 text--primary">My Website</h1>
    <p class="text--l text--base-light">Subtitle here</p>
  </header>
  
  <main class="grid--2 gap--l">
    <article class="bg--neutral-ultra-light padding--l radius--m">
      <h2 class="text--h3 margin-bottom--m">Article Title</h2>
      <p class="text--m">Article content...</p>
    </article>
    
    <aside class="bg--primary-ultra-light padding--l radius--m">
      <h3 class="text--h4 text--primary margin-bottom--s">Sidebar</h3>
      <p class="text--s">Sidebar content...</p>
    </aside>
  </main>
</div>
```

### Color System
```html
<!-- Text colors -->
<h2 class="text--primary">Primary heading</h2>
<p class="text--base-light">Lighter body text</p>
<span class="text--success">Success message</span>

<!-- Background colors -->
<div class="bg--primary-light text--primary-dark padding--m">
  Light background with dark text
</div>

<!-- Transparency variants -->
<div class="bg--accent-trans-20">
  20% transparent accent background
</div>
```

### Interactive Components
```html
<!-- Buttons -->
<button class="btn btn--primary">Primary Button</button>
<button class="btn btn--secondary btn--outline">Secondary Outline</button>
<button class="btn btn--accent btn--light">Light Button</button>

<!-- Cards -->
<div class="bg--white padding--l radius--m shadow--m">
  <h3 class="text--h4 margin-bottom--s">Card Title</h3>
  <p class="text--m text--base-light">Card content</p>
  <button class="btn btn--primary margin-top--m">Action</button>
</div>
```

## Understanding the Style Guide

The included interactive style guide (`examples/style-guide.html`) demonstrates:

1. **Interactive Color System** - Click color wheels to see variables
2. **Typography Scale** - See how all text sizes relate
3. **Spacing Demo** - Interactive gap spacing controls
4. **Grid Layouts** - Live grid configuration changes
5. **Component Examples** - Buttons, cards, and more

## Customization

### Method 1: CSS Variables (Recommended)
Override variables in your own CSS:

```css
:root {
  --primary: #e74c3c;
  --secondary: #3498db;
  --content-width: 1200px;
  --base-font-size: 18px;
}
```

### Method 2: SCSS Configuration
For deeper customization, modify the SCSS config:

```scss
// Override before importing
$framework-config: (
  'colors': (
    'primary': #your-color,
    'secondary': #your-color,
  ),
  'breakpoints': (
    'tablet': 800px,
    'desktop': 1200px,
  ),
);

@import 'path/to/framework/src/main';
```

## Common Patterns

### Responsive Grids
```html
<!-- Auto-responsive: stacks on mobile, 3 columns on desktop -->
<div class="grid--3 gap--l">
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
</div>

<!-- Asymmetric layout -->
<div class="grid--1-3 gap--m">
  <aside>Sidebar (1/4 width)</aside>
  <main>Main content (3/4 width)</main>
</div>
```

### Content Sectioning
```html
<section class="section-space--l">
  <div class="container">
    <h2 class="text--h2 text--center margin-bottom--xl">Section Title</h2>
    <div class="content-grid">
      <!-- Content automatically centers and can break out to feature areas -->
    </div>
  </div>
</section>
```

### State Management
```html
<!-- Hover states -->
<div class="bg--neutral hover:bg--neutral-light">Hover me</div>

<!-- Focus states (automatically included on interactive elements) -->
<button class="btn btn--primary">Accessible button</button>

<!-- Shadow states -->
<div class="shadow--m hover:shadow--l">Card with hover effect</div>
```

## Development Workflow

1. **Start with semantic HTML**
2. **Add utility classes for styling**
3. **Use the interactive style guide to find the right classes**
4. **Customize variables as needed**
5. **Build components by combining utilities**

For instructions on building and watching the CSS files during development, see the **[Build Instructions](BUILD.md)**.

## Next Steps

- Explore the interactive style guide
- Check out the examples in the `/examples` folder
- Read the full documentation in README.md
- Learn how to build and customize the framework in [BUILD.md](BUILD.md)
- Join the community discussions for tips and best practices

## Need Help?

- **Style Guide**: Open `examples/style-guide.html` for interactive examples
- **Documentation**: See README.md for complete API reference
- **Examples**: Check the `/examples` folder for real-world usage

---

**Attribution**: This framework is inspired by [Kevin Geary](https://geary.co) and the [Automatic.css team](https://automaticcss.com). Their pioneering work in systematic CSS architecture provides the foundation for this implementation.
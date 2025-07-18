# Build Instructions - Custom ACSS Framework Lite

This guide explains how to build, watch, and develop the Custom ACSS Framework Lite CSS files.

## Prerequisites

- Node.js (v14 or higher)
- npm (comes with Node.js)

## Initial Setup

1. Clone the repository:
```bash
git clone git@github.com:DigiSavvy-Inc/acss-lite.git
cd acss-lite
```

2. Install dependencies:
```bash
npm install
```

## Build Commands

### Build All Files
```bash
npm run build
```
This command builds all CSS variations:
- `dist/framework.css` - Complete framework (expanded format)
- `dist/framework.min.css` - Complete framework (minified)
- `dist/framework-vars.css` - CSS variables only (minified)
- `dist/framework-utilities.css` - Utility classes only (minified)

### Development Mode (Watch)
```bash
npm run dev
# or
npm run watch
```
This watches for changes in `src/` directory and automatically rebuilds `dist/framework.css` when you save files.

### Individual Build Commands

Build specific files when needed:

```bash
# Build expanded CSS only
npm run build:expanded

# Build minified CSS only
npm run build:compressed

# Build CSS variables only
npm run build:vars

# Build utility classes only
npm run build:utilities
```

## File Structure

```
src/
├── config/           # Framework configuration
│   └── _settings.scss
├── foundation/       # Core functions, mixins, variables
│   ├── _breakpoints.scss
│   ├── _functions.scss
│   ├── _mixins.scss
│   ├── _reset.scss
│   ├── _variables-export.scss
│   └── _variables.scss
├── systems/          # Design systems
│   ├── _colors.scss
│   ├── _effects.scss
│   ├── _layout.scss
│   ├── _spacing.scss
│   └── _typography.scss
├── utilities/        # Utility classes
│   ├── _colors.scss
│   ├── _display.scss
│   ├── _effects.scss
│   ├── _layout.scss
│   ├── _position.scss
│   ├── _responsive.scss
│   ├── _spacing.scss
│   └── _text.scss
├── patterns/         # Component patterns
│   ├── _alerts.scss
│   ├── _badges.scss
│   ├── _buttons.scss
│   ├── _cards.scss
│   ├── _forms.scss
│   └── _navigation.scss
├── main.scss         # Main entry point
└── utilities-export.scss  # Utilities-only entry point

dist/                 # Built CSS files (generated)
├── framework.css
├── framework.min.css
├── framework-vars.css
└── framework-utilities.css
```

## Development Workflow

1. **Start watching for changes:**
   ```bash
   npm run dev
   ```

2. **Make changes to SCSS files in `src/`**
   - Variables: `src/foundation/_variables.scss`
   - Colors: `src/systems/_colors.scss`
   - Typography: `src/systems/_typography.scss`
   - Custom utilities: Add to appropriate file in `src/utilities/`

3. **Test your changes:**
   - Open `examples/style-guide.html` in a browser
   - The CSS will auto-update when you save (refresh browser to see changes)

4. **Build for production:**
   ```bash
   npm run build
   ```

## Customization

To customize the framework settings, edit `src/config/_settings.scss`:

```scss
// Example customizations
$framework-config: (
  'colors': (
    'primary': #e74c3c,
    'secondary': #3498db,
  ),
  'typography': (
    'base-size': 18px,
    'scale': 1.25,
  ),
  'spacing': (
    'base': 1rem,
  ),
  'content-width': 1200px,
  'enable-smooth-scroll': true,
);
```

## Troubleshooting

### Changes not appearing
1. Make sure `npm run dev` is running
2. Check for SCSS compilation errors in terminal
3. Hard refresh your browser (Ctrl+Shift+R or Cmd+Shift+R)

### Build errors
1. Delete `node_modules` and reinstall:
   ```bash
   rm -rf node_modules
   npm install
   ```
2. Ensure you're using a compatible Node.js version (14+)

### Deprecation warnings
The Sass compiler may show deprecation warnings. These don't affect functionality but indicate areas that may need updates in future versions.

## Contributing

When contributing changes:
1. Always run `npm run build` before committing
2. Test changes in `examples/style-guide.html`
3. Ensure no build errors occur
4. Update relevant documentation if adding new features
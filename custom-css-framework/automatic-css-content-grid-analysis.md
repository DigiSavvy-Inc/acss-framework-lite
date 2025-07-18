# AutomaticCSS Content-Grid System: Mathematical Implementation Analysis

## Overview

This document analyzes the mathematical calculations and implementation details of AutomaticCSS's content-grid system, providing specific file references where each calculation can be found in the plugin codebase.

**Plugin Location:** `/Users/alexandervasquez/Repositories/upstream-bricks-github/wp-content/plugins/automaticcss-plugin/`

## Core Mathematical Concepts

### 1. Auto-Grid Breakpoint Calculations

**File:** `assets/scss/modules/grid/_grid-maps.scss:1-6`

The plugin calculates responsive breakpoints for auto-grids using a sophisticated mathematical formula:

```scss
$auto-grid-math: $base-space * 2rem;
$auto-break-2: ($vp-max - $base-space * 2) * 1rem / 2.99;
$auto-break-3: ($vp-max - $base-space * 2) * 1rem / 3.99;
$auto-break-4: ($vp-max - $base-space * 2) * 1rem / 4.99;
$auto-break-5: ($vp-max - $base-space * 2) * 1rem / 5.99;
$auto-break-6: ($vp-max - $base-space * 2) * 1rem / 6.99;
```

**Mathematical Formula:**
```
breakpoint = (max_viewport - padding) / (desired_columns + 0.99)
```

**Key Insight:** The `+ 0.99` creates a buffer to prevent premature grid collapse due to sub-pixel rounding issues, ensuring items don't wrap until they truly need to.

### 2. Auto-Fit Grid Implementation

**File:** `assets/scss/modules/grid/_grid-maps.scss:32-56`

The auto-grids use CSS Grid's `auto-fit` with sophisticated `minmax()` calculations:

```scss
"auto-3": repeat(
  auto-fit,
  minmax(min(#{$auto-break-3}, 100vw - #{$auto-grid-math}), 1fr)
),
"auto-4": repeat(
  auto-fit,
  minmax(min(#{$auto-break-4}, 100vw - #{$auto-grid-math}), 1fr)
),
```

**Mathematical Breakdown:**
- `min(calculated_breakpoint, available_space - padding)`
- Compares the calculated breakpoint against actual available space
- Ensures items never exceed container bounds
- Uses `1fr` for maximum flexibility after minimum requirements are met

### 3. Content-Width System

**File:** `assets/scss/modules/_width.scss:17-26`

Two complementary content-width approaches:

```scss
.content-width:not([class*="breakout--"]) {
  inline-size: 100%;
  max-inline-size: var(--content-width);
  margin-inline: auto;
}

.content-width--safe:not([class*="breakout--"]) {
  inline-size: 100%;
  max-inline-size: var(--content-width-safe);
  margin-inline: auto;
}
```

**Safe Content Width Calculation:**
**File:** `assets/scss/modules/_variables.scss:49`

```scss
--content-width-safe: min(var(--width-content), calc(100% - var(--section-padding-x) * 2));
```

**Formula:** `min(content_width, viewport_width - (horizontal_padding * 2))`

This ensures content never gets too close to viewport edges by maintaining consistent horizontal padding.

### 4. Grid Stagger Prevention Logic

**File:** `assets/scss/modules/grid/_grid.scss:48-91`

Special handling prevents grid staggering on smaller screens:

```scss
@include breakpoint(l) {
  .grid--auto-1-2 {
    display: grid !important;
    grid-template-columns: repeat(
      auto-fit,
      minmax(min(#{$auto-break-3}, 100vw - #{$auto-grid-math}), 1fr)
    );
  }
  // ... continues for other auto-grid variants
}
```

**Key Strategy:** Forces all auto-grids to use consistent breakpoint calculations at the large breakpoint and below, preventing visual inconsistencies.

### 5. Standard Grid Definitions

**File:** `assets/scss/modules/grid/_grid-maps.scss:8-64`

The plugin defines three grid types with different mathematical approaches:

#### Standard Grids (Equal Columns)
```scss
standard: (
  "1": repeat(1, minmax(0, 1fr)),
  "2": repeat(2, minmax(0, 1fr)),
  "3": repeat(3, minmax(0, 1fr)),
  // ... up to 12 columns
),
```

#### Premade Grids (Proportional Ratios)
```scss
premade: (
  "1-2": minmax(0, 1fr) minmax(0, 2fr),
  "1-3": minmax(0, 1fr) minmax(0, 3fr),
  "2-1": minmax(0, 2fr) minmax(0, 1fr),
  // ... various ratios
),
```

#### Auto Grids (Responsive Calculations)
```scss
auto: (
  "auto-2": repeat(auto-fit, minmax(min(#{$auto-break-2}, 100vw - #{$auto-grid-math}), 1fr)),
  // ... uses calculated breakpoints
),
```

### 6. Viewport Calculation Variables

**File:** `assets/scss/helpers/_calc-math.scss:1-5`

Foundation calculations for responsive behavior:

```scss
$clamp-math: calc(1vw - #{$vp-min} / 100 * 1rem);
$vp-delta: calc(#{$vp-max} - #{$vp-min});
$calc-math: calc(100vw - (#{$vp-min} * 1rem) / (#{$vp-max} - #{$vp-min}));
$auto-grid-math: calc(100vw - (#{$base-space} * 3) * 1rem); // commented out
```

These variables support the fluid calculations used throughout the grid system.

## Implementation Details

### Grid Generation Process

**File:** `assets/scss/modules/grid/_grid.scss:8-24`

```scss
@each $grid-type, $col-set in $grids {
  @each $col-count, $value in $col-set {
    .grid--#{$col-count} {
      display: grid !important;
      grid-template-columns: #{$value};
      inline-size: 100%;
      
      @if $col-count == "1" {
        > * {
          grid-column: 1 !important;
        }
      }
    }
  }
}
```

### Responsive Grid Classes

**File:** `assets/scss/modules/grid/_grid.scss:25-44`

Breakpoint-specific grid classes are generated dynamically:

```scss
@each $breakpoint, $value in $breakpoints {
  @include breakpoint($breakpoint) {
    @each $grid-type, $col-set in $grids {
      @each $col-count, $colValue in $col-set {
        @if $grid-type == standard {
          .grid--#{$breakpoint}-#{$col-count} {
            grid-template-columns: #{$colValue};
          }
        }
      }
    }
  }
}
```

### Grid Span and Positioning

**File:** `assets/scss/modules/grid/_grid.scss:120-178`

Mathematical control for grid item positioning:

```scss
@each $column, $value in $gridColumns {
  .col-span--#{$column} {
    grid-column: span #{$value};
  }
  .col-start--#{$column} {
    grid-column-start: #{$value};
  }
  .col-end--#{$column} {
    grid-column-end: #{$value};
  }
}
```

## Key Mathematical Innovations

### 1. Sub-Pixel Precision
- Uses `.99` suffixes instead of whole numbers for breakpoint calculations
- Prevents premature wrapping due to browser rounding inconsistencies
- Ensures smooth grid behavior across different screen sizes

### 2. Container-Aware Calculations
- All breakpoints account for container padding (`$auto-grid-math`)
- Uses `min()` function to respect actual available space
- Prevents horizontal overflow in constrained containers

### 3. Proportional Scaling
- Maintains mathematical relationships between grid sizes
- Consistent `.99` increment pattern across all auto-breakpoints
- Harmonious ratios in premade grid configurations

### 4. Performance Optimization
- Calculations done at compile-time, not runtime
- Static CSS classes generated from SCSS maps
- No JavaScript required for responsive behavior

## Usage Examples

Based on the mathematical implementations:

```css
/* Auto-grid that switches from 3 columns to fewer based on available space */
.grid--auto-3 {
  grid-template-columns: repeat(
    auto-fit, 
    minmax(min(344px, calc(100vw - 2rem)), 1fr)
  );
}

/* Content-width that respects container padding */
.content-width--safe {
  max-inline-size: min(var(--width-content), calc(100% - var(--section-padding-x) * 2));
}

/* Proportional grid with 1:2 ratio */
.grid--1-2 {
  grid-template-columns: minmax(0, 1fr) minmax(0, 2fr);
}
```

## Conclusion

AutomaticCSS's content-grid system achieves sophisticated responsive behavior through precise mathematical calculations that account for:

- Viewport constraints and available space
- Container padding and margins  
- Sub-pixel precision and browser rounding
- Proportional relationships between grid elements
- Performance optimization through compile-time calculations

The system's mathematical foundation ensures consistent, predictable behavior across different screen sizes and container contexts while maintaining visual harmony through proportional scaling.
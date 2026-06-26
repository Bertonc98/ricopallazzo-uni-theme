# Ricopallazzo Touying Theme

A custom theme for the Typst presentation package **Touying**, providing:

- Custom title slide
- Branded header and footer
- Multiple progress indicator styles
- Automatic section slides with outline
- Color themes
- Alert boxes
- Configurable branding

---

# Installation

```typst
#import "@preview/touying:0.7.4": *
#import "theme.typ": *
```

Wrap the entire presentation with:

```typst
#show: ricopallazzo-theme.with(
    ...
)
```

---

# Basic Example

```typst
#import "@preview/touying:0.7.4": *
#import "theme.typ": *

#show: ricopallazzo-theme.with(
    aspect-ratio: "presentation-16-9",
    theme: "orange",
    title: "My Presentation",
    short_title: "Presentation",
    author: "John Doe",
    institute: "University",
    logo: "assets/logo.png",
    logo_name: "assets/logo_text.png",
)

#title-slide()

= First Section

== First slide

Hello world.
```

---

# Theme Parameters

## ricopallazzo-theme

```typst
#show: ricopallazzo-theme.with(...)
```

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `aspect-ratio` | string | `"16-9"` | Paper format passed to Touying |
| `theme` | string | `"blue"` | Color palette defined in `themes_colors.typ` |
| `title` | content/string | `none` | Presentation title |
| `short_title` | content/string | `none` | Short title shown in footer |
| `author` | content/string | `none` | Author name |
| `institute` | content/string | `none` | Institution shown on title slide |
| `date` | bool | `true` | Show today's date on title slide |
| `logo` | path | `"assets/logo_RGB.png"` | Logo displayed in header |
| `logo_name` | path | `"assets/logo_RGB.png"` | Large logo shown on title slide |
| `progress` | string | `"slide"` | Progress indicator mode |
| `prefix` | string | `"triangle"` | Outline prefix style |

---

# Title Slide

Generate the cover slide with

```typst
#title-slide()
```

The slide automatically displays:

- title
- short title
- author
- institute
- current date (optional)
- large branding logo

The layout includes a colored polygon in the upper-right corner and a large logo positioned in the lower-right area.

---

# Slides

Slides are created normally with headings:

```typst
= Section

== Slide title

Content...
```

The theme automatically replaces Touying's default slide layout with the custom one.

---

# Automatic Section Slides

Each level-1 heading (`=`) automatically generates a section slide containing the presentation outline.

Example:

```typst
= Optimization

== Model

...

== Results

...
```

The outline:

- highlights the current section
- fades previous/future sections
- creates clickable navigation links

---

# Header

Every content slide contains a custom header with three areas.

## Left

Displays:

- current section
- slide title (or custom title)

## Center

Displays the selected progress indicator.

## Right

Displays the logo.

---

# Footer

The footer contains:

Left:

- short presentation title

Center:

- author

Right:

- current slide number
- total number of slides

Example:

```
Optimization | Alberto Bertoncini | 12 / 34
```

---

# Progress Indicators

The appearance is controlled by

```typst
progress: ...
```

Available modes are:

## slide

Displays one dot per slide.

Current and previous slides are highlighted.

```typst
progress: "slide"
```

---

## section

Displays one dot per section.

Useful for presentations with many slides.

```typst
progress: "section"
```

---

## slide-by-section

Displays one dot per slide while inserting larger spacing between different sections.

```typst
progress: "slide-by-section"
```

Example

```
● ● ●   ● ● ● ●   ● ●
```

---

## mini

Uses Touying's built-in miniature slide navigation.

```typst
progress: "mini"
```

---

# Outline Prefix

Controls how entries appear in automatic section slides.

## Numbering

```typst
prefix: "numbering"
```

Produces

```
1
2
3
```

---

## Triangle

```typst
prefix: "triangle"
```

Produces

```
▶
▶
▶
```

---

# Alert Boxes

The theme provides

```typst
#alert_box(...)
```

Example

```typst
#alert_box[
Important result
]
```

Custom color angle:

```typst
#alert_box(
    angle: 120deg
)[
Green message
]
```

Custom text color:

```typst
#alert_box(
    content_color: white
)[
Dark text example
]
```

---

# Color Themes

The theme loads palettes from

```
src/themes_colors.typ
```

Each palette must define

```typst
(
    primary: ...,
    lightest: ...,
    darkest: ...,
    light-grey: ...,
    dark-grey: ...
)
```

Example

```typst
blue: (
    primary: rgb(...),
    lightest: rgb(...),
    darkest: rgb(...),
    light-grey: rgb(...),
    dark-grey: rgb(...),
)
```

Select it with

```typst
theme: "blue"
```

---

# Custom Slide Titles

Normally the slide title is taken from the level-2 heading.

It can be overridden using

```typst
#slide(title: "Custom Title")[
    ...
]
```

The custom title is displayed in the header.

---

# Internal Components

The theme is organized around the following functions.

| Function | Purpose |
|----------|---------|
| `ricopallazzo-theme` | Main theme configuration |
| `slide` | Standard presentation slide |
| `title-slide` | Cover slide |
| `new-section-slide` | Automatic outline slide |
| `header` | Header renderer |
| `footer` | Footer renderer |
| `progress-indicator` | Chooses progress visualization |
| `dots` | Dot rendering engine |
| `alert_box` | Styled alert component |

---

# Typical Configuration

```typst
#show: ricopallazzo-theme.with(
    aspect-ratio: "presentation-16-9",

    theme: "orange",

    title: "My Presentation",
    short_title: "Presentation",

    author: "John Doe",
    institute: "University",

    logo: "assets/logo.png",
    logo_name: "assets/logo_text.png",

    progress: "slide-by-section",

    prefix: "triangle",

    date: true,
)
```

This configuration enables:

- 16:9 presentation
- orange color palette
- custom branding
- automatic section slides
- slide-by-section progress indicator
- triangular outline bullets
- current date on the title slide

# Lewes HC – Visiting Team Guide

| File | What it is |
|------|------------|
| `lewes-visiting-team-guide.html` | Source page (a single embedded SVG laid out for A4) |
| `Lewes HC - visiting team guide.pdf` | A4 PDF export |

## Converting the HTML to an A4 PDF

The page's CSS sets the print size to A4 and fixes the SVG to exactly that size:

```css
@page { size:210mm 297mm; margin:0; }
svg { display:block; width:210mm; height:297mm; }
```

Keep the SVG at a fixed `210mm × 297mm`. Don't use `width:100%; height:auto`.
The viewBox (595 × 842) is a hair taller than A4's exact proportions
(594.96 × 841.92 pt), so auto-height overflows the page by a fraction of a point
and Chrome adds a blank second page.

### Command line (headless Chrome)

```bash
google-chrome --headless --no-pdf-header-footer \
    --print-to-pdf="Lewes HC - visiting team guide.pdf" \
    "file://$PWD/lewes-visiting-team-guide.html"
```

Chrome uses the CSS `@page` size, so you don't need a paper-size flag.

Check the result. It should be a single A4 page:

```bash
pdfinfo "Lewes HC - visiting team guide.pdf" | grep -E 'Pages|Page size'
# Pages:      1
# Page size:  594.96 x 841.92 pts (A4)
```

### From the browser (no command line)

1. Open `lewes-visiting-team-guide.html` in Chrome.
2. Press **Ctrl+P** and set **Destination** to **Save as PDF**.
3. Under **More settings**:
   - **Paper size:** A4
   - **Margins:** None
   - **Headers and footers:** off
   - **Background graphics:** on
4. Click **Save**.

### Printing tips

- Print at 100% / "Actual size" so the printer doesn't add its own scaling.
- The design goes right to the page edges. Most home printers can't print to the
  edge, so expect a thin white border unless a print shop trims it.

# QR Code Generator

A clean, dark-themed QR code generator that turns any URL or text into a downloadable QR code. Supports color customization, size control, and four error correction levels.

![QR Code Generator](https://img.shields.io/badge/HTML-CSS-JS-purple?style=flat-square) ![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)

---

## Features

- **Live generation** — QR updates automatically as you type (debounced)
- **Custom colors** — pick any foreground and background color
- **Size control** — slider from 128px to 512px
- **Error correction levels** — L (7%), M (15%), Q (25%), H (30%)
- **Download as PNG** — saves the QR code directly to your device
- **Copy URL** — copies the input text/URL to your clipboard

---

## How to Use

1. Open `index.html` in any browser — or visit the live GitHub Pages link
2. Type or paste a **URL or any text** into the input field
3. The QR code generates **live as you type**
4. Adjust **size**, **colors**, and **error correction** as needed
5. Click **Download PNG** to save the QR image
6. Scan with any phone camera to test it

---

## Error Correction Levels Explained

| Level | Recovery | Best for |
|-------|----------|----------|
| L | 7% | Clean environments, digital screens |
| M | 15% | General use (default) |
| Q | 25% | Slightly dirty or printed surfaces |
| H | 30% | Logos overlaid on the QR, rough surfaces |

Higher correction = more complex QR = harder to scan at small sizes. Use **H** only if you plan to overlay a logo on the QR code.

---

## How to Customize

All customization lives inside `index.html`. No build tools needed.

### Change the default colors

Find the color inputs in the HTML and change the `value` attributes:

```html
<input type="color" id="fgColor" value="#1a1a2e">  <!-- QR color -->
<input type="color" id="bgColor" value="#ffffff">  <!-- background -->
```

Set them to any valid hex color. For a white-on-black QR:
```html
<input type="color" id="fgColor" value="#ffffff">
<input type="color" id="bgColor" value="#000000">
```

### Change the default error correction level

Find the button that starts active and switch which one has the `active` class:

```html
<button class="ec-btn" data-level="L">L ...</button>
<button class="ec-btn active" data-level="M">M ...</button>  <!-- active = default -->
<button class="ec-btn" data-level="Q">Q ...</button>
<button class="ec-btn" data-level="H">H ...</button>
```

Move `active` to `data-level="H"` if you want maximum error correction by default.

Also update the JS variable:
```js
let ecLevel = 'M'; // change to 'L', 'Q', or 'H'
```

### Change the default QR size

Find the size slider and change `value`:

```html
<input type="range" id="sizeSlider" min="128" max="512" step="16" value="256">
```

Set `value="512"` for a larger default, or change `max` to allow even bigger sizes.

### Change the auto-generate delay

The QR regenerates while you type, with a 500ms debounce. To change the delay:

```js
debounceTimer = setTimeout(() => { if (inputText.value.trim()) generate(); }, 500);
//                                                                            ^^^
//                                                               change this in ms
```

Set to `0` for instant generation, or `1000` for a 1-second delay.

### Change the download filename

Find the download handler and update the filename:

```js
link.download = 'qrcode.png'; // change to any name you want
```

For example: `link.download = 'my-qr-code.png';`

### Change the page layout (side-by-side vs stacked)

The two-column layout uses CSS Grid. Find the `.page` rule:

```css
.page {
  max-width: 860px;
  display: grid;
  grid-template-columns: 1fr 1fr; /* two equal columns */
}
```

Change to `grid-template-columns: 1fr` for a single stacked column on all screen sizes.

---

## Tech Stack

| Layer | Tech |
|-------|------|
| Structure | HTML5 |
| Styling | CSS3 (grid, custom properties, transitions) |
| Logic | Vanilla JavaScript |
| QR Engine | [qrcodejs](https://github.com/davidshimjs/qrcodejs) (CDN) |
| Font | Inter (Google Fonts) |

---

## License

MIT — free to use, modify, and distribute.

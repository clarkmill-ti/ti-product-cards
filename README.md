# TI Product Card Builder

A self-hosted tool for building branded product/sponsor card iframes to embed in The Information's CMS.

## What it does

- **Build** product cards using The Information's exact design tokens (beige `#F7F5F2`, charcoal `#2F3538`, magenta `#F32A52`)
- **Preview** live at different breakpoints
- **Export** each card as a standalone self-contained HTML file
- **Embed** cards in articles via `<iframe>` — no CMS plugin required

## Setup (GitHub Pages)

1. Fork or clone this repo
2. Enable GitHub Pages: **Settings → Pages → Deploy from branch → main / root**
3. Your builder is live at `https://YOUR-ORG.github.io/YOUR-REPO/`

## Workflow

1. Open `index.html` in your browser (or on GitHub Pages)
2. Fill in the form: product name, description, price, CTA, image URL
3. Choose theme (Light / Dark) and layout
4. Click **Save Card** → then **Export / Deploy**
5. Download the generated card HTML
6. Drop it in the `cards/` folder and push to GitHub
7. Copy the iframe snippet into the CMS article

## Embed example

```html
<iframe
  src="https://YOUR-ORG.github.io/YOUR-REPO/cards/google-gemini-ad.html"
  width="100%"
  height="320"
  frameborder="0"
  scrolling="no"
  style="border:none;display:block;"
></iframe>
```

## Auto-height (optional)

Each exported card sends its height to the parent page via `postMessage`:

```js
window.addEventListener('message', (e) => {
  if (e.data?.type === 'ti-card-height') {
    document.querySelector('iframe').style.height = e.data.height + 'px';
  }
});
```

Add this snippet to your CMS article template to eliminate whitespace below cards.

## File structure

```
your-repo/
├── index.html        ← Card builder tool
├── README.md
└── cards/
    ├── google-gemini-ad.html
    ├── digitalocean-sponsor.html
    └── ...
```

## Design tokens

| Token | Value |
|---|---|
| Background beige | `#F7F5F2` |
| Charcoal | `#2F3538` |
| Magenta | `#F32A52` |
| Mid gray | `#8D9395` |
| Border | `#DDD9D4` |

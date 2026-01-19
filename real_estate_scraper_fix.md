# Real Estate Scraper Fix Specification

**Date:** 2026-01-19
**Target Site:** immobilien.derstandard.at
**Prototype:** real-estate-financing.html

---

## Problem Statement

The current scraper implementation in `real-estate-financing.html` fails to extract property data correctly from `immobilien.derstandard.at` listing pages. The selectors used do not match the actual DOM structure of the website.

### Expected Data (Test URL: https://immobilien.derstandard.at/detail/15006491)
- **Address:** 1070 Wien, Burggasse
- **Headline:** ZENTRAL & RUHIG - sanierter Altbau mit Lift innerhalb des Gürtels
- **Price (Kaufpreis):** € 445.000
- **Living Area (Wohnfläche):** 71.3 m²
- **Rooms (Zimmer):** 3
- **Main Image:** https://i.prod.mp-dst.onyx60.com/plain/immoimporte/justimmo2/storage.justimmo.at/thumb/2b57b81c76350b0c883c1b45b0847788/fm_h1080_w1920/6hrGts5ZkOQIX9pz5eZreN20251210.jpg/...

---

## Correct CSS Selectors

### 1. Address
**Selector:** `.heading-section-address`

```javascript
const address = doc.querySelector('.heading-section-address')?.textContent.trim();
// Returns: "1070 Wien, Burggasse"
```

### 2. Headline/Title
**Selector:** `h1` (with classes `Heading_heading___t1Z5 Heading_headingInseratTitle__tnAUR`)

```javascript
const headline = doc.querySelector('h1')?.textContent.trim();
// Returns: "ZENTRAL & RUHIG - sanierter Altbau mit Lift innerhalb des Gürtels"
```

### 3. Price, Living Area, Rooms (Key Statistics)
**Structure:** These are in `.sc-stat` containers with `.sc-stat-label` and `.sc-stat-value` children

```html
<div class="sc-stat">
  <div class="sc-stat-label">Kaufpreis</div>
  <div class="sc-stat-value sc-stat-value-default">€ 445.000</div>
</div>
<div class="sc-stat">
  <div class="sc-stat-label">Wohnfläche</div>
  <div class="sc-stat-value sc-stat-value-md">71.3 m²</div>
</div>
<div class="sc-stat">
  <div class="sc-stat-label">Zimmer</div>
  <div class="sc-stat-value sc-stat-value-md">3</div>
</div>
```

**Extraction Function:**
```javascript
function extractStatByLabel(doc, labelText) {
    const stats = doc.querySelectorAll('.sc-stat');
    for (const stat of stats) {
        const label = stat.querySelector('.sc-stat-label');
        if (label && label.textContent.trim().toLowerCase() === labelText.toLowerCase()) {
            const value = stat.querySelector('.sc-stat-value');
            return value ? value.textContent.trim() : null;
        }
    }
    return null;
}

// Usage:
const price = extractStatByLabel(doc, 'Kaufpreis');      // "€ 445.000"
const livingArea = extractStatByLabel(doc, 'Wohnfläche'); // "71.3 m²"
const rooms = extractStatByLabel(doc, 'Zimmer');          // "3"
```

### 4. Main Image
**Structure:** Images are in `<picture>` elements with `<source>` tags containing the actual image URLs in `srcset`

```html
<picture>
  <source srcset="https://i.prod.mp-dst.onyx60.com/plain/immoimporte/justimmo2/storage.justimmo.at/thumb/.../format:avif/...">
  <source srcset="https://i.prod.mp-dst.onyx60.com/plain/immoimporte/justimmo2/storage.justimmo.at/thumb/.../format:jpg/...">
  <img src="placeholder.svg" alt="Bild 1 von 13" class="sc-image sc-image-default">
</picture>
```

**Extraction Function:**
```javascript
function extractMainImage(doc) {
    // Get the first picture element's source
    const pictures = doc.querySelectorAll('picture');
    for (const picture of pictures) {
        const sources = picture.querySelectorAll('source');
        for (const source of sources) {
            const srcset = source.getAttribute('srcset');
            if (srcset && !srcset.includes('placeholder')) {
                // Extract the URL from srcset (may contain width descriptors)
                const url = srcset.split(' ')[0].split(',')[0].trim();
                if (url.includes('justimmo') || url.includes('mp-dst')) {
                    return url;
                }
            }
        }
    }

    // Fallback: Check og:image meta tag
    const ogImage = doc.querySelector('meta[property="og:image"]');
    if (ogImage) {
        return ogImage.getAttribute('content');
    }

    return null;
}
```

---

## Complete Updated scrapeProperty Function

Replace the existing `scrapeProperty` function with:

```javascript
async function scrapeProperty(url) {
    try {
        const proxies = [
            'https://corsproxy.io/?',
            'https://api.codetabs.com/v1/proxy?quest='
        ];

        let html = null;

        for (const proxyUrl of proxies) {
            try {
                const response = await fetch(proxyUrl + encodeURIComponent(url), {
                    timeout: 10000
                });
                if (response.ok) {
                    html = await response.text();
                    break;
                }
            } catch (error) {
                console.log(`Proxy ${proxyUrl} failed, trying next...`);
            }
        }

        if (!html) {
            console.log('All proxies failed, using demo data');
            return getDemoPropertyData();
        }

        const parser = new DOMParser();
        const doc = parser.parseFromString(html, 'text/html');

        // Extract using correct selectors
        const data = {
            title: doc.querySelector('h1')?.textContent.trim() || '',
            location: doc.querySelector('.heading-section-address')?.textContent.trim() || '',
            price: extractPrice(doc),
            livingArea: extractStatByLabel(doc, 'Wohnfläche') || 'N/A',
            rooms: extractStatByLabel(doc, 'Zimmer') || 'N/A',
            type: 'Wohnung', // Default or extract from page
            description: extractDescription(doc),
            image: extractMainImage(doc)
        };

        console.log('Extracted data:', data);

        if (!data.title || !data.price) {
            return getDemoPropertyData();
        }

        return data;
    } catch (error) {
        console.error('Scraping error:', error);
        return getDemoPropertyData();
    }
}

function extractStatByLabel(doc, labelText) {
    const stats = doc.querySelectorAll('.sc-stat');
    for (const stat of stats) {
        const label = stat.querySelector('.sc-stat-label');
        if (label && label.textContent.trim().toLowerCase() === labelText.toLowerCase()) {
            const value = stat.querySelector('.sc-stat-value');
            return value ? value.textContent.trim() : null;
        }
    }
    return null;
}

function extractPrice(doc) {
    const priceText = extractStatByLabel(doc, 'Kaufpreis');
    if (priceText) {
        // Parse "€ 445.000" to number 445000
        const match = priceText.match(/[\d.,]+/);
        if (match) {
            const priceStr = match[0].replace(/\./g, '').replace(',', '.');
            return parseFloat(priceStr);
        }
    }
    return null;
}

function extractMainImage(doc) {
    const pictures = doc.querySelectorAll('picture');
    for (const picture of pictures) {
        const sources = picture.querySelectorAll('source');
        for (const source of sources) {
            const srcset = source.getAttribute('srcset');
            if (srcset && !srcset.includes('placeholder')) {
                const url = srcset.split(' ')[0].split(',')[0].trim();
                if (url.startsWith('http') && (url.includes('justimmo') || url.includes('mp-dst'))) {
                    return url;
                }
            }
        }
    }

    const ogImage = doc.querySelector('meta[property="og:image"]');
    if (ogImage) {
        return ogImage.getAttribute('content');
    }

    return 'https://via.placeholder.com/800x400/1e3c72/ffffff?text=Property+Image';
}

function extractDescription(doc) {
    // Description is in a region with heading "Beschreibung"
    const regions = doc.querySelectorAll('region, section, [role="region"]');
    for (const region of regions) {
        const heading = region.querySelector('h2, h3');
        if (heading && heading.textContent.toLowerCase().includes('beschreibung')) {
            const paragraphs = region.querySelectorAll('p, div:not([class])');
            const texts = Array.from(paragraphs).map(p => p.textContent.trim()).filter(t => t.length > 20);
            return texts.join(' ').substring(0, 500);
        }
    }
    return '';
}
```

---

## Summary of Changes

| Field | Old Selector(s) | New Selector(s) |
|-------|----------------|-----------------|
| Address | `.object-location, [itemprop="address"], .location` | `.heading-section-address` |
| Title | `h1.object-title, h1[itemprop="name"], .detail-title` | `h1` |
| Price | `.object-price, [itemprop="price"], .price` | `.sc-stat` with label "Kaufpreis" → `.sc-stat-value` |
| Living Area | Label search in `.heading-section-stats` | `.sc-stat` with label "Wohnfläche" → `.sc-stat-value` |
| Rooms | Label search in `.heading-section-stats` | `.sc-stat` with label "Zimmer" → `.sc-stat-value` |
| Image | `img.sc-image-default` src attribute | `picture source` srcset attribute |

---

## Testing

After implementing the fix, test with:
1. https://immobilien.derstandard.at/detail/15006491 (test listing)
2. Other random listings from immobilien.derstandard.at to ensure selectors work universally

---

## Notes

- The website uses a React-based frontend with lazy-loaded images
- Images use `<picture>` elements with WebP/AVIF sources in `srcset` and placeholder SVGs in `<img>` tags
- Key statistics (price, area, rooms) follow a consistent `.sc-stat` → `.sc-stat-label` + `.sc-stat-value` pattern
- The address uses `.heading-section-address` class consistently across listings

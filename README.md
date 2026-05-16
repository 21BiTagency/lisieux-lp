# Residenza Lisieux — Landing Page

Landing page one-page per il cantiere "Residenza Lisieux" ad Albignasego (PD), località San Giacomo. Cliente: **Tettorosso Immobiliare — Agenzia Voltabarozzo**. Costruttore: **COEB Costruzioni S.r.l.**.

## Status

- **Tipo**: pagina dimostrativa / template costruttori
- **Indicizzazione**: `noindex, nofollow` — raggiungibile solo via link diretto
- **Form contatto**: NON funzionale (template visivo, alert su submit)
- **Telefono / email / WhatsApp**: funzionanti, agenzia Voltabarozzo

## Stack

- HTML statico single file (`index.html`)
- Tailwind CSS via Play CDN
- Alpine.js v3 + plugin `collapse` (lightbox planimetria, accordion FAQ)
- lite-youtube-embed (embed video performante)
- Font Inter Figtree (font ufficiale Tettorosso)
- Nessun build system

## Struttura

```
lisieux-lp/
├── index.html
├── _headers              # Cloudflare Pages headers (noindex, cache, security)
├── robots.txt            # Disallow totale
├── .gitignore
├── README.md
├── assets/
│   ├── img/
│   │   ├── hero-rendering.jpg     # 1536x1024, 297KB
│   │   ├── og-image.jpg           # 1200x630, 156KB
│   │   ├── pianta-tipo-trilocale.jpg  # render 3D arredato trilocale piano primo
│   │   ├── mappa-zona.jpg         # 1074x720, 261KB
│   │   └── logo-tettorosso.svg    # logo ufficiale (3.3KB)
│   └── pdf/
│       └── capitolato-lisieux.pdf  # capitolato ufficiale (archivio, non linkato)
└── source/               # NON deployata (.gitignore) — sorgenti originali
```

Peso totale assets pubblicati: ~1.4 MB.

## Brand identity (estratta dal sito Tettorosso)

- **Rosso primario**: `#E73C3E` (dal logo SVG ufficiale)
- **Rosso scuro hover**: `#C8302C`
- **Testo dark**: `#3C3C3C`
- **Background warm**: `#F5F4F0`
- **Border**: `#E5E5E5`
- **Font**: `Figtree` (font del sito Tettorosso live)

## Sezioni

1. Header sticky (logo + CTA)
2. Hero rendering edificio + CTA primaria/secondaria
3. Video YouTube (placeholder ID `c_-CclcT1L0` — sostituibile)
4. Quattro motivi (USP differenziali)
5. Tre tipologie (quadrilocale terra, trilocale, quadrilocale terrazza)
6. La pianta — render 3D unico, lightbox zoomabile
7. Capitolato in linguaggio acquirente (8 blocchi)
8. Dove si trova (mappa + link Google Maps)
9. Classe energetica A4 (scala APE visuale)
10. FAQ accordion (8 domande)
11. Contatti (form template + box agenzia + WhatsApp CTA)
12. Footer (4 sedi Tettorosso)

## Deploy su Cloudflare Pages

### Opzione A — Via Wrangler (locale)

```bash
cd lisieux-lp
wrangler pages deploy . --project-name=lisieux
```

URL produzione: `https://tettorossonuovecostruzioni.it` (preview Pages: `https://lisieux.pages.dev`)

### Opzione B — Via GitHub + Cloudflare Dashboard

1. Push del repo su `Moreno-005/lisieux-lp`
2. Cloudflare Dashboard → Pages → Create Project → Connect to Git
3. Selezionare repo, branch `main`
4. Build settings: nessuno (sito statico)
5. Output directory: `/` (root)

## Modifica video YouTube

Sostituire `c_-CclcT1L0` nel tag `<lite-youtube videoid="...">` (sezione 6.3) con l'ID del video reale.

## Aggiungere planimetria piano terra

Quando disponibile:
1. Convertire in JPG q88, dimensione comparabile (~2000px lato lungo)
2. Salvare in `assets/img/planimetria-piano-terra.jpg`
3. Decommentare il blocco placeholder nella sezione 6.6 (è presente come commento HTML)

## Sostituire le immagini

```bash
# Hero (rendering edificio)
magick nuovo-hero.png -resize '1920x1920>' -quality 85 -strip assets/img/hero-rendering.jpg
magick nuovo-hero.png -resize '1200x630^' -gravity center -extent 1200x630 -quality 85 -strip assets/img/og-image.jpg

# Planimetria (render 3D)
magick nuova-planimetria.png -resize '2000x2000>' -quality 90 -strip assets/img/planimetria.jpg
```

## Contatti agenzia

- **Tettorosso Immobiliare — Voltabarozzo**
- Via Piovese, 276 — 35127 Padova
- Tel: 049 636 7877 / WhatsApp: +39 049 636 7877
- voltabarozzo@tettorossoimmobiliare.it
- Lun-Ven: 9:00-12:30 / 15:00-19:30, Sab: 9:00-12:30

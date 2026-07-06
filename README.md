<p align="center">
  <img src="assets/preview.webp" alt="Sitio de TAIRIK" width="840">
</p>

<h1 align="center">TAIRIK</h1>
<p align="center"><b>Sitio editorial one-pager · by ShowUp</b></p>
<p align="center"><a href="https://t4irik.cl"><b>🔗 t4irik.cl</b></a></p>
<p align="center">
  <img src="https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white">
  <img src="https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white">
  <img src="https://img.shields.io/badge/Canvas-cuenta%20regresiva-000000">
  <img src="https://img.shields.io/badge/Vercel-deploy-000000?logo=vercel">
</p>

> Estética dossier con portada "DOSIER · 001", contador en vivo y partículas en canvas. Sin
> frameworks: un solo archivo, máximo rendimiento.

---

Sitio one-pager de **Tairik (Maximiliano Román)** — prensa, explainer y host de [shisi.news](https://shisi.news).

## Stack

- HTML + CSS + JS vanilla, un solo archivo (`index.html`).
- Hosting estático en **Vercel**.
- Videos servidos directo desde `/assets/videos/` (mp4 comprimidos con ffmpeg, CRF 28).

## Estructura

```
.
├── index.html          # Sitio completo (estilo + script inline)
├── vercel.json         # Headers de seguridad + cache rules
├── .gitignore
├── README.md
└── assets/
    ├── tairik-hero.jpg # Hero del bloque inicial (1000px ancho)
    ├── videos/         # Reels y entrevistas (.mp4)
    └── thumbs/         # Posters de los videos (.jpg)
```

## Desarrollo local

No hay build step. Servís estático con cualquiera de estos:

```bash
# Python
python -m http.server 8000

# Node (npx, sin install)
npx serve

# PHP
php -S localhost:8000
```

Abrí `http://localhost:8000`.

## Deploy

### Vercel CLI

```bash
npm i -g vercel
vercel        # Preview
vercel --prod # Producción
```

### Desde el dashboard

1. Importar repo de GitHub en [vercel.com/new](https://vercel.com/new).
2. Framework Preset: **Other** (es estático).
3. Build/Output: dejar vacío (no necesita build).
4. Deploy.

### URL canónica

Todas las URLs absolutas de `index.html` (canonical, OG, Twitter, JSON-LD), `robots.txt` y
`sitemap.xml` apuntan al dominio final **https://www.t4irik.cl**. Si el dominio cambia, reemplazar
en los tres archivos:

```powershell
(Get-Content index.html) -replace 'www\.t4irik\.cl','dominio-nuevo.cl' | Set-Content index.html
```

## Reemplazar/agregar videos

1. Dejar el `.mp4` nuevo en `assets/videos/` con nombre kebab-case (`viral-4.mp4`).
2. Dejar el poster en `assets/thumbs/` con el mismo nombre (`viral-4.jpg`).
3. Comprimir antes (importante para BW):

   ```bash
   ffmpeg -i original.mp4 \
     -vf "scale=540:960:force_original_aspect_ratio=decrease" \
     -c:v libx264 -preset slow -crf 28 -profile:v high -pix_fmt yuv420p \
     -c:a aac -b:a 96k -movflags +faststart \
     viral-4.mp4
   ```

4. Agregar el bloque `<article class="vid-slot">` correspondiente en `index.html` (ver virales/entrevistas).

## Booking

`t4irik@gmail.com` · Santiago, Chile

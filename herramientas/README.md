# Herramientas

Plantillas para generar las imágenes de la web. No se publican (están en `.vercelignore`). Se usan Chrome, `sips` y `cwebp`/`ffmpeg`, que ya están en el Mac. Sin dependencias nuevas.

Los comandos se ejecutan desde la raíz de este repositorio.

## Foto de la portada

Se genera desde el original de `laura-sales-closer/07-fotos/laura-foto-perfil.jpg`, que **nunca se modifica**: se copia a una carpeta temporal y se trabaja sobre la copia.

Recorte 4:5 (960 × 1200 desde x=150, y=0), sin retoque, en 480 y 800 px de ancho y en AVIF, WebP y JPEG:

```bash
T=$(mktemp -d); cp ../laura-sales-closer/07-fotos/laura-foto-perfil.jpg "$T/orig.jpg"
sips -c 1200 960 --cropOffset 0 150 "$T/orig.jpg" --out "$T/crop.jpg"
for w in 480 800; do h=$((w*5/4)); sips -z $h $w "$T/crop.jpg" -s format png --out "$T/$w.png"; sips -s format jpeg -s formatOptions 82 "$T/$w.png" --out recursos/img/laura-martinez-galvez-$w.jpg; cwebp -quiet -q 80 "$T/$w.png" -o recursos/img/laura-martinez-galvez-$w.webp; sips -s format avif -s formatOptions 60 "$T/$w.png" --out recursos/img/laura-martinez-galvez-$w.avif; done
```

## Imagen para compartir en redes (Open Graph, 1200 × 630)

`imagen-redes.html` (español) e `imagen-redes.html?fr` (francés). Regenerarla si cambia el titular o la foto:

```bash
C="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"; T=$(mktemp -d)
"$C" --headless=new --hide-scrollbars --window-size=1200,630 --virtual-time-budget=3000 --screenshot="$T/es.png" "file://$PWD/herramientas/imagen-redes.html"
"$C" --headless=new --hide-scrollbars --window-size=1200,630 --virtual-time-budget=3000 --screenshot="$T/fr.png" "file://$PWD/herramientas/imagen-redes.html?fr"
sips -s format jpeg -s formatOptions 85 "$T/es.png" --out recursos/img/og-es.jpg
sips -s format jpeg -s formatOptions 85 "$T/fr.png" --out recursos/img/og-fr.jpg
```

## Icono

`icono.html` → `apple-touch-icon.png` (180 px) y `favicon.ico` (32 px). `favicon.svg` se edita a mano.

```bash
C="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"
"$C" --headless=new --hide-scrollbars --window-size=180,180 --virtual-time-budget=3000 --screenshot="$PWD/apple-touch-icon.png" "file://$PWD/herramientas/icono.html"
ffmpeg -loglevel error -y -i apple-touch-icon.png -vf scale=32:32:flags=lanczos favicon.ico
```

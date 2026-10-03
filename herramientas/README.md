# Herramientas

Plantillas para generar las imágenes de la web. No se publican (están en `.vercelignore`). Se usan Chrome, `sips`, `cwebp`/`dwebp` y `ffmpeg`, que ya están en el Mac. Sin dependencias nuevas.

Los comandos se ejecutan desde la raíz de este repositorio.

## Foto de la portada

Se genera desde `../laura-sales-closer/07-fotos/laura-foto-perfil-sin-fondo.png` (1200 × 1200, con el fondo ya quitado), que **nunca se modifica**: se copia a una carpeta temporal y se trabaja sobre la copia. El difuminado del borde inferior no está en la imagen: lo pone el CSS (`mask-image` en `.retrato img`).

Recorte 4:5 (960 × 1200 desde x=202, y=0), sin retoque, en 480 y 800 px de ancho y en WebP y PNG, los dos con transparencia y sin los metadatos de Canva que trae el original. Sin AVIF: `sips` guarda la transparencia de forma que Chrome y Firefox no la reconocen y pintan el fondo negro. El PNG se saca de un WebP sin pérdida porque `dwebp` no copia metadatos:

```bash
T=$(mktemp -d); cp ../laura-sales-closer/07-fotos/laura-foto-perfil-sin-fondo.png "$T/orig.png"
sips -c 1200 960 --cropOffset 0 202 "$T/orig.png" --out "$T/crop.png"
for w in 480 800; do h=$((w*5/4)); sips -z $h $w "$T/crop.png" --out "$T/$w.png"; cwebp -quiet -q 80 -alpha_q 90 "$T/$w.png" -o recursos/img/laura-martinez-galvez-$w.webp; cwebp -quiet -lossless "$T/$w.png" -o "$T/$w-ll.webp"; dwebp -quiet "$T/$w-ll.webp" -o recursos/img/laura-martinez-galvez-$w.png; done
```

La foto anterior, con fondo, se guarda como `laura-martinez-galvez-con-fondo-*` (AVIF, WebP y JPEG). La web ya no la usa.

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

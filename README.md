# Web profesional de Laura Martínez Gálvez

Tu web personal para recruiters y empresas: quién eres, qué resultados tienes, cómo vendes y cómo contactar contigo. En español y en francés.

- **Dirección:** https://lauramartinezgalvez.com (cuando el dominio esté conectado).
- **Se publica sola:** cada cambio que se sube a GitHub aparece en la web en uno o dos minutos (Vercel).

## Qué hay en la web

1. Portada: tu nombre, tu posicionamiento y tu foto.
2. Resultados: primera en ventas de tu equipo al cierre de 2025, aprox. 52.000 € en ventas, +8 años de experiencia comercial y español y francés.
3. Cómo vendes, en cuatro pasos.
4. Tres situaciones reales: el colegio, los clientes holandeses y el ventilador que de verdad ventila.
5. Experiencia, formación e idiomas.
6. Contacto: email y LinkedIn. **Sin teléfono y sin CV descargable**: el CV se pide por email, y así envías el adaptado a cada empresa.

## De dónde sale cada texto

Todo sale de tu repositorio de búsqueda de empleo (`laura-sales-closer`): perfil, cifras, historias y formación. Aquí no se inventa nada.

- [textos-web.md](textos-web.md): todos los textos de la web, con la fuente de cada uno. **Si un texto cambia, se cambia ahí primero.**
- Si cambia algo en tu perfil (una formación terminada, una cifra nueva), hay que revisar también la web. Pídeselo a Claude: "He terminado HubSpot, actualiza la web".

## Qué pedirle a Claude

| Quiero… | Pídele |
|---|---|
| Cambiar un texto | "En la web, cambia [esto] por [esto]" |
| Añadir algo nuevo | "He terminado el curso X, añádelo a la web" |
| Ver cómo queda antes de publicar | "Enséñame la web en el móvil" |

## Qué hay en cada archivo

No hace falta abrir nada de esto; está aquí por si tienes curiosidad.

| Archivo o carpeta | Qué es |
|---|---|
| `index.html` | La web en español |
| `fr/index.html` | La web en francés |
| `recursos/` | El diseño (`estilos.css`), las tipografías y tus fotos optimizadas para la web |
| `textos-web.md` | Los textos aprobados y su fuente |
| `herramientas/` | Plantillas para generar la imagen de redes y el icono |
| `favicon.*`, `apple-touch-icon.png` | El icono de la pestaña del navegador |
| `robots.txt`, `sitemap.xml` | Le dicen a Google qué páginas hay |
| `vercel.json` | Ajustes de la publicación |
| `404.html` | La página que sale si alguien escribe mal la dirección |

## Privacidad

- La web no usa cookies ni herramientas de seguimiento.
- Solo publica tu email profesional, tu ciudad y tu LinkedIn. Nunca el teléfono.
- Las tipografías se sirven desde la propia web, no desde Google.
- Este repositorio es **público**: aquí no se guardan datos personales ni notas internas.

## Estado (2026-10-03)

- ✅ Textos aprobados por Laura en español y francés.
- ✅ Web maquetada y revisada en escritorio y móvil.
- ⏳ Publicarla en Vercel (cuenta de Laura). Mientras la dirección sea la provisional de Vercel, Google no la indexa.
- ⏳ Conectar el dominio `lauramartinezgalvez.com` (lo compra Donato en Cloudflare).
- ⏳ Después: añadir la web a LinkedIn (información de contacto) y a la firma del email.

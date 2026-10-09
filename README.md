# Web de Alma Norel · Cuentos para Imaginar

Web estática (solo HTML + CSS, sin JavaScript ni paso de compilación) para la colección
**Cuentos para Imaginar** de Alma Norel. Se publica en GitHub Pages con el dominio
propio **almanorel.com**.

## Estructura

```
/
├── index.html          → redirige a /cuentos/
├── cuentos/index.html  → página principal (destino del QR: https://almanorel.com/cuentos)
├── 404.html            → página de error
├── assets/style.css    → estilos (fuentes del sistema, nada de terceros)
├── assets/favicon.svg
├── assets/img/         → ilustraciones (webp + jpg; versiones -800/-480 más ligeras para móvil)
├── CNAME               → contiene exactamente: almanorel.com
├── .nojekyll           → indica a GitHub Pages que no procese con Jekyll
└── preview-*.png       → capturas de vista previa (se pueden borrar antes de publicar)
```

> Importante: el QR del libro apunta a `https://almanorel.com/cuentos`. No cambies el nombre
> de la carpeta `cuentos/` ni muevas `cuentos/index.html`.

## Ver la web en local

Las rutas son absolutas (`/assets/style.css`), así que hay que abrirla con un servidor:

```bash
cd web-almanorel
python3 -m http.server 8000
# abrir http://localhost:8000/cuentos/
```

## Publicar en GitHub Pages

1. Crea un repositorio en GitHub (por ejemplo `almanorel-web`), público.
2. Sube **el contenido** de esta carpeta a la raíz de la rama `main`
   (que `index.html`, `CNAME` y `cuentos/` queden en la raíz del repositorio).
3. En el repositorio: **Settings → Pages**.
   - *Source*: **Deploy from a branch**.
   - *Branch*: `main` y carpeta `/ (root)`. Guardar.
4. En **Custom domain** escribe `almanorel.com` y guarda (el archivo `CNAME` ya lo incluye).
5. Cuando el DNS esté propagado y GitHub haya emitido el certificado, marca **Enforce HTTPS**.
6. Recomendado: verifica el dominio en tu cuenta (**Settings de tu perfil u organización →
   Pages → Add a domain**) para evitar que otra persona pueda usarlo. GitHub te dará un
   registro TXT que tendrás que añadir en el DNS.

## Registros DNS (en el proveedor del dominio almanorel.com)

Dominio raíz (`almanorel.com`, a veces se escribe `@`):

| Tipo | Nombre | Valor |
|------|--------|-------|
| A    | @ | 185.199.108.153 |
| A    | @ | 185.199.109.153 |
| A    | @ | 185.199.110.153 |
| A    | @ | 185.199.111.153 |
| AAAA | @ | 2606:50c0:8000::153 |
| AAAA | @ | 2606:50c0:8001::153 |
| AAAA | @ | 2606:50c0:8002::153 |
| AAAA | @ | 2606:50c0:8003::153 |

Subdominio `www` (para que `www.almanorel.com` también funcione y redirija):

| Tipo  | Nombre | Valor |
|-------|--------|-------|
| CNAME | www | `TU-USUARIO.github.io` (sustituye por tu usuario u organización de GitHub, sin el nombre del repositorio) |

Notas:
- Borra cualquier otro registro A/AAAA/CNAME antiguo de `@` o `www` que apunte a otro sitio
  (por ejemplo, a una página de "aparcamiento" del registrador).
- No toques los registros MX si usas el correo `hola@almanorel.com`.
- La propagación del DNS puede tardar desde minutos hasta 24–48 horas.
- Comprueba con: `dig almanorel.com +short` y `dig www.almanorel.com +short`.
- Consulta la documentación oficial por si GitHub actualiza estas IPs:
  https://docs.github.com/es/pages/configuring-a-custom-domain-for-your-github-pages-site

## Pendientes

- Añadir los botones "Comprar en Amazon" y "Leer en Kindle" en la tarjeta de
  "Ardi y la casita secreta" (`cuentos/index.html`, hay comentarios HTML marcando el lugar
  exacto) y cambiar entonces la etiqueta "En preparación".
- "Navidad para imaginar" (actividades para colorear) está marcada "En preparación": añadir
  su enlace cuando esté listo (hay un comentario HTML en su sección). Sin PDF ni dibujos sueltos.
- No subir PDFs de los libros a esta web.
- Si se cambian las ilustraciones, regenerar también las versiones reducidas
  (`ardi-banner-800`, `animales-banner-800`, `ardi-vertical-480`, `libro-vertical-480`, en
  .webp y .jpg) y mantener los nombres; `og:image` apunta a
  `https://almanorel.com/assets/img/ardi-banner.jpg`.
- Borrar `preview-mobile.png` y `preview-desktop.png` antes de publicar (opcional).

## Privacidad

La web no usa cookies, formularios, analíticas, rastreadores ni fuentes externas.
No recoge ningún dato personal.

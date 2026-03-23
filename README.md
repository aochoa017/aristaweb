# AristaWeb

Landing page pública de **AristaWeb** — hosting gestionado, mantenimiento WordPress y consultoría web para autónomos en España.

---

## Estructura del proyecto

```
aristaweb/
├── index.html      # Landing page principal
├── style.css       # Hoja de estilos (sin dependencias externas)
├── favicon.svg     # Favicon SVG
├── robots.txt      # Instrucciones para crawlers
├── sitemap.xml     # Sitemap (actualizar con el dominio real)
└── README.md       # Este archivo
```

---

## Previsualizar localmente

No necesitas instalar nada. Abre el proyecto con cualquiera de estos métodos:

### Opción A — Python (la más rápida)

```bash
# Python 3
python -m http.server 8000

# Python 2 (si no tienes Python 3)
python -m SimpleHTTPServer 8000
```

Luego abre [http://localhost:8000](http://localhost:8000) en tu navegador.

### Opción B — Node.js (`npx serve`)

```bash
npx serve .
```

### Opción C — VS Code + extensión Live Server

Instala la extensión [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) y haz clic en **"Go Live"** en la barra inferior.

---

## Despliegue

### Opción 1 — GitHub Pages (gratis, ideal para empezar)

1. Ve a **Settings → Pages** en el repositorio de GitHub.
2. Selecciona la rama `main` y la carpeta raíz (`/`).
3. GitHub publicará el sitio en `https://<usuario>.github.io/<repositorio>/`.

> ⚠️ Para repos privados, GitHub Pages requiere GitHub Pro o superior.

### Opción 2 — DigitalOcean (producción)

Sube los ficheros al servidor con `rsync` o `scp`:

```bash
rsync -avz --delete ./ usuario@tu-servidor:/var/www/aristaweb/
```

Configura Nginx para servir el directorio, por ejemplo:

```nginx
server {
    listen 80;
    server_name domain-name.es www.domain-name.es;
    root /var/www/aristaweb;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

---

## Añadir dominio más adelante

1. **Compra el dominio** (p. ej. `domain-name.es`) en un registrador como Namecheap, Porkbun o Nominalia.
2. **Actualiza los registros DNS** apuntando al servidor (registro `A` a la IP del droplet).
3. **Añade SSL con Certbot** (Let's Encrypt):

   ```bash
   certbot --nginx -d domain-name.es -d www.domain-name.es
   ```

4. **Actualiza el sitio**:
   - Reemplaza `REPLACE_WITH_YOUR_DOMAIN` en `robots.txt` y `sitemap.xml`.
   - Añade `<link rel="canonical" href="https://domain-name.es/">` en el `<head>` de `index.html`.
   - Añade `og:url` en los metadatos Open Graph.

---

## Personalización rápida

| Placeholder | Dónde | Descripción |
|---|---|---|
| `contacto@domain-name.es` | `index.html` | Email de contacto real |
| `https://calendly.com/REPLACE_ME` | `index.html` | URL de Calendly para reservar llamadas |
| `https://wa.me/REPLACE_ME` | `index.html` | Número de WhatsApp (formato internacional sin `+`, ej. `34600000000`) |
| `REPLACE_WITH_YOUR_DOMAIN` | `robots.txt`, `sitemap.xml` | Dominio real cuando esté disponible |

---

## Licencia

Uso privado. © 2025 AristaWeb.

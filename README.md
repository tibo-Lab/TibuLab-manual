# TibuLab User Manual

The end-user manual for TibuLab: one static page (`index.html`) plus screenshots (`img/`). It has no build step and no server code. Any web server, or a double-click on `index.html`, opens it.

It lives apart from the app repository (`TibuLab`), so screenshots and text can change without touching the app.

## Where it is used

The app's **Help** button (top bar) opens the address in the app's `.env`:

```dotenv
TIBULAB_MANUAL_URL=https://docs.tibulab.com     # default: the published manual
```

| Install | Value | How the manual is served |
|---|---|---|
| Cloud (tibulab.com) | `https://docs.tibulab.com` | This repository published as a static site (GitHub Pages, Netlify, or a folder on the VPS). |
| Local server with internet | leave the default | The published manual. |
| Local server **offline** | `/manual/` | Copy this folder onto the server and add an Apache `Alias` (below). |

Apache alias (inside the TibuLab `<VirtualHost>`, before `DocumentRoot` rules apply). Replace `/path/to/TibuLab-manual` with the folder where you copied the manual:

```apache
Alias /manual "/path/to/TibuLab-manual"
<Directory "/path/to/TibuLab-manual">
    Require all granted
</Directory>
```

Restart Apache after adding it.

## Editing

- Text: edit `index.html`. Each section is a `<section class="doc" id="…">` with a matching link in the sidebar (`<nav class="toc">`).
- Pictures: `img/<area>-<screen>.jpg`, about 1366×768, JPEG quality around 75, under ~150 KB each. Take them from the **demo lab** only (made-up patients), never from a real lab.
- Use the exact button labels the app shows, and describe only what exists in the app.
- Check after a change: open the page at desktop and phone width; every image must load and there must be no sideways scrolling.

## Publish

Push this repository and serve its root as a static site, e.g. GitHub Pages (branch `main`, folder `/`), with the custom domain `docs.tibulab.com`.

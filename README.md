# Mi Organizador — Deploy en GitHub Pages

App de productividad personal con sincronización en Google Drive.
Login con Google real, sin tokens manuales.

---

## Paso 1 — Crear repo en GitHub

1. Abrí [github.com/new](https://github.com/new)
2. Nombre: `mi-organizador` (o el que quieras)
3. Marcá **Public**
4. Hacé clic en **Create repository**

---

## Paso 2 — Subir los archivos

Desde la carpeta de este proyecto, en tu terminal:

```bash
git init
git add .
git commit -m "primer commit"
git branch -M main
git remote add origin https://github.com/TU_USUARIO/mi-organizador.git
git push -u origin main
```

---

## Paso 3 — Activar GitHub Pages

1. En tu repo → **Settings** → **Pages**
2. Source: **Deploy from a branch**
3. Branch: `main` / `/ (root)`
4. Guardá. En ~2 minutos tu app va a estar en:
   `https://TU_USUARIO.github.io/mi-organizador/`

---

## Paso 4 — Crear credenciales de Google

1. Abrí [console.cloud.google.com](https://console.cloud.google.com)
2. Creá un proyecto nuevo (o usá uno existente)
3. **APIs & Services** → **Enable APIs** → habilitá **Google Drive API**
4. **APIs & Services** → **Credentials** → **Create Credentials** → **OAuth client ID**
5. Application type: **Web application**
6. Nombre: `Mi Organizador`
7. En **Authorized JavaScript origins** agregá:
   ```
   https://TU_USUARIO.github.io
   ```
8. En **Authorized redirect URIs** agregá:
   ```
   https://TU_USUARIO.github.io/mi-organizador/
   ```
9. Hacé clic en **Create** → copiá el **Client ID** (termina en `.apps.googleusercontent.com`)

---

## Paso 5 — Pegar el Client ID en la app

Abrí `index.html` y buscá esta línea cerca del final:

```javascript
const CLIENT_ID  = '__GOOGLE_CLIENT_ID__';
```

Reemplazá `__GOOGLE_CLIENT_ID__` con tu Client ID real:

```javascript
const CLIENT_ID  = '123456789-abc.apps.googleusercontent.com';
```

Guardá y volvé a hacer push:

```bash
git add index.html
git commit -m "agrego client id"
git push
```

---

## Listo 🎉

Abrí `https://TU_USUARIO.github.io/mi-organizador/`, hacé clic en
**Entrar con Google**, autorizá una sola vez y tu app queda conectada.

- Los datos se guardan automáticamente en **organizador-datos.json** en tu Drive
- El login dura semanas (refresh token automático)
- Funciona desde cualquier dispositivo con el mismo Google

---

## Problemas frecuentes

| Error | Solución |
|---|---|
| `redirect_uri_mismatch` | Verificá que la URI en Google Console coincida exactamente con tu URL de GitHub Pages (con `/` al final) |
| `Access blocked` | El proyecto en Google Console puede necesitar estar en modo "Testing" con tu email como usuario de prueba |
| No carga después del login | Abrí DevTools (F12) → Console y fijate el error |

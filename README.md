# Accesos Remotos Carel - Frisertec (Prototipo)

Sitio estático (HTML + Tailwind CDN) que muestra un panel de accesos remotos.
**Este repo usa datos de ejemplo (placeholder)**, no credenciales reales.

## ⚠️ Antes de usar datos reales

El "Admin Login" de este prototipo es solo una capa visual: todos los datos
en `ACCESS_DATA` (dentro de `index.html`) se descargan al navegador de
cualquier visitante, esté logueado o no. **No reemplaces los placeholders
por credenciales reales de clientes en este archivo estático.**

Para producción con datos reales, mover `ACCESS_DATA` a un backend
(por ejemplo, una API Route de Vercel + autenticación real) que solo
entregue las credenciales a usuarios ya autenticados en el servidor.

## Subir a GitHub

```bash
cd frisertec-accesos
git init
git add .
git commit -m "Prototipo panel de accesos remotos"
git branch -M main
git remote add origin https://github.com/TU_USUARIO/TU_REPO.git
git push -u origin main
```

## Desplegar en Vercel

Opción 1 — Dashboard:
1. Entra a https://vercel.com/new
2. Importa el repositorio de GitHub que acabas de crear.
3. Framework Preset: "Other" (sitio estático). No necesita build command.
4. Deploy.

Opción 2 — CLI:
```bash
npm i -g vercel
cd frisertec-accesos
vercel
```

## Estructura
```
frisertec-accesos/
├── index.html      # Sitio completo (HTML + CSS + JS embebido)
├── vercel.json      # Config mínima para Vercel
├── .gitignore
└── README.md
```

## Responsive
El grid usa Tailwind (`grid-cols-1` en móvil, hasta `xl:grid-cols-4` en
pantallas grandes), el buscador y el modal se adaptan al ancho de pantalla.
Se probó visualmente en anchos de móvil (~375px), tablet y desktop.

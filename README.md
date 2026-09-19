# Frisertec - Accesos Remotos & Reportes (Prototipo)

Sitio estático (HTML + Tailwind CDN) con dos partes integradas:

1. **Provincias → Locales**: sidebar con las 24 provincias de Ecuador
   (Guayas por defecto). En escritorio queda siempre visible a la
   izquierda; en móvil se abre con el botón del mapa (arriba a la
   izquierda). Al elegir una provincia, el centro muestra sus locales.
2. **Detalle del local**: al hacer clic en un local se abre su ficha de
   acceso (credenciales tras Admin Login) y, debajo, su **historial de
   reportes** completo — no un solo reporte, sino todos los que se han
   creado para ese local a lo largo del tiempo.

Cada reporte incluye: código autogenerado, tipo (emergencia/mantenimiento),
fecha, hora de entrada/salida (selector nativo; se muestra en 12h AM/PM),
personal asignado (antes del problema), problema reportado, reparación,
implementos e imágenes opcionales. Desde el detalle se puede **descargar PDF**.

**Permisos:** sin login solo se ven los reportes; con Admin Login se puede
crear, editar y eliminar. La provincia y el local se toman del local actual.

**Todos los datos (locales y el reporte de ejemplo) son placeholders.**

## ⚠️ Antes de usar datos reales

- El "Admin Login" de Accesos Remotos es solo una capa visual: todos los
  datos en `ACCESS_DATA` (dentro de `index.html`) se descargan al navegador
  de cualquier visitante, esté logueado o no. **No reemplaces los
  placeholders por credenciales reales de clientes en este archivo
  estático.** Para producción, mover `ACCESS_DATA` a un backend con
  autenticación real (ej. API Route de Vercel + JWT/sesión).

- Los **Reportes** se guardan en `localStorage` del navegador: son locales a
  ese dispositivo/navegador, no se comparten entre usuarios ni dispositivos,
  y tienen un límite de tamaño (~5-10 MB), fácil de superar si se suben
  muchas fotos. Para un uso real (varios técnicos, varios dispositivos,
  historial que no se pierda al borrar caché) se necesita un backend real:
  API + base de datos + almacenamiento de archivos (ej. Vercel + Postgres/
  Supabase + Vercel Blob o S3).

- Las imágenes de los reportes se guardan tal cual las entrega el navegador
  (sin recomprimir), para no perder su metadata original (fecha de captura,
  GPS si el celular la incluyó). Esa metadata se intenta leer con la
  librería EXIF.js solo para mostrarla en el detalle del reporte; no todos
  los formatos/celulares la incluyen.

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

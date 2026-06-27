# Isla Pelele · Catálogo de cartas coleccionables

Aplicación web de catálogo de cartas coleccionables **personalizadas**,
inspirada visualmente en los juegos de cartas tipo TCG pero **sin usar ningún
recurso oficial de terceros**. Todo el contenido (imágenes, nombres, datos) es
propio y vive en archivos locales.

Construida con **Next.js (App Router) + React + TypeScript + TailwindCSS**.

## ✨ Características

- Flujo de 4 pantallas: inicio → personaje → colección → cartas → detalle.
- Datos 100 % locales: sin base de datos ni APIs externas.
- Añadir una carta = copiar un PNG + añadir una línea de JSON.
- Modo oscuro / claro con conmutador.
- Cuadrícula responsive (móvil y escritorio).
- Cartas con inclinación 3D y brillo holográfico según la rareza.
- Código modular y tipado, preparado para crecer (buscador, filtros,
  favoritos, más colecciones y personajes) sin reorganizar el proyecto.

## 📁 Estructura del proyecto

```
isla-pelele-tcg/
├── app/                      # Rutas (App Router)
│   ├── layout.tsx            # Layout raíz: fuentes, providers, cabecera
│   ├── page.tsx              # Pantalla 1 · Inicio + selección de personaje
│   ├── providers.tsx         # Providers de cliente (tema + personaje)
│   ├── not-found.tsx         # Página 404
│   ├── colecciones/
│   │   └── page.tsx          # Pantalla 2 · Selección de colección
│   └── cartas/
│       ├── page.tsx          # Pantalla 3 · Cuadrícula de cartas
│       └── [id]/
│           └── page.tsx      # Pantalla 4 · Detalle de carta
├── components/               # Componentes reutilizables de UI
├── context/                  # React Context (personaje seleccionado)
├── hooks/                    # Hooks personalizados (useCharacter)
├── lib/                      # Acceso a datos tipado (cartas, colecciones…)
├── data/                     # Datos en JSON (la fuente de la verdad)
│   ├── cards.json
│   ├── collections.json
│   └── characters.json
├── types/                    # Tipos TypeScript del dominio
├── styles/                   # CSS global y variables de tema
└── public/                   # Imágenes locales
    ├── cards/                # 001.png, 002.png, ...
    ├── collections/          # isla_pelele.png
    └── characters/           # personaje_a.png, personaje_b.png
```

## 🚀 Instalación

Requisitos: **Node.js 18.18 o superior** y npm.

```bash
npm install
```

## ▶️ Ejecutar en local

```bash
npm run dev
```

Abre <http://localhost:3000> en el navegador. El servidor recarga
automáticamente al guardar cambios.

Otros comandos:

```bash
npm run build   # compila para producción
npm start       # sirve la compilación de producción
npm run lint    # comprueba el código
```

## 🃏 Cómo añadir una carta nueva

Solo dos pasos, sin tocar el código:

1. **Copia tu PNG** dentro de `public/cards/`, por ejemplo `public/cards/013.png`.

2. **Añade una línea** al array de `data/cards.json`:

   ```json
   {
     "id": 13,
     "numero": "013",
     "nombre": "Mi carta nueva",
     "rareza": "Común",
     "tipo": "Objeto",
     "coleccion": "isla_pelele",
     "imagen": "/cards/013.png"
   }
   ```

   - `id`: número único (no repetir).
   - `numero`: texto, conserva los ceros (`"013"`).
   - `rareza`: una de `Común`, `Poco común`, `Rara`, `Épica`, `Legendaria`
     (controla el color y el brillo holográfico).
   - `tipo`: libre (`Criatura`, `Objeto`, `Energía`, `Hechizo`, `Terreno`…).
   - `coleccion`: el `id` de una colección de `data/collections.json`.
   - `imagen`: la ruta dentro de `public` (empieza por `/`).

La carta aparece automáticamente en la cuadrícula y obtiene su propia página
de detalle. No hace falta reiniciar nada en desarrollo.

> Las imágenes recomendadas son verticales (proporción 5:7, p. ej. 500×700 px).
> La app recorta al encajar, así que cualquier PNG funciona.

## 🗂️ Cómo modificar el JSON

- **Cartas** → `data/cards.json`
- **Colecciones** → `data/collections.json` (añade aquí nuevas colecciones)
- **Personajes** → `data/characters.json` (añade aquí más personajes)

Los tipos en `types/index.ts` describen la forma exacta de cada objeto, así que
tu editor te avisará si falta un campo.

## ☁️ Cómo desplegar en Vercel

1. Sube el proyecto a GitHub (ver más abajo).
2. Entra en <https://vercel.com> e inicia sesión.
3. **Add New… → Project** e importa tu repositorio.
4. Vercel detecta Next.js automáticamente: no cambies ninguna opción.
5. Pulsa **Deploy**.

No hay variables de entorno ni configuración extra: el proyecto funciona tal
cual, porque todo es local.

## 🐙 Cómo subir el proyecto a GitHub

```bash
git init
git add .
git commit -m "Primera versión de Isla Pelele"
git branch -M main
git remote add origin https://github.com/TU_USUARIO/TU_REPO.git
git push -u origin main
```

(El `.gitignore` ya excluye `node_modules`, `.next` y archivos de entorno.)

## 🔮 Preparado para el futuro

La estructura ya está pensada para crecer sin reorganizar nada:

- **Más colecciones**: añade una entrada en `collections.json` y crea las
  cartas con su `coleccion` correspondiente.
- **Más personajes**: añade una entrada en `characters.json`.
- **Buscador / filtros**: añade la lógica sobre `lib/cards.ts` (ya devuelve
  arrays tipados) y un componente de UI; los datos no cambian.
- **Favoritos / colección propia**: añade un nuevo Context dentro de
  `app/providers.tsx`, igual que `CharacterProvider`.

## 📝 Notas

- Las imágenes incluidas son marcadores de posición generados; sustitúyelas por
  tu propio arte cuando quieras.
- No se usa ningún recurso, nombre ni logotipo oficial de ninguna marca.

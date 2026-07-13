# my_webpage

Código fuente de la web personal de **Álvaro Zorrilla Carriquí**, generada con [Quarto](https://quarto.org/) y publicada en GitHub Pages: https://azcarriqui77.github.io/my_webpage/

## Requisitos

- [Quarto CLI](https://quarto.org/docs/get-started/) (>= 1.8)
- Opcional: [R](https://www.r-project.org/) — el workflow de publicación instala `rmarkdown`, aunque el sitio no depende de código R en la actualidad

## Levantar la web en local

Desde la raíz del repositorio:

```sh
quarto preview
```

Esto compila el sitio y abre un navegador con recarga automática al guardar cambios en cualquier `.qmd`, `.scss` o `.css`.

Para generar el sitio estático sin servidor de desarrollo (se genera en `_site/`, ignorado por git):

```sh
quarto render
```

## Despliegue

El sitio se publica automáticamente en **GitHub Pages** mediante GitHub Actions ([.github/workflows/publish.yml](.github/workflows/publish.yml)): cada `push` a `main` dispara un workflow que renderiza el proyecto con Quarto y despliega el resultado. No hace falta ningún paso manual — basta con hacer commit y push a `main`. El progreso puede seguirse en la pestaña [Actions](https://github.com/azcarriqui77/my_webpage/actions) del repositorio.

## Estructura del repositorio

```
.
├── _quarto.yml              # Configuración del proyecto y del sitio (navbar, footer, tema, formato)
├── theme-light.scss         # Variables de Bootstrap/Sass y tokens de color para el modo claro
├── theme-dark.scss          # Variables de Bootstrap/Sass y tokens de color para el modo oscuro
├── styles.css                # Estilos propios (tipografía, navbar, tarjetas, animaciones, etc.)
├── index.qmd                 # Página de inicio (bio, foto, enlaces de contacto)
├── blog.qmd                  # Página de listado del blog (lee los posts de posts/)
├── posts/                    # Entradas del blog (actualmente vacío salvo _metadata.yml)
│   └── _metadata.yml          # Opciones comunes a todas las entradas del blog
├── cv/                       # Página del CV
│   ├── index.qmd               # Enlaces de descarga a las versiones del CV
│   ├── cv_spanish.pdf
│   └── cv_english.pdf
├── papers/
│   └── index.qmd               # Listado de publicaciones (placeholder, próximamente)
├── presentations/
│   └── index.qmd               # Listado de charlas/presentaciones (placeholder, próximamente)
├── quotes/
│   └── index.qmd               # Colección de citas curadas
├── avatar.jpg                 # Foto de perfil usada en index.qmd
├── fonts/                     # Fuente Atkinson Hyperlegible (no usada actualmente en styles.css)
└── .github/workflows/publish.yml  # Workflow de CI/CD: build con Quarto + deploy a GitHub Pages
```

### Ficheros de configuración clave

- **`_quarto.yml`**: define el título del sitio, metadatos (Open Graph, Twitter Card), la barra de navegación, el pie de página, los comentarios (utterances) y qué temas Sass usa cada modo (`theme.light` / `theme.dark`).
- **`theme-light.scss` / `theme-dark.scss`**: sobrescriben variables de Bootstrap (colores, tipografía, radios de borde, etc.) para cada modo. Quarto compila cada uno en su propio bundle CSS y alterna entre ellos con el botón de la navbar.
- **`styles.css`**: reglas CSS que no dependen de variables de Sass — importación de fuentes de Google, estilos de navbar/tarjetas/chips/enlaces "about" y animaciones. Se carga después de los temas compilados.

## Convenciones

- Cada sección del sitio es una carpeta con su propio `index.qmd`; Quarto genera `carpeta/index.html` a partir de él.
- Los ficheros PDF (CV) se sirven directamente desde su carpeta y se referencian como recursos en `_quarto.yml`.

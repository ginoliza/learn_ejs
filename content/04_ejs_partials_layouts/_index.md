+++
archetype = "chapter"
title = "4. Partials y layouts de EJS"
weight = 4
+++

Partials son pedazos de código que pueden ser reutilizados (ej: `header` `footer`) y así poder crear layouts
```js {title="index.ejs" hl_lines="1 3"}
<%- include("partials/header.ejs") %>
... contenido html
<%- include("partials/footer.ejs") %>
```

## CSS e imágenes
`app.use(express.static("public"))` especifica que todo el contenido estático (css e imagenes) está dentro de la carpeta `public` y así poder usar rutas relativas

```sh {hl_lines="2 5-10"}
.
├── index.js
├── package-lock.json
├── package.json
├── public
│   ├── images
│   │   └── cat.jpeg
│   └── styles
│       ├── content.css
│       └── layout.css
│
└── views
    ├── about.ejs
    ├── contact.ejs
    ├── index.ejs
    └── partials
        ├── footer.ejs
        └── header.ejs
```
```html {title="header.ejs"}
<link rel="stylesheet" href="/styles/layout.css">
```

```html {title="contact.ejs"}
<img class="profile" src="images/cat.jpeg" alt="cat profile">
```

## Reto:
Modificar el código para que se renderice `/`, `/contact` y `/about` con estilos y la imagen

{{% resources color="fuchsia" icon="fa-fw fab fa-hackerrank" /%}}

{{% expand title="solución" %}}
```js {title="index.js"}
...
// permite usar CSS e imagenes
app.use(express.static("public")) 

// rutas para / /about y /contact
app.get("/", (req, res)=>{
  res.render("index.ejs")
})

app.get("/about", (req, res)=>{
  res.render("about.ejs")
})

app.get("/contact", (req, res)=>{
  res.render("contact.ejs")
})
...
```

- Agregar `<%- include("partials/header.ejs") %>` y `<%- include("partials/footer.ejs") %>` al inicio y al final en `views/about.ejs` y `views/contact.ejs`
{{% /expand %}}

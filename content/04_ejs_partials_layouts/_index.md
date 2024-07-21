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
```js {title="index.js"}
import express from "express";

const app = express();
const port = 3000;

/* Write your code here:
Step 1: Render the home page "/" index.ejs
Step 2: Make sure that static files are linked to and the CSS shows up.
Step 3: Add the routes to handle the render of the about and contact pages.
  Hint: Check the nav bar in the header.ejs to see the button hrefs
Step 4: Add the partials to the about and contact pages to show the header and footer on those pages. */

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```

```js {title="views/index.ejs"}
<%- include("partials/header.ejs") %>


  <h1>Home Page</h1>

  <p>Lorem ipsum dolor sit amet, et proin, justo mus. Porta suspendisse turpis netus sagittis tortor at, vitae aliquet
    pharetra cras velit, id gravida, neque nulla lorem, posuere hac. Ultricies eget lacus vehicula, in ante aliquam
    et,facilisis tempor duis orci. Sed molestie sem in duis eu id, nisl id ultricies metus blandit eget praesent, pede
    tempornullam, vitae arcu tortor suspendisse nibh risus. Nulla id suscipit reiciendis nulla erat. Porta enim aute
    luctus,ducimus sodales dolor.
  </p>
  <p>
    Quam purus justo enim purus, dolor enim, ut eu lectus nam eget nibh. Ante illum nullam leo, vivamus aliquam massa
    massainceptos fermentum porttitor, blandit vehicula, lorem in placerat ut aliquam at sociosqu. Vivamus duis
    ultricies
    aliquam placerat, tincidunt scelerisque imperdiet, egestas erat vel. Libero rerum. Donec ligula tristique, purus
    montes,
    feugiatid nunc in a nec. Duis odio, vitae sed etiam mi massa, laoreet amet purus amet rhoncus, eget sed, arcu
    urna.
    Maecenaswisi id, at donec enim. Proin nisl, pulvinar leo suspendisse, cum parturient non, congue leo et ut in,
    neque ut
    lacusauctor quam fermentum urna. Metus quis, mauris dictum aptent ultrices nulla viverra ornare, tempor elit enim
    leo
    donec,sed sed. Vivamus sapien facilisi, tempor arcu nulla justo sed et, eget suspendisse lacus sed nunc mattis
    lectus.
    Metusgravida.</p>

  <%- include("partials/footer.ejs") %>
```

```js {title="views/about.ejs"}
<h1>About Me</h1>
<img class="profile" src="images/cat.jpeg" alt="cat profile">
<p>
  Quam purus justo enim purus, dolor enim, ut eu lectus nam eget nibh. Ante illum nullam leo, vivamus aliquam massa
  massainceptos fermentum porttitor, blandit vehicula, lorem in placerat ut aliquam at sociosqu. Vivamus duis
  ultricies
  aliquam placerat, tincidunt scelerisque imperdiet, egestas erat vel. Libero rerum. Donec ligula tristique, purus
  montes,
  feugiatid nunc in a nec. Duis odio, vitae sed etiam mi massa, laoreet amet purus amet rhoncus, eget sed, arcu
  urna.
  Maecenaswisi id, at donec enim. Proin nisl, pulvinar leo suspendisse, cum parturient non, congue leo et ut in,
  neque ut
  lacusauctor quam fermentum urna. Metus quis, mauris dictum aptent ultrices nulla viverra ornare, tempor elit enim
  leo
  donec,sed sed. Vivamus sapien facilisi, tempor arcu nulla justo sed et, eget suspendisse lacus sed nunc mattis
  lectus.
  Metusgravida.</p>
```

```js {title="views/contact.ejs"}
<h1>Contact Me</h1>
<form>
  <input name="name" type="text" class="feedback-input" placeholder="Name" />
  <input name="email" type="text" class="feedback-input" placeholder="Email" />
  <textarea name="text" class="feedback-input" placeholder="Comment"></textarea>
  <input type="submit" value="SUBMIT" />
</form>
```

```js {title="views/partials/header.ejs"}
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.1/dist/css/bootstrap.min.css">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.10.2/css/all.css">
  <link rel="stylesheet" href="/styles/layout.css">
  <link rel="stylesheet" href="/styles/content.css">
  <title>EJS Partials</title>
</head>
<header>
  <nav class="navbar navbar-expand-custom navbar-mainbg">
    <a class="navbar-brand navbar-logo" href="#">My Portfolio</a>
    <button class="navbar-toggler" type="button" aria-controls="navbarSupportedContent" aria-expanded="false"
      aria-label="Toggle navigation">
      <i class="fas fa-bars text-white"></i>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav ml-auto">
        <div class="hori-selector">
          <div class="left"></div>

        </div>

        <li class="nav-item">
          <a class="nav-link" href="/"><i class="far fa-copy"></i>Home</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="/about"><i class="far fa-clone"></i>About</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="/contact"><i class="far fa-calendar-alt"></i>Contact</a>
        </li>

      </ul>
    </div>
  </nav>
</header>
<main class="container">
```

```js {title="views/partials/footer.ejs"}
</main>
<footer>
  <div class="waves">
    <div class="wave" id="wave1"></div>
    <div class="wave" id="wave2"></div>
    <div class="wave" id="wave3"></div>
    <div class="wave" id="wave4"></div>
  </div>
  <ul class="social_icon">
    <li><a href="#"><ion-icon name="logo-facebook"></ion-icon></a></li>
    <li><a href="#"><ion-icon name="logo-twitter"></ion-icon></a></li>
    <li><a href="#"><ion-icon name="logo-linkedin"></ion-icon></a></li>
    <li><a href="#"><ion-icon name="logo-instagram"></ion-icon></a></li>
  </ul>

  <ul class="menu">
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Services</a></li>
    <li><a href="#">Team</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
  <p class="copyright"> Made with ❤️ in London.</p>
</footer>
<script type="module" src="https://unpkg.com/ionicons@5.5.2/dist/ionicons/ionicons.esm.js"></script>
<script nomodule src="https://unpkg.com/ionicons@5.5.2/dist/ionicons/ionicons.js"></script>

</body>

</html>
```

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

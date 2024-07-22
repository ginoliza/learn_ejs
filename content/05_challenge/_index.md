+++
archetype = "chapter"
title = "5. Reto"
weight = 5
+++

{{% resources sort="asc" color="fuchsia" icon="fa-fw fab fa-hackerrank" /%}}

{{% expand title="solución" %}}
```js {title="index.js"}
...
app.use(express.static("public"))

app.get("/", (req, res) => {  
  res.render("index.ejs")
});

app.post("/submit", (req, res) => {
  var name = noun[Math.floor(Math.random() * noun.length)];
  var adjective = adj[Math.floor(Math.random() * adj.length)];
  res.render("index.ejs", {name: `${name} ${adjective}`})
});
...
```

```js {title="index.ejs"}
<%- include("partials/header.ejs") %>
<form action="/submit" method="POST">
  <% if (locals.name) { %>
   <h1><%= name %></h1>
  <% } else { %>
    <h1>Welcome to the Band Generator 🤟</h1>
  <% } %>

  <input type="submit" value="Generate Name"><br>  
</form>
<%- include("partials/footer.ejs") %>
```

```css {title="header.ejs"}
<link rel="stylesheet" href="styles/main.css">
```

```js {title="footer.ejs"}
<p>Copyright © <%= new Date().getFullYear() %></p>
```
{{% /expand %}}


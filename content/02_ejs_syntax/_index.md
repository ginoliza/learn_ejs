+++
archetype = "chapter"
title = "2. Sintaxis EJS"
weight = 2
+++

## Tags EJS

- Salida JS genera algo en html `<%= %>` 
- Ejecutar JS `<% console.log("js") %>`
- Renderizar HTML `<%- "<h1>html</h1>" %>`
- Escape: `<%% %%>`para mostrar `<%` o `%>`
- Comentarios `<%# comentario %>`
- Incluir otro archivo EJS `<%- include("header.ejs") %>`

Ej - 
{{< highlight type="js" wrap="true" title="index.js">}}
let bowl = ["apples", "oranges", "pears"];

app.get("/", (req, res) => {
    res.render(__dirname + "/views/index.ejs", { fruits: bowl });
})
{{< /highlight >}}

{{< highlight type="html" wrap="true" title="views/index.ejs">}}
<%# lista no ordenada de frutas %>
  <ul>
  <% fruits.forEach((fruit) => {%>
    <li>
    <%= fruit %>
    </li>
    <% }) %>
  </ul>
{{< /highlight >}}

## Reto
A partir de :

{{< highlight type="js" wrap="true" title="index.ejs">}}

<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>EJS Tags</title>
</head>

<body>
  <h1>
    <!-- title -->     
  </h1>
  <p>Current second:
    <!-- seconds -->     
  </p>  
    <!-- lista si es par -->
    <!-- caso contrario:  -->
    <!-- <p>No hay items para mostrar</p> -->    
  <p>
    <!-- htmlContent -->     
  </p>
  <%- include("footer.ejs") %>
</body>

</html>
{{< /highlight >}}

{{< highlight type="js" wrap="true" title="index.js">}}
import express from "express";
const app = express();
const port = 3000;

app.get("/", (req, res) => {
  const data = {
    title: "EJS Tags",
    seconds: new Date().getSeconds(),
    items: ["apple", "banana", "cherry"],
    htmlContent: "<em>This is some strong text</em>",
  };
  res.render("index.ejs", data);
});

app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});

{{< /highlight >}}

Modificar `index.ejs` de tal manera que cumpla las instrucciones

{{% expand title="solución" %}}
```js
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>EJS Tags</title>
</head>

<body>
  <h1>
    <!-- Tite goes here -->
     <%= title %>
  </h1>
  <p>Current second:
    <!-- Current second goes here -->
     <%= seconds %>
  </p>
  <%  if (seconds % 2===0) {  %>
  <ul>
    <% for(let i=0;i<items.length;i++) {%>
      <li><%= items[i] %></li>
      <% } %>
    <!-- List goes here if current second is even. -->
    <!-- Otherwise it should display the following: -->
    <!-- <p>No items to display</p> -->
  </ul>
  <% } else { %>
  <p>No items to display</p>
  <% } %>
  <p>
    <!-- HTML content goes here -->     
     <%- htmlContent %>
     <%- "<br>" %>
  </p>
  <%- include("footer.ejs") %>
</body>

</html>
{{% /expand %}}

+++
archetype = "chapter"
title = "3. Parsear datos a templates EJS"
weight = 3
+++

## locals
Qué tal si no hay datos que pasar? En `render` no se pasa ningún dato como parámetro, por lo tanto `index.ejs` no tiene de donde sacar `data`. 

{{< highlight type="js" wrap="true" title="index.js">}}
...
app.get("/", (req, res) => {  
  res.render("index.ejs");
});
...
{{< /highlight >}}

{{< highlight type="js" wrap="true" title="index.ejs">}}
<h1> <%= data %> </h1>
{{< /highlight >}}

`locals.fruits` permite verificar la existencia de algo antes de usarlo 
{{< highlight type="js" wrap="true" title="index.ejs">}}

<% if (locals.data) { %>
    <h1> <%= data %> </h1>
<% } %>
{{< /highlight >}}

## Enviar datos de EJS al servidor
`req.body` permite acceder a los valores `name` del formulario en `index.ejs`. Ej: `fName`

{{< highlight type="html" wrap="true" title="index.ejs" hl_lines="2">}}
<form>
    <input type="text" name="fName">
    <input type="submit" value="OK">
</form>
{{< /highlight >}}

{{< highlight type="js" wrap="true" title="index.js" hl_lines="3">}}
...
app.post("/submit", (req, res) => {
    res.render("index.ejs", { name: req.body["fName"]});
});
...
{{< /highlight >}}

## Reto
Contar el número de caracteres del nombre completo, sumando nombre y apellido.
- Mediante el formulario enviar `fName` y `lName` 
- Si existe el número de letras del nombre completo imprimir: "Ingrese nombre", caso contrario imprimir: "Su nombre tiene X dígitos"

{{< highlight type="js" wrap="true" title="index.js">}}
import express from "express";
import bodyParser from "body-parser";

const app = express();
const port = 3000;

app.use(bodyParser.urlencoded({ extended: true }));

app.get("/", (req, res) => {});

app.post("/submit", (req, res) => {});

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});

{{< /highlight >}}

{{< highlight type="html" wrap="true" title="index.ejs">}}
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Name Letters</title>
</head>

<body>
  <!-- Write your ejs code here -->
  <form action="/submit" method="POST">
    <input type="text" name="fName" placeholder="First name">
    <input type="text" name="lName" placeholder="Last name">
    <input type="submit" value="OK">
  </form>
</body>

</html>
{{< /highlight >}}

{{% expand title="solución" open="true" %}}

```js {title="index.js"}
...
app.get("/", (req, res) => {
  res.render("index.ejs");
});

app.post("/submit", (req, res) => {
  var num = (req.body["fName"] + req.body["lName"]).length;  
  console.log(num);
  res.render("index.ejs", {num});
});
...
```

```js {title="index.ejs"}
...
<body>
  <!-- Write your ejs code here -->
   <% if(locals.num) {%>
      <h1>Tu nombre tiene <%= locals.num %> caracteres</h1>
    <% } else{%>
      <h1>Ingrese nombre</h1>
      <% } %>
  <form action="/submit" method="POST">
...
```
{{% /expand %}}
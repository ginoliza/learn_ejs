+++
archetype = "chapter"
title = "1. EJS"
weight = 1
+++

## EJS
Embedded JavaScript, tiene extensión `.ejs`. Es básicamente HTML con pedazos de JS dentro. 

## EJS language support
Un plug in para VSCode de syntax highlighting

## render (express)
Usar `render` en lugar de `sendFile` ya que sólo funciona para páginas estáticas, no templates. Además se puede enviar datos como segundo parámetro `{ name: "gino angelo" }`

{{< highlight type="js" wrap="false" hl_lines="3" title="index.js">}}
...
app.get("/", (req, res) => {
    res.render("index.ejs", { name: req.body["name"] });
})
...
{{< /highlight >}}

El código JS debe ir dentro de `<%= %>`

{{< highlight type="html" wrap="true" hl_lines="2" title="views/index.ejs">}}
<h1>Hello <%= name %></h1>
{{< /highlight >}}

## Reto
Escribir `index.js` e `index.ejs` de modo que se detecte el día con la función `getDay` e imprima un html:
- Si es fin de semana: Hey, it's the weekend! It's time to have fun
- Si es dia de semana: Hey, it's a weekday! It's time to work hard

{{< highlight type="html" wrap="true" lineNos="true" title="index.ejs">}}
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Some page</title>
</head>
<body>
  <h1>Hey, it's <%= today %>! It's time to <%= advice %></h1>
</body>
</html>
{{< /highlight >}}

{{< highlight type="js" wrap="true" lineNos="true" title="index.js">}}
import express from 'express';
import { dirname } from "path";
import { fileURLToPath } from "url";

const __dirname = dirname(fileURLToPath(import.meta.url));

const app = express()
const port = 3000

const d = new Date();
let day = d.getDay();

var today = "a weekday"
var advice = "work hard"

app.get("/", (req, res) => {
    if(day > 5){
        today = "the weekend"
        advice = "have fun"
    }
    res.render(__dirname + "/views/index.ejs", { today, advice });
})

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
  console.log(day);
})
{{< /highlight >}}
# Introducción a Express.js

## Objetivo

Vamos a desarrollar una API conectada a MongoDB. El propósito de este repositorio es centralizar la documentación necesaria para construir una API utilizando Express, ya que a su formador no le agrada completamente la que está disponible en línea. Este tutorial incluirá enlaces a secciones específicas de la documentación existente, así como información adicional propia. Además, se planea proporcionar un video de apoyo para facilitar el proceso.

## primeros pasos

Recuerda debes tener instalado [Node.js](https://nodejs.org/en/download), despues crea y entra a la carpeta donde vas a guardar el proyecto.

```
mkdir app
cd app
```

Una vez dentro de la carpeta usa el siguiente comando para crear un archivo que contendra la informacion de configuracion del proyecto (recuerda personalizarla). Deja el punto de entrada como index.js

```
npm init
```

Vamos a instalar express.js

```
npm install express
```

les debe aparecer un archivo package-lock.json y una carpeta node_modules, en este momento es buena idea crear el .gitignore para que no se suba esta ultima.

```
touch .gitignore
```

dentro poner

```
node_modules
```

Ahora vamos a crear un archivo llamado index.js

```
touch index.js
```

Vamos a instalar nodemon para que nos recarge el servidor siempre que realicemos cambios (opcional)

```
npm install nodemon --develop
```

al final de esta seccion deben tener algo parecido a esto:

<img src="img/primeros_pasos.png" alt="estructura de carpetas y archivos al final primeros pasos">

## Hola Mundo

Dentro de index.js vamos a poner el siguiente codigo:

```
const express = require("express")
const app = express()

const PORT = 3006
app.set("port",PORT)

app.get("/",(req,res)=>{
    console.log("hola mundo")
    res.send("hola mundo")
})

app.listen(PORT,()=>{
    console.log(`Escuchando en el puerto ${PORT}`)
})

```

Para levantar el servidor vamos a correr el siguiente comando en una consola al nivel del index.js

```
node index.js
```

Si abren el navegador y escriben la dirección 127.0.0.1:3006, encontrarán el clásico "Hola Mundo".

## Prueba de Rutas

Para Detectar errores en las rutas de los archivos de manera temprana vamos a empezar creando la carpeta routes

```
mkdir routes
touch routes/router.proyectos.js
```

y vamos a poner el siguiente código

```
const express = requiere("express")
const router = express.Router()
router.get("/"),(req,res)=>{
    console.log("hola desde rutas")
    res.send("hola desde rutas")
}
module.exports = router
```

despues añadimos las siguientes lineas de código a app.js

```
// esto en las importaciones
const proyectoRoutes = require("./routes/routes.proyectos.js")
// esto encima del app.get
app.use("/api/author/",authorRoutes)
```

y lo probamos en el navegador, debe aparecer el texto hola desde routes y el log esta en la consola donde se levanto el servidor.

```
127.0.0.1:3005/api/author/
```

## Prueba de Controlador

Una vez el archivo router/author esta funcionando pasamos a el controlador creamos

```
mkdir controllers
touch controllers/routes.proyectos.js
```

y ponemos el siguiente codigo:

```
exports.Hola = (req,res)=>{
    console.log("Hola desde el controlador")
    res.send("hola desde el controlador")
}
```

modificamos el archivo rotes/author

```
const express = require("express")
const proyectoControllers = require("../controllers/controllers.proyecto")
const router = express.Router()

router.get("/", proyectoControllers.Hola)

module.exports = router

```

y lo probamos en el navegador en la misma ruta anterior

# Prueba-tecnica-olam

este proyecto sencillo es una prueba tecnica para la compañia olam creative la cual consiste en una sopa de letras que podemos armar y pasarle palabras a buscar

# Tecnologia usadas

- Quasar framework para maquetar y formularios
- vue3 como tecnologia en frontend
- npm y yarn para manejo de paquetes
- uso de sass precompilador de css
- uso de componentes

# Quasar App (prueba-tecnica-quasar)

A Quasar Project

## Install the dependencies

```bash
yarn
# or
npm install
```

### Start the app in development mode (hot-code reloading, error reporting, etc.)

```bash
quasar dev
```

### Lint the files

```bash
yarn lint
# or
npm run lint
```

### Format the files

```bash
yarn format
# or
npm run format
```

### Build the app for production

```bash
quasar build
```

### Customize the configuration

See [Configuring quasar.config.js](https://v2.quasar.dev/quasar-cli-webpack/quasar-config-js).

## Guia de usuario
1. setear el numero de columnas de la sopa de letras (esta no tiene que ser de NxN sino que puede ser asimetrica) ![image](https://github.com/andresknoo00001/Prueba-tecnica-olam/assets/32203440/1692953c-c7ee-4b13-b99c-c77a8bd753e0)
  la idea aca es poner el numero de columnas que queremos que tenga la sopa de letras (horizontalmente cuantos cuadros tendrá)
2. aca setearemos el numero de filas de la matriz ![image](https://github.com/andresknoo00001/Prueba-tecnica-olam/assets/32203440/35d0e027-4ce9-4a15-ab92-2f9a550b3178)
   cuantas filas tendremos en la sopa de letras (verticalmente cuantos cuadros tendremos)
3. - ya aca comenzamos a contstruir la sopa de letras, debemos ingresar fila por fila la informacion separando las letras por coma "," ![image](https://github.com/andresknoo00001/Prueba-tecnica-olam/assets/32203440/e35bdb14-4a05-4682-a4ba-c2fec5348534)
   - ![image](https://github.com/andresknoo00001/Prueba-tecnica-olam/assets/32203440/d6e07a26-96f3-4b1d-962f-7e5599ff7b1f)
   - La aplicacion realiza la validacion de que la cantidad de letras separadas por coma corresponda al numero de columnas indicadas en la parte superior ![image](https://github.com/andresknoo00001/Prueba-tecnica-olam/assets/32203440/a3a340ba-5d6c-49a3-9d25-1b7a9dca99c9)
   - Cuando el numero de letras es correcto, almacena la informacion e indica cuantas filas mas debemos agregar para construir la sopa de letras ![image](https://github.com/andresknoo00001/Prueba-tecnica-olam/assets/32203440/b9bd8b4c-59f4-47f2-96a3-78f8809e99cf)
 


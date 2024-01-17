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

### Entrada recomendada para filas de sopa de letras
- Numero Columnas: 14
- Numero filas: 14
- filas:
  1. N,D,E,K,I,C,A,N,G,U,R,O,G,E
  2. S,X,R,Y,K,V,I,I,Q,G,W,Q,O,D
  3. J,A,G,U,A,R,Z,W,B,N,K,O,U,A
  4. M,L,E,L,E,F,A,N,T,E,H,O,G,W
  5. L,O,B,O,N,U,T,R,I,A,O,U,S,U
  6. W,W,O,S,O,G,A,T,O,V,R,T,M,O
  7. H,L,Z,N,C,T,Y,Z,E,O,X,A,U,R
  8. C,E,C,Y,T,I,B,U,R,O,N,S,R,O
  9. C,O,N,E,J,O,Y,U,S,M,R,S,H,T
  10. Y,N,I,F,E,F,P,T,E,Z,O,O,S,F
  11. O,S,S,E,R,P,I,E,N,T,E,F,L,G
  12. P,P,V,D,D,X,U,F,A,L,C,O,N,Y
  13. M,O,N,O,C,U,Q,W,M,A,N,A,T,I
  14. N,N,X,H,E,B,P,M,U,P,E,R,R,O
- Palabras: MANATI,PERRO,GATO ,CONEJO ,TIBURON,ELEFANTE,ALCON,SERPIENTE ,JAGUAR ,CANGURO ,LOBO, MONO,NUTRIA,LEON,LORO,TORO,ORUGA,TIGRE,CACATUA,KOALA,PUMA,AGUILA
 
### Guia de usuario
1. setear el numero de columnas de la sopa de letras (esta no tiene que ser de NxN sino que puede ser asimetrica) ![image](https://github.com/andresknoo00001/Prueba-tecnica-olam/assets/32203440/1692953c-c7ee-4b13-b99c-c77a8bd753e0)
  la idea aca es poner el numero de columnas que queremos que tenga la sopa de letras (horizontalmente cuantos cuadros tendrá)
2. aca setearemos el numero de filas de la matriz ![image](https://github.com/andresknoo00001/Prueba-tecnica-olam/assets/32203440/35d0e027-4ce9-4a15-ab92-2f9a550b3178)
   cuantas filas tendremos en la sopa de letras (verticalmente cuantos cuadros tendremos)
3. - ya aca comenzamos a contstruir la sopa de letras, debemos ingresar fila por fila la informacion separando las letras por coma "," ![image](https://github.com/andresknoo00001/Prueba-tecnica-olam/assets/32203440/e35bdb14-4a05-4682-a4ba-c2fec5348534)
   - ![image](https://github.com/andresknoo00001/Prueba-tecnica-olam/assets/32203440/d6e07a26-96f3-4b1d-962f-7e5599ff7b1f)
   - La aplicacion realiza la validacion de que la cantidad de letras separadas por coma corresponda al numero de columnas indicadas en la parte superior ![image](https://github.com/andresknoo00001/Prueba-tecnica-olam/assets/32203440/a3a340ba-5d6c-49a3-9d25-1b7a9dca99c9)
   - Cuando el numero de letras es correcto, almacena la informacion e indica cuantas filas mas debemos agregar para construir la sopa de letras ![image](https://github.com/andresknoo00001/Prueba-tecnica-olam/assets/32203440/b9bd8b4c-59f4-47f2-96a3-78f8809e99cf)
   - Cuando terminamos de armar la sopa de letras el sistema no nos permite ingresar mas filas y nos notifica que ya esta listo ![image](https://github.com/andresknoo00001/Prueba-tecnica-olam/assets/32203440/11b91b25-6727-490c-87e7-edd86db132a0)
4. luego de que ingresamos las filas de la sopa de letras, la aplicacion nos habilita el formulario para ingresar las palabras a buscar, podemos hacerlo de forma individual o ingresnadolas sepadas por coma
   ![image](https://github.com/andresknoo00001/Prueba-tecnica-olam/assets/32203440/57b75b67-825c-4b3d-9fe8-58cedd525e4b)
5. para buscar las palabras simplemente le damos click a submit y el sistema busca las palabras y te dice cuales encuentra y cuales no ![image](https://github.com/andresknoo00001/Prueba-tecnica-olam/assets/32203440/2380e24d-68bb-49d1-b9c9-38db0e756b62)
6. por ultimo pero no menos importante, si queremos resetear los valores solo debemos oprimir el boton de reset para limpiar la informacion ![image](https://github.com/andresknoo00001/Prueba-tecnica-olam/assets/32203440/84af9e46-4481-4d0a-86f4-92aa0a921cf6) y ![image](https://github.com/andresknoo00001/Prueba-tecnica-olam/assets/32203440/452bc6a6-7a08-46bf-8312-23174c132f95)



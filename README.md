# Uso de Conventional Commits, Commitlint y Husky en Proyectos

En este tutorial, aprenderemos a utilizar _Conventional Commits_ junto con _Commitlint_ y _Husky_ para mantener mensajes de commit consistentes y generar changelogs automáticamente. Este enfoque mejora la comprensión de los cambios en el proyecto y asegura una colaboración más efectiva entre los desarrolladores.

<img src="https://media1.giphy.com/media/kH6CqYiquZawmU1HI6/giphy.gif?cid=ecf05e47gxcc9d3ykdkw3aeew06ijwhze4iq2b4wgoxnr1em&ep=v1_gifs_search&rid=giphy.gif&ct=g" alt="Git" width="200">

## Paso 1: Configuración de Conventional Commits

1. Instala la extensión [Conventional Commits](https://marketplace.visualstudio.com/items?itemName=vivaxy.vscode-conventional-commits) en Visual Studio Code para facilitar el proceso de commits.

2. Abre las extensiones en Visual Studio Code con `Ctrl + Shift + P` y busca "Conventional Commits". Selecciona la opción y presiona `Enter`.

3. En el cuadro de diálogo, elige el tipo de commit que estás realizando. Puedes seleccionar entre opciones como feat (nueva característica), fix (corrección de errores), entre otros.
4. Si tu cambio se relaciona con un componente (**scoope**) específico , puedes elegir o crear un ámbito. Esto proporciona un contexto adicional sobre el alcance del commit.

5. Selecciona un gitmoji que represente visualmente el propósito de tu commit. Estos emoticonos ayudan a identificar rápidamente la naturaleza de los cambios.
6. Proporciona una descripción breve y concisa del cambio que estás realizando. Usa un lenguaje claro y directo.
7. Opcionalmente, puedes agregar una descripción más detallada del commit para proporcionar información adicional, si es necesario.
8. Si es relevante, enumera los cambios importantes o los problemas cerrados por este commit. Esto facilita el seguimiento y la documentación de los cambios realizados.
9. Puedes personalizar un atajo para acceder más rápidamente a la extensión, por ejemplo, `Shift + Alt + G`.

## Paso 2: Configuración de Commitlint

_Commitlint_ es una herramienta de línea de comandos, pero la podemos integrar en nuestro proyecto e incluso unirlo a nuestro github para asegurarnos que cada que vamos hacer un commit ese hook se lance, verifiqué si sigue las normas de estilo de **Conventional Commits** y si es asi el commit se realizara.

1. Inicia un nuevo proyecto npm con `npm init -y`.
2. Instala las dependencias de desarrollo:
   ```bash
   npm install --save-dev @commitlint/cli @commitlint/config-conventional
   ```
3. Crea un archivo `commitlint.config.js` en la raíz del proyecto con el siguiente contenido:

   ```js
   module.exports = {
     extends: ["@commitlint/config-conventional"],
   };
   ```

   Lo que estamos haciendo es heredar las normas de estilo de **Conventional Commits**, la cual es la libreria que acabamos de instalar.

## Paso 3: Configuración de Husky

_Husky_ es una herramienta que simplifica la configuración de ganchos (hooks) de Git en proyectos de desarrollo. Permite ejecutar scripts automáticamente en eventos específicos, como antes de confirmar o antes de enviar cambios al repositorio. Esto facilita la automatización de tareas, como ejecutar pruebas o formatear código, contribuyendo a mantener la calidad y consistencia en el desarrollo de software.

1. Instala Husky como dependencia de desarrollo:
   ```bash
    npm i -D husky
   ```
2. Añade el script de preparación para Husky en tu archivo package.json:

   ```json
    "scripts": {
   "prepare": "husky install"
   }
   ```

   Ejecuta el comando:

   ```bash
    npm run prepare
   ```

3. Añade el hook commit-msg utilizando el siguiente comando:
   ```bash
    npx husky add .husky/commit-msg "npx --no -- commitlint --edit ${1}"
   ```
4. Luego, creamos un archivo `.gitignore` y agregamos la línea `node_modules` en su interior.

## Paso 4: Uso de Conventional-changelog

_Conventional Changelog_ es una herramienta que automatiza la generación de registros de cambios (changelogs) basados en las convenciones establecidas por los mensajes de commit. Al seguir las convenciones de **Conventional Commits**, facilita la creación de changelogs coherentes y comprensibles. La herramienta analiza los mensajes de commit y genera automáticamente registros de cambios, mejorando la documentación y comunicación efectiva de las actualizaciones del software.

1. Instala conventional-changelog-cli de forma global o local:

   ```bash
    npm install -g conventional-changelog-cli
   ```

   O de forma local:

   ```bash
    npm install --save-dev conventional-changelog-cli
   ```

2. Genera el archivo de changelog con el siguiente comando:
   ```bash
    conventional-changelog -i CHANGELOG.md -s -r 0
   ```

## Paso 6: Recursos Útiles

[**Conventional Commits**](https://www.conventionalcommits.org/en/v1.0.0/) - [**gitmoji**](https://gitmoji.dev/) - [**commitlint**](https://commitlint.js.org/#/) - [**husky**](https://typicode.github.io/husky/getting-started.html)

Con estos pasos, estarás utilizando _Conventional Commits, Commitlint y Husky_ en conjunto, asegurando un flujo de trabajo consistente y generando changelogs automáticamente. Este enfoque mejora la calidad del código y la colaboración en el desarrollo de proyectos.

<div style="text-align: center;">
  <a href="https://github.com/emiliojrb26" target="_blank">@emiliojrb</a>
</div>

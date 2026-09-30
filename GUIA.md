# Estación Aurora · Guía de configuración

Tiempo aproximado: 15 a 20 minutos, una sola vez.
Solo tú necesitas cuenta (de Google y de GitHub). Tus compañeros solo escanean el QR y votan.

---

## Parte 1 · Crear el proyecto en Firebase

1. Entra a **https://console.firebase.google.com** con tu cuenta de Google.
2. Clic en **Crear un proyecto** (o "Agregar proyecto"). Ponle un nombre, por ejemplo `estacion-aurora`.
   - Google Analytics no es necesario; puedes desactivarlo.
3. Cuando el proyecto esté listo, en la pantalla principal haz clic en el ícono **`</>` (Web)** para registrar una app web.
   - Nombre: `aurora-web`. **No** marques "Firebase Hosting".
   - Firebase te mostrará un bloque de código con `const firebaseConfig = { ... }`. **Déjalo abierto o cópialo**; lo usas en la Parte 3.

## Parte 2 · Activar la base de datos y el acceso anónimo

**Base de datos**

1. En el menú izquierdo: **Compilación → Realtime Database → Crear base de datos**.
2. Ubicación: la que aparezca por defecto (por ejemplo Estados Unidos) está bien.
3. Elige **Iniciar en modo bloqueado** y termina.
4. Entra a la pestaña **Reglas**, borra todo lo que hay y pega el contenido del archivo `reglas-firebase.json`. Clic en **Publicar**.

**Acceso anónimo** (así nadie tiene que registrarse)

1. En el menú izquierdo: **Compilación → Authentication → Comenzar**.
2. En la pestaña **Método de acceso**, elige **Anónimo**, actívalo y guarda.

## Parte 3 · Pegar tu configuración en la página

1. Abre `index.html` con cualquier editor de texto (Bloc de notas, VS Code…).
2. Busca el bloque que dice `PEGA AQUÍ LA CONFIGURACIÓN DE TU PROYECTO DE FIREBASE`.
3. Reemplaza cada `"PEGA_AQUI"` con el valor correspondiente del bloque que te dio Firebase en la Parte 1.
   - Revisa que `databaseURL` esté incluido. Si no aparece en el bloque de Firebase, cópialo de la parte de arriba de la página de **Realtime Database** (se ve como `https://estacion-aurora-default-rtdb.firebaseio.com`).
4. Guarda el archivo.

> Estos datos no son secretos: están pensados para ir dentro de páginas web. La seguridad la ponen las reglas que pegaste en la Parte 2.

## Parte 4 · Publicar la página (GitHub Pages)

1. Entra a **https://github.com** con tu cuenta y crea un repositorio nuevo **público**, por ejemplo `estacion-aurora`.
2. En el repositorio: **Add file → Upload files**, arrastra `index.html` y confirma con **Commit changes**.
3. Ve a **Settings → Pages**. En "Branch" elige `main` y la carpeta `/ (root)`, y guarda.
4. Espera uno o dos minutos. GitHub te mostrará la dirección, algo como
   `https://TU-USUARIO.github.io/estacion-aurora/`

**Recomendado:** en Firebase, ve a **Authentication → Configuración → Dominios autorizados** y agrega `TU-USUARIO.github.io`.

## Parte 5 · El día de la presentación

- **En la computadora del proyector** abre la dirección agregando `#presentador` al final:
  `https://TU-USUARIO.github.io/estacion-aurora/#presentador`
  Ahí ves la historia, las barras de votos, el QR y los controles.
- **Tus compañeros** escanean el QR. Les abre la dirección normal, sin `#presentador`, y solo pueden votar.
- Flujo: esperas a que voten → **Cerrar votación** → **Continuar con la opción ganadora**. Si hay empate, tocas la opción que decides que gana.
- Al llegar a un final puedes presionar **Empezar de nuevo**.

### Ensayo antes de clase

- Abre la página del presentador en tu computadora y la página normal en tu celular. Vota desde el celular y revisa que la barra se mueva.
- Antes de configurar Firebase, la página del presentador funciona en **modo ensayo** con los botones "+1 A / +1 B".

### Si cambias de computadora para presentar

La primera computadora que abre `#presentador` queda como la única que puede controlar la historia (así ningún alumno puede adelantarla). Para presentar desde otra computadora:

1. En Firebase, **Realtime Database → Datos**.
2. Pasa el cursor sobre el nodo `state` y bórralo (ícono de basura).
3. Abre `#presentador` en la nueva computadora.

Puedes borrar también el nodo `votes` para limpiar los votos viejos; no es obligatorio.

---

## Límites del plan gratuito

El plan gratuito de Firebase (Spark) aguanta de sobra un salón de clases: permite 100 conexiones simultáneas y varios GB de transferencia al mes.

## Cambiar la historia

Toda la historia está en `index.html`, en el bloque `const STORY = { ... }`. Cada escena tiene su título, texto y dos opciones, y cada opción indica a qué escena lleva (`next`). Los finales llevan `ending: true`. Puedes editarlo tú o pedirme una historia nueva y te regreso el archivo listo.

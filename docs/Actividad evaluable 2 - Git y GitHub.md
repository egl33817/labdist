# Actividad evaluable 2 - Git y GitHub

> **Documento realizado por Roberto Delgado Sánchez - Alumno de Despliegue de Aplicaciones Web - DAW**

[TOC]

## 1. Consideraciones previas

En esta actividad se pondrán en práctica los conocimientos adquiridos en esta asignatura sobre el sistema de control de versiones **Git**, realizando la primera parte en nuestra máquina local utilizando el intérprete de comandos **Git** **Bash** y la segunda en la plataforma **GitHub** en combinación con la herramienta **SourceTree**, que permite trabajar con **Git** en modo gráfico. Todas las cuestiones planteadas en la actividad serán debidamente documentadas con la inclusión de los comandos ejecutados y los resultados de dicha ejecución.

En la parte final de este documento se incluyen enlaces tanto al repositorio remoto creado en **GitHub** como al vídeo creado con los contenidos requeridos.

## 2. Trabajo en local

Antes de empezar con nuestra tarea, además de revisar la configuración de nuestro repositorio local, ejecutaremos el siguiente comando para que el historial de ramas de **Git** se mantenga como un árbol:

```bash
$ git config --global merge.ff false
```

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213093939960.png" alt="image-20250213093939960" style="zoom:67%;" />

La configuración de partida de nuestro repositorio local se comprueba con el comando que se muestra a continuación y es la siguiente:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213094059639.png" alt="image-20250213094059639" style="zoom:67%;" />

En los recuadros rojos se pueden ver tanto mis datos personales (nombre, apellidos y correo de **educastur**) como que el primer comando que se ejecutó para el tema del historial de ramas se ejecutó correctamente.

Una vez tenemos listo el entorno, podemos empezar a resolver las cuestiones.

### 2.1 Cuestión 1 - Inicialización  y primeros pasos

**Inicializa un nuevo repositorio Git en una carpeta llamada `labdist` y agrega los archivos proporcionados en el aula virtual. Renombra la rama master a `main` , si es necesario, realiza el primer `commit` y, finalmente, muestra el log del repositorio.**

El primer paso es crear el repositorio **Git**, para lo cual nos situamos en la carpeta deseada (en mi caso será la situada en `D:\Despliegue\PracticaGit`) y ejecutamos el siguiente comando, que creará una carpeta llamada `labdist` en cuyo interior inicializará nuestro repositorio:

```bash
$ git init labdist
```

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213094835202.png" alt="image-20250213094835202" style="zoom:67%;" />

Como se puede ver en la captura, se ejecutan otros comandos con el siguiente objetivo:

- `pwd`: para que quede claro en qué carpeta estamos trabajando.
- `ls`: para comprobar que, efectivamente, se ha creado la carpeta de nombre `labdist`.
- `ls -al`: para verificar que tenemos una carpeta oculta de nombre `git`, lo que certifica que el repositorio se ha creado correctamente.

Ahora copiamos los archivos facilitados en el aula virtual con el explorador de archivos de Windows, mostrando en la siguiente captura de pantalla que, efectivamente, se han copiado correctamente:

```bash
$ ls -al
```

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213095318214.png" alt="image-20250213095318214" style="zoom:67%;" />

Cambiamos el nombre de la rama `master` a `main`, ya que cuando pasemos a la parte del trabajo en remoto será necesario que se llame así, pues en **GitHub** la rama principal tiene esa denominación. Ese cambio de nombre se hace con este comando:

```bash
$ git branch -M main
```

En la imagen se puede observar cómo, efectivamente, la rama `master` pasa a llamarse `main`:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213095754793.png" alt="image-20250213095754793" style="zoom:67%;" />

Hacemos ahora nuestro primer `commit`, para lo cual movemos en primer lugar nuestros ficheros del directorio de trabajo a la llamada `staging area` y luego ejecutamos el `commit`. Los comandos implicados en este proceso son los que se muestran a continuación:

```bash
$ git status
$ git add .
$ git status
$ git commit -m "Realizamos el primer commit con los archivos de partida de nuestra web"
$ git status
```

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213100414179.png" alt="image-20250213100414179" style="zoom:67%;" />

En principio la ejecución del comando `git status` no sería necesaria, pero considero interesante que quede claro el camino que siguen los archivos que hemos subido al repositorio desde el directorio de trabajo hasta su inclusión en el primer `commit`. Se marca en rojo el comando más importante aquí, `git commit`.

Ya por último mostramos el log del repositorio:

```bash
$ git log
```

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213100712497.png" alt="image-20250213100712497" style="zoom:67%;" />

Podemos ver en la captura detalles del `commit` como su código Hash completo, rama en la que se ha hecho, datos del autor del mismo y el mensaje añadido.

### 2.2 Cuestión 2 - Gitignore

**Incluye un fichero `.gitignore` para que los ficheros `README.md` , `LICENCE.txt` y `passwords.txt` sean ignorados por el control de versiones. Realiza el commit y muestra los logs del repositorio en una línea.**

A veces tendremos algún tipo de archivo que no queremos que sea controlado por **Git**, como por ejemplo archivos temporales, binarios, aquellos que son generados por el IDE que estemos usando, etc. En el archivo `.gitignore` se especifican los datos de aquellos archivos que queremos que sean ignorados (como su propio nombre indica) por el sistema de control de versiones, en nuestro caso son los tres indicados en el enunciado: `README.md`, `LICENCE.txt` y `passwords.txt`.

El archivo `.gitignore` se crea en la carpeta raíz de nuestro repositorio e introducimos en él los nombres de esos archivos que deben ser ignorados. El proceso implica la ejecución de los siguientes comandos y se puede ver en la captura de pantalla:

```bash
$ pwd
$ ls -al
$ vi .gitignore
$ cat .gitignore
$ ls -al
```

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213103046666.png" alt="image-20250213103046666" style="zoom:67%;" />

Con los comandos ejecutados se demuestra que el archivo `.gitignore` no existía inicialmente y cómo se procedió a su creación con el editor `vi`. Su contenido se limita al nombre de los tres archivos que queremos ignorar.

Hacemos el `commit` para que el archivo `.gitignore` sea controlado por **Git**, ejecutando `git status` para ver los pasos que sigue dicho fichero: 

```bash
$ git status
$ git add .
$ git status
$ git commit -m "Agregamos el fichero .gitignore a nuestro repositorio"
$ git status
```

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213103833261.png" alt="image-20250213103833261" style="zoom:67%;" />

Ya por último mostramos los logs del repositorio en una única línea:

```bash
$ git log --oneline
```

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213103935708.png" alt="image-20250213103935708" style="zoom:67%;" />

### 2.3 Cuestión 3 - Creamos algunos archivos

**En el repositorio, crea los archivos `README.md` , `LICENCE.txt` y `passwords.txt` con algún contenido. Muestra el estado del repositorio. Muestra el listado de archivos ignorados.**

La creación de los archivos no tiene ningún misterio, se lleva a cabo con `vi` y en la siguiente imagen se puede ver su contenido:

```bash
$ vi README.md
$ vi LICENCE.txt
$ vi passwords.txt
```

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213104551771.png" alt="image-20250213104551771" style="zoom:67%;" />

Cuando comprobamos el estado del repositorio es cuando vemos realmente el trabajo que realiza `.gitignore`, ya que aunque hay tres ficheros nuevos en el repositorio, al figurar en la lista de aquellos que deben ser ignorados al hacer un `git status` vemos que el directorio de trabajo permanece vacío:

```bash
$ ls -al
$ git status
```

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213105307848.png" alt="image-20250213105307848" style="zoom:67%;" />

Por último, para ver la lista de archivos que están siendo ignorados por **Git** gracias a `.gitignore` se usa el comando que se muestra a continuación:

```bash
$ git status --ignored
```

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213105758968.png" alt="image-20250213105758968" style="zoom:67%;" />

### 2.4 Cuestión 4 - Creación de una nueva rama

**Crea una rama de nombre `feature-estilos`, cámbiate a ella y lleva a cabo las siguientes tareas:**

- **modifica el archivo `estilos.css` añadiendo los siguientes estilos:**
  - **propiedad `color` del `body` y de `h2` : `#2a2a2a`**
  - **propiedad `background-color` de `header` y `footer`: `#2a75ff`**
- **comprueba el estado del repositorio. Añade los cambios, realiza un `commit` con el mensaje "actualizados estilos a azules"**.

En primer lugar creamos la rama `feature-estilos` con el siguiente comando:

```bash
$ git branch feature-estilos
$ git branch
```

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213110242273.png" alt="image-20250213110242273" style="zoom:67%;" />

El segundo comando ejecutado, `git branch`, nos sirve para ver el listado de ramas que tenemos en el repositorio y que la activa es `main` (es la que tiene el asterisco al lado de su nombre). Nos cambiamos a la rama recién creada con el siguiente comando y comprobamos (de nuevo con `git branch`) que es la rama que tenemos activa ahora:

```bash
$ git checkout feature-estilos
$ git branch
```

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213110513604.png" alt="image-20250213110513604" style="zoom:67%;" />

Una vez situados en esta rama, hacemos los cambios indicados en el archivo `estilos.css` con el **IDE** **Visual Studio Code**, incluyendo capturas de pantalla de dichos cambios y de cómo se mostraba nuestra web antes y después de los mismos:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213110605468.png" alt="image-20250213110605468" style="zoom:67%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213110924157.png" alt="image-20250213110924157" style="zoom:67%;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213111020036.png" alt="image-20250213111020036" style="zoom:67%;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213111101490.png" alt="image-20250213111101490" style="zoom:67%;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213111137870.png" alt="image-20250213111137870" style="zoom:67%;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213111216329.png" alt="image-20250213111216329" style="zoom:67%;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213111253416.png" alt="image-20250213111253416" style="zoom:67%;" />

No forma parte de la práctica, pero se quiere dejar constancia de que, una vez que se guardan los cambios realizados en el archivo `estilos.css`, el propio **IDE** nos informa de que esos cambios han sido detectados por **Git**, de tal forma que ahora aparece una letra `M` a la derecha del nombre del archivo:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213111505505.png" alt="image-20250213111505505" style="zoom:67%;" />

Para finalizar con este apartado, toca comprobar el estado del repositorio, añadir los cambios y hacer un `commit` con el mensaje `"Actualizados estilos a azules"`. Como todas esas tareas ya las hemos hecho con anterioridad, se muestran todos los comandos del tirón para no ser repetitivos, así como su resultado y la aplicación de esos nuevos estilos a nuestra web:

```bash
$ git status
$ git add .
$ git status
$ git commit -m "Actualizados estilos a azules"
$ git status
```

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213111911506.png" alt="image-20250213111911506" style="zoom:67%;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213112016185.png" alt="image-20250213112016185" style="zoom:80%;border:1px solid black;" />

Son cambios muy sutiles y casi no se observa diferencia.

### 2.5 Cuestión 5 - Regreso a la rama main

**Vuelve a la rama `main`y en el archivo `index.html` añade un comentario donde se indique tu nombre como autor de la página. Comprueba el estado del repositorio. Añade los cambios, realiza un `commit` con el mensaje `"Añadido autor en index"`. Muestra los logs del repositorio en una línea, gráficamente y con 'decoración'.**

En primer lugar hacemos el cambio de rama con el comando siguiente:

```bash
$ git checkout main
```

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213112440128.png" alt="image-20250213112440128" style="zoom:67%;" />

Como se puede ver en las capturas de pantalla, con el comando `git branch` se comprueba cómo, efectivamente, se hace ese cambio entre ramas. Volvemos a continuación a **Visual Studio Code** y añadimos el comentario solicitado, tal y como se puede ver en esta captura de pantalla:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213112827483.png" alt="image-20250213112827483" style="zoom:80%;" />

Comprobamos el estado del repositorio, añadimos los cambios y hacemos el `commit`, todo ello aplicando los comandos que ya hemos visto a lo largo de la actividad:

```bash
$ git status
$ git add .
$ git status
$ git commit -m "Añadido autor en index"
$ git status
```

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213113029312.png" alt="image-20250213113029312" style="zoom:67%;" />

Por último, mostramos los logs del repositorio en una línea, en modo gráfico y con decoración:

```bash
$ git log --oneline --graph --decorate
```

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213113331402.png" alt="image-20250213113331402" style="zoom:67%;" />

### 2.6 Cuestión 6 - Fusión de las ramas

**Fusiona la rama `feature-estilos` en la rama `main` . Muestra los logs del repositorio en una línea, gráficamente y con 'decoración'.**

Al estar ya situados en la rama `main` (era necesario para resolver la cuestión anterior), la fusión de la rama llamada `feature-estilos` se hace con este comando:

```bash
$ git merge feature-estilos
```

Como se hace un `commit` de manera automática al fusionar las ramas, se nos abre el editor `vi` con un mensaje por defecto para ese `commit`. Dejamos un comentario personalizado, aunque no se indique en el enunciado:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213113834812.png" alt="image-20250213113834812" style="zoom:67%;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213113916797.png" alt="image-20250213113916797" style="zoom:67%;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213114023934.png" alt="image-20250213114023934" style="zoom:67%;" />

Una vez fusionadas las ramas, mostramos los logs del repositorio con las opciones solicitadas:

```bash
$ git log --oneline --graph --decorate
```

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213114251575.png" alt="image-20250213114251575" style="zoom:67%;" />

## 3. Trabajo en remoto

Antes de empezar con nuestra tarea, nos registramos con nuestra cuenta de educastur para poder usar SourceTree y luego comprobamos que esta herramienta está configurada con las opciones indicadas en el enunciado:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213114832480.png" alt="image-20250213114832480" style="zoom: 40%;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213115109132.png" alt="image-20250213115109132" style="zoom:50%;border:1px solid black;" />

### 3.1 Cuestión 1 - Añadir el repositorio local a SourceTree

**Continúa con el repositorio `labdist` . Añade el repositorio a SourceTree.**

Para gestionar nuestro repositorio local `labdist` con SourceTree, lo único que tenemos que hacer es ir a la opción `Add` e incluir la localización del directorio donde está alojado nuestro repositorio, tal y como se puede ver a continuación:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213115603135.png" alt="image-20250213115603135" style="zoom: 50%;border:1px solid black;" />

Una vez añadido podemos ver de forma gráfica los diversos aspectos relacionados con nuestro repositorio, como son los `commits` hechos con sus detalles, ramas creadas y fusionadas, etc.:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213120828307.png" alt="image-20250213120828307" style="zoom:67%;border:1px solid black;" />

### 3.2 Cuestión 2 - Crear repositorio remoto en GitHub y asociarlo al local

**En tu cuenta de GitHub, crea un repositorio remoto y sube al remoto los ficheros de tu repositorio local. Debes subir todas las ramas. Muestra, además, la captura de pantalla donde se vean en GitHub, algo similar a esto:**

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213121005632.png" alt="image-20250213121005632" style="zoom: 33%;" />

En primer lugar, nos vamos a **GitHub** y, tras loguearnos con nuestra cuenta de **educastur**, creamos un repositorio remoto de nombre `labdist` y de acceso público:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213121333467.png" alt="image-20250213121333467" style="zoom: 50%;" />

![image-20250213122157384](./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213122157384.png)

Una vez creado el repositorio en **GitHub**, de vuelta en **SourceTree** asociamos nuestro repositorio local con el remoto siguiendo los pasos que se muestran en las siguientes imágenes:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213122050690.png" alt="image-20250213122050690" style="zoom: 40%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213122410308.png" alt="image-20250213122410308" style="zoom:50%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213122539567.png" alt="image-20250213122539567" style="zoom:50%;border:1px solid black;" />

Luego subimos todas las ramas que tenemos definidas en nuestro repositorio local al remoto con la opción `Push`:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213122821863.png" alt="image-20250213122821863" style="zoom: 33%;border:1px solid black;" />

Y comprobamos que aparece correctamente en **GitHub**:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213123014924.png" alt="image-20250213123014924" style="zoom:80%;" />

### 3.3 Cuestión 3 - Creación de una nueva rama y cambiamos un archivo

**En el repositorio local, crea una rama `feature-index`. Añade el siguiente código dentro de la `<section class='about'>`. Añade los cambios y crea un commit con el mensaje "Añadido párrafo equipo en index.html". Sube los cambios al remoto.**

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213211058554.png" alt="image-20250213211058554" style="zoom:50%;" />

Para crear una nueva rama en nuestro repositorio local, hacemos clic en la opción `Branch` de **SourceTree**, luego le asignamos el nombre indicado a la rama y al estar marcado el checkbox `checkout new branch` en cuanto se crea pasa a ser la rama activa.

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213211728353.png" alt="image-20250213211728353" style="zoom: 45%;border:1px solid black;" />

En la siguiente captura de pantalla se puede ver que la rama activa es `feature-index`:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213211841493.png" alt="image-20250213211841493" style="zoom:50%;border:1px solid black;" />

Ahora añadimos el código facilitado en el archivo `index.html` usando **Visual Studio Code**:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213212648502.png" alt="image-20250213212648502" style="zoom:80%;" />

Subimos los cambios a la `staging area` seleccionando el fichero `index.html` en la parte inferior de la ventana de **SourceTree**, concretamente donde pone `Unstaged files`, y al pulsar en el botón `Stage Selected` el archivo queda listo para hacerle el `commit`:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213213026070.png" alt="image-20250213213026070" style="zoom:50%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213213138120.png" alt="image-20250213213138120" style="zoom:50%;border:1px solid black;" />

Para hacer el `commit` pulsamos en el botón correspondiente y escribimos el mensaje en el recuadro inferior:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213213412711.png" alt="image-20250213213412711" style="zoom:80%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213213525849.png" alt="image-20250213213525849" style="zoom:50%;border:1px solid black;" />

Para subir los cambios al remoto hacemos clic en el botón `Push`, seleccionamos las ramas que queremos subir y ejecutamos el`Push`:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213213720237.png" alt="image-20250213213720237" style="zoom:50%;border:1px solid black;" />

Comprobamos que los cambios quedan reflejados en **GitHub**:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213214123357.png" alt="image-20250213214123357" style="zoom:80%;" />

### 3.4 Cuestión 4 - Regreso a main y fusión con la rama antes creada

**En el repositorio local, fusiona la rama `feature-index` en la rama `main`.**

En primer lugar, nos movemos a la rama `main` haciendo doble clic en su nombre:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213214517844.png" alt="image-20250213214517844" style="zoom:50%;border:1px solid black;" />

Luego hago clic con el botón derecho sobre la rama llamada `feature-index` y, haciendo clic con el botón derecho sobre su nombre, selecciono la opción denominada `Merge feature-index into current branch` del menú contextual que aparece, con la que haremos esa fusión de la rama `feature-index` en `main`:

Confirmamos que queremos hacer el `merge` y este queda finiquitado:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213215034789.png" alt="image-20250213215034789" style="zoom:50%;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213215118346.png" alt="image-20250213215118346" style="zoom:50%;border:1px solid black;" />

### 3.5 Cuestión 5 - Hacemos cambios en otro archivo

**Edita el archivo `contacto.html`, borra unas cuantas líneas y muestra los ficheros con cambios pendientes y las diferencias entre ellos. Añade los cambios y haz un `commit`.**

Vamos a borrar las líneas en `contacto.html` (en concreto, borramos el `header` y el `footer`) usando el IDE **Visual Studio Code**:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213215914566.png" alt="image-20250213215914566" style="zoom:80%;" />

Para ver los ficheros con cambios pendientes y las diferencias respecto a sus versiones originales sólo hacer falta ir a la parte inferior de **SourceTree**, seleccionar el único fichero que aparece como modificado (`contacto.html`) y ver en la parte derecha las diferencias (en concreto, marca en un color rosáceo las líneas que hemos eliminado, incluidas las que originalmente estaban en blanco):

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213220245144.png" alt="image-20250213220245144" style="zoom:80%;border:1px solid black;" />

Añadimos los cambios y hacemos el `commit` correspondiente siguiendo los pasos ya vistos con anterioridad:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213220407430.png" alt="image-20250213220407430" style="zoom: 50%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213220749055.png" alt="image-20250213220749055" style="zoom:50%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213220919064.png" alt="image-20250213220919064" style="zoom:80%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213221029886.png" alt="image-20250213221029886" style="zoom:80%;border:1px solid black;" />

### 3.6 Cuestión 6 - Deshacer cambios antes hechos

**Te das cuenta del error, así que deshaz TOTALMENTE el `commit` anterior. Captura el estado actual del repositorio y asegúrate de que el fichero `contacto.html` ha recuperado las líneas borradas y no hay cambios pendientes en el repositorio.**

Para deshacer el `commit`, nos situamos en el punto del repositorio al que queremos volver (el `commit` anterior en nuestro caso) y, haciendo clic con el botón derecho sobre el mismo, seleccionamos la opción `Reset current branch to this commit`:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213221821849.png" alt="image-20250213221821849" style="zoom:50%;border:1px solid black;" />

En la ventana emergente que aparece, escogemos la opción `Hard - discard all working copy changes` en el desplegable `Using mode` para que el archivo `contacto.html` recupere su estado original:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213222037468.png" alt="image-20250213222037468" style="zoom: 50%; border: 1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213222117041.png" alt="image-20250213222117041" style="zoom:50%;" />

Confirmamos el mensaje que nos advierte que se descartarán todos los cambios que había en el directorio de trabajo y verificamos que el archivo `contacto.html` ha vuelto a su estado original y que no hay cambios pendientes en el repositorio:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213222430598.png" alt="image-20250213222430598" style="zoom:50%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213222559120.png" alt="image-20250213222559120" style="zoom:80%;" />

### 3.7 Cuestión 7 - Creación de otra rama

**Crea una rama `feature-mapa` y cámbiate a ella. Incluye este código en el archivo `contacto.html`. Añade los cambios y haz un `commit`.**

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213222725399.png" alt="image-20250213222725399" style="zoom: 50%;" />

Los pasos para crear la rama son los mismos que ya hemos visto con anterioridad:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213222954157.png" alt="image-20250213222954157" style="zoom: 50%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213223304254.png" alt="image-20250213223304254" style="zoom:50%;border:1px solid black;" />

Vemos que es la rama activa, así que incluimos el código en el archivo indicado:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213223751964.png" alt="image-20250213223751964" style="zoom:80%;" />

Añadimos los cambios a la staging area y hacemos el commit correspondiente:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213223941761.png" alt="image-20250213223941761" style="zoom:67%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213224132394.png" alt="image-20250213224132394" style="zoom:80%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213224302852.png" alt="image-20250213224302852" style="zoom:67%;border:1px solid black;" />

### 3.8 Cuestión 8 - Subir los cambios de todas las ramas al remoto

**Sube los cambios de todas las ramas al repositorio remoto y, a continuación, muestra en GitHub los cambios del archivo `contacto.html` en la rama `feature-mapa`.**

Como ya hemos hecho con anterioridad, hacemos un `Push` de los cambios subiendo todas las ramas:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213225125376.png" alt="image-20250213225125376" style="zoom:50%;border:1px solid black;" />

Luego comprobamos en **GitHub** los cambios que ha sufrido el archivo `contacto.html` en la rama `feature-mapa`:

![image-20250213225004855](./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213225004855.png)

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213225630487.png" alt="image-20250213225630487" style="zoom:80%;" />

### 3.9 Cuestión 9 - Regreso a main y fusión con la última rama creada

**En GitHub, en la rama `main`, fusiona la rama `feature-mapa`. Baja los cambios del remoto al repositorio local. Deja los dos repositorios sincronizados y muestra una captura donde se vea la página principal de tu repositorio remoto.**

Para hacer esa fusión, nos vamos a la pestaña `Pull requests` y hacemos un `pull request` de los cambios introducidos por la rama `feature-mapa`, tal y como se puede ver a continuación:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213230217490.png" alt="image-20250213230217490" style="zoom:80%;" />

![image-20250213230648453](./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213230648453.png)

Nos aparece un mensaje indicando que tenemos una `pull request` pendiente de revisión:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213230752479.png" alt="image-20250213230752479" style="zoom:50%;" />

Pulsamos en `Merge pull request` y ya estarían fusionadas las ramas `main` y `feature-mapa`:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213231001734.png" alt="image-20250213231001734" style="zoom:50%;" />

![image-20250213231111583](./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213231111583.png)

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213231150925.png" alt="image-20250213231150925" style="zoom:50%;" />

Para dejar los dos repositorios sincronizados, me voy a **SourceTree**, cambio la rama activa a `main` y hago un `Pull` para bajar los cambios desde el repositorio remoto alojado en **GitHub**:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213232029133.png" alt="image-20250213232029133" style="zoom:80%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250213232146379.png" alt="image-20250213232146379" style="zoom:80%;border:1px solid black;" />

## 4. Conflictos

Esta parte se realizará con la herramienta gráfica **SourceTree** y **GitHub**.

### 4.1 Cuestión 1 - Crear una nueva rama y añadir código a un fichero

**Crea una rama `hotfix.js`. Cámbiate a ella. Añade este código en el fichero `script.js`. Confirma el cambio y haz un `commit` con el mensaje "Corregido problema en script.js" (fíjate en los números de línea de tu editor).**

```javascript
if (mensaje.value.trim() === "") 
{
    alert("Por favor, ingrese un mensaje.");
    valid = false;
}
```

Creamos la rama `hotfix-js`, nos cambiamos a ella y añadimos en `script.js` el código facilitado:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214153115227.png" alt="image-20250214153115227" style="zoom: 50%; border: 1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214153618775.png" alt="image-20250214153618775" style="zoom: 60%; border: 1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214153510822.png" alt="image-20250214153510822" style="zoom:67%;" />

Confirmamos el cambio (es decir, añadimos el archivo a la `staging area`) y hacemos un `commit` con el mensaje que figura en el enunciado:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214153808299.png" alt="image-20250214153808299" style="zoom:67%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214154032683.png" alt="image-20250214154032683" style="zoom: 40%; border: 1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214154001432.png" alt="image-20250214154001432" style="zoom:80%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214154214002.png" alt="image-20250214154214002" style="zoom:80%;border:1px solid black;" />

### 4.2 Cuestión 2 - Volver a main y modificar ese mismo fichero

**Vuelve a la rama `main` . En el fichero `script.js` en las mismas líneas que en la cuestión anterior, añade el código siguiente. Confirma el cambio y haz un `commit` con el mensaje "corregido problema en script.js rama main".**

```javascript
if (mensaje.value.trim() === "") 
{
    alert("Ingrese un mensaje, por favor");
    valid = false;
}
```

Volvemos a la rama `main`:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214154432703.png" alt="image-20250214154432703" style="zoom:60%;border:1px solid black;" />

Añadimos el código facilitado al fichero `script.js`, haciendo que su ubicación coincida con la de las líneas que añadimos en este mismo fichero cuando estábamos en la rama `hotfix-js`:

![image-20250214154727149](./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214154727149.png)

Confirmamos el cambio subiendo el archivo a la `staging area` y hacemos el `commit` correspondiente:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214154949771.png" alt="image-20250214154949771" style="zoom:80%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214155915169.png" alt="image-20250214155915169" style="zoom:50%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214160104981.png" alt="image-20250214160104981" style="zoom:80%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214160140177.png" alt="image-20250214160140177" style="zoom:80%;border:1px solid black;" />

### 4.3 Cuestión 3 - Fusionar ambas ramas y resolver el conflicto

**Fusiona la rama `hotfix-js` en `main` . Debe producirse un conflicto. Resuélvelo como consideres oportuno. Cuando termines la resolución del conflicto sube los cambios al remoto.**

Estando seleccionada como rama activa `main`, hago clic con el botón derecho sobre la rama `hotfix-js` y escojo la opción `Merge hotfix.js into current branch`:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214160517947.png" alt="image-20250214160517947" style="zoom:50%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214160624050.png" alt="image-20250214160624050" style="zoom:50%;" />

Una vez aceptada la confirmación de que queremos fusionar ambas ramas, nos aparece un menaje advirtiéndonos de la existencia de un conflicto. Si voy a **Visual Studio Code** puedo ver marcadas las líneas que generan dicho conflicto, el cual debo resolver manualmente, ya que el sistema de control de versiones no puede saber cuál es la mejor opción.

En mi caso, me quedo con la versión que habíamos puesto en la rama `hotfix-js`:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214161055616.png" alt="image-20250214161055616" style="zoom:80%;" />

Hago clic en `Agregar cambio entrante` para que se quede el código que aporta la rama `hotfix-js`:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214161356426.png" alt="image-20250214161356426" style="zoom:67%;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214161443278.png" alt="image-20250214161443278" style="zoom:67%;" />

Una vez resuelto el conflicto en el **IDE**, lo marco como tal en **SourceTree** haciendo clic con el botón derecho sobre el nombre del archivo:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214161717316.png" alt="image-20250214161717316" style="zoom:50%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214161813180.png" alt="image-20250214161813180" style="zoom:50%;" />

Hacemos el `commit` correspondiente:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214162958449.png" alt="image-20250214162958449" style="zoom:80%;border:1px solid black;" />

Y subo los cambios al repositorio remoto:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214163130760.png" alt="image-20250214163130760" style="zoom:80%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214163218425.png" alt="image-20250214163218425" style="zoom:67%;border:1px solid black;" />

Hago la comprobación en **GitHub**:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214163342099.png" alt="image-20250214163342099" style="zoom:80%;" />

## 5. Subida de documentación al repositorio

**En la carpeta del proyecto `labdist` añade una carpeta `docs`. Copia en esta carpeta el fichero markdown y la carpeta con las imágenes. Incluye también el PDF. Añade todo al repositorio y súbelo al remoto.**

La tarea de crear la carpeta `docs` y copiar en ella el fichero `markdown` y la carpeta con las imágenes se hace con el explorador de archivos de Windows (el archivo no incluye el enlace al vídeo).

![image-20250214164935999](./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214164935999.png)

Ya sólo queda añadir estos ficheros a la `staging area`, hacer el `commit` correspondiente y subir estos archivos a **GitHub**:

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214165354578.png" alt="image-20250214165354578" style="zoom:50%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214165455698.png" alt="image-20250214165455698" style="zoom:50%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214165632143.png" alt="image-20250214165632143" style="zoom:80%;border:1px solid black;" />

<img src="./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214165907922.png" alt="image-20250214165907922" style="zoom:67%;border:1px solid black;" />

Compruebo que tengo la documentación disponible en **GitHub**:

![image-20250214170046523](./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214170046523.png)

![image-20250214170124383](./Actividad%20evaluable%202%20-%20Git%20y%20GitHub.assets/image-20250214170124383.png)

## 6. Enlaces de interés

### 6.1 Repositorio en GitHub

https://github.com/egl33817/labdist

### 6.2 Vídeo solicitado para la práctica
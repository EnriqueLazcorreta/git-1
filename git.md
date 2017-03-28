# Git
Git es un sistema de control de versiones distribuido, creado en C por Linus Torvalds para gestionar de forma colaborativa el desarrollo del kernel Linux. Es software libre y su desarrollo y mantenimiento está a cargo de la comunidad libre.

Git trabaja sobre repositorios, controlando cualquier cambio realizado sobre los archivos incluidos en un proyecto. Opera a nivel local, un proyecto git se crea en una carpeta de nuestra máquina (a la que llamaremos repositorio local), se añade información sobre el usuario de la máquina (o se utiliza la que ya está en la máquina) y se incluyen los archivos sobre los que queremos tener control. Cuando hay cambios significativos en el repositorio se puede hacer una copia íntegra (estado, instantánea, snapshoot) que quedará registrada anotando sólo los cambios producidos desde el estado anterior.

Git crea la historia de todos los cambios realizados en una carpeta (y registrados) desde su estado inicial. Permite recuperar cualquiera de los estados registrados, crear ramas a partir de cualquier estado, fusionar diferentes estados...





## Instalar git
git es software libre y se puede instalar en cualquier sistema operativo. A continuación los más populares, empezando por el que aconsejamos para desarrollar software en general, Linux.



### Linux
Instalar git en Linux es tan simple como usar tu gestor de paquetes favorito. Por ejemplo (recuerda que normalmente necesitarás privilegios de root para instalar cualquier programa):

- Arch Linux `# pacman -S git`
- Sistemas Debian, Ubuntu, Mint... `# apt-get install git`
- Gentoo `# emerge --ask --verbose dev-vcs/git`
- Sistemas Red Hat, Fedora: `# yum install git`



### macOS
Hay dos maneras de instalar Git en Mac, la más fácil es utilizar el instalador gráfico: [Git for OS X](https://code.google.com/p/git-osx-installer/)



### MS-Windows
Para instalar git en Windows podemos descargar el programa instalador en su [web oficial](http://git-scm.com/downloads).





## Configuración

Lo primero que hay que hacer antes de empezar a usar git es configurar un par de parámetros básicos que nos identifican como usuario: nombre y correo electrónico.

Git usará estos datos para identificar nuestros aportes o modificaciones.

Configurar estos parámetros es muy fácil. Desde la línea de comandos escribimos las siguientes órdenes:

`git config --global user.name "Nombre que quieras mostrar"`

y

`git config --global user.email "correo@electroni.com"`

¿qué acabamos de hacer? Veamoslo, paso a paso:

Todos los comandos de git empiezan con la palabra `git`.

En este caso, el comando en sí mismo es `config`, que sirve para configurar varias opciones de git, en el primer caso `user.name` y en el segundo `user.email`.

Habrás notado que hay un parámetro `--global` en cada uno de los comandos. Sirve para decirle a git que esos datos se aplican a todos los repositorios que abras.

Si quieres que algún repositorio concreto use unos datos distintos, puedes llamar al mismo comando, desde el directorio de ese repositorio, pero usando el parámetro `--local` en lugar de `--global`.

    Las opciones que configures como --global se almacenarán, por defecto, en un archivo de tu carpeta home, llamado .gitconfig. Las opciones --local lo harán en un archivo config dentro del directorio .git de tu proyecto.

Hay más opciones que se pueden configurar, puedes verlas (y ver los valores que tienen) con el comando:

`git config --list`

Si te has equivocado al escribir alguno de estos datos o quieres cambiarlo, sólo tienes que volver a ejecutar el comando correspondiente de nuevo, y sobrescribirá los datos anteriores.

Una opción de configuración muy cómoda es

`git config --global color.ui true`

que hace que el interfaz de git use (si es posible) colores para resaltar distintos aspectos en el texto de sus mensajes.







## Uso
Si escribimos

`git --help`

en la terminal obtendremos las primeras nociones de git.

```
usage: git [--version] [--help] [-C <path>] [-c name=value]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]

These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone      Clone a repository into a new directory
   init       Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add        Add file contents to the index
   mv         Move or rename a file, a directory, or a symlink
   reset      Reset current HEAD to the specified state
   rm         Remove files from the working tree and from the index

examine the history and state (see also: git help revisions)
   bisect     Use binary search to find the commit that introduced a bug
   grep       Print lines matching a pattern
   log        Show commit logs
   show       Show various types of objects
   status     Show the working tree status

grow, mark and tweak your common history
   branch     List, create, or delete branches
   checkout   Switch branches or restore working tree files
   commit     Record changes to the repository
   diff       Show changes between commits, commit and working tree, etc
   merge      Join two or more development histories together
   rebase     Reapply commits on top of another base tip
   tag        Create, list, delete or verify a tag object signed with GPG

collaborate (see also: git help workflows)
   fetch      Download objects and refs from another repository
   pull       Fetch from and integrate with another repository or a local branch
   push       Update remote refs along with associated objects

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.
```




## Creación de un proyecto git

Para iniciar un proyecto git podemos escribir

`git clone <origen>`

o

`git init`

El primer comando creará un directorio en el que clonará toda la información que contiene el origen. El segundo comando se ejecuta en la raíz de una carpeta local para crear el repositorio git o reiniciar uno ya existente.





## Mantenimiento del repositorio
Un repositorio git recoge la historia completa del contenido de nuestro directorio local. La historia empieza en el primer `commit` y va relatando todos los estados que hemos guardado en cada nuevo `commit`. No es un proceso automático que detecta cuándo es importante fijar un cambio, es un proceso inteligente guiado por el usuario. Git recordará todo lo que el usuario le indique que ha de recordar, ignorará aquello que no queramos/necesitemos recordar y permitirá recuperar cualquier punto de su historia.





## El archivo .gitignore

Cuando hacemos `git add .` preparamos todos los archivos que han sido modificados o añadidos. Esta suele ser la primera orden que uso cuando creo un repositorio git en una carpeta con muchos arhcivos, es más cómodo que añadir los archivos uno a uno. Pero en casi todos mis proyectos hay archivos auxiliares sobre los que no quiero guardar ninguna copia. Archivos de contraseñas, temporales, borradores, binarios compilados, archivos de configuración local...

    En proyecto de desarrollo en C o C++ suelo tener la carpeta obj para alojar los archivos objeto creados en cada compilación, y la carpeta bin para alojar los binarios creados. En mis proyectos LaTeX se crean muchos archivos temporales (log, aux, dvi, lof, lot, bit, idx, glo, bbl, bcf, ilg, toc, ind, out, blg, fdb_latexmk, fls, gz, nav, vrb, snm, pyg, loe, lol, run.xml, spl, synctex.gz...). Algunos editores de texto usan una copia temporal de los archivos que estoy editando, con el mismo nombre pero terminado en el signo "~". Estos archivos se crean de forma automática a partir de los archivos que realmente edito yo (fuentes), los podré reproducir siempre que tenga las fuentes  por lo que no necesito guardar ninguno de ellos en el repositorio git.

Git utiliza el archivo `.gitignore`, situado en el directorio raíz del proyecto, para recordar qué archivos o carpetas debe ignorar en cada proyecto. También utiliza el archivo `.config/git/ignore` para saber qué archivos deben ignorarse a nivel global. Cada línea de esos archivos puede contener un comentario ignorado por git (comienza con #), el nombre de un archivo o carpeta (`portada.png`, `obj/`, `bin/`...) o una plantilla (`*.aux`, `*~`, `password.*`...).

Podemos cambiar la ubicación del archivo global con la orden

`git config --global core.excludesfile RUTA_AL_ARCHIVO_IGNORE`

Por ejemplo, para usar el archivo `ignorar-git` de tu directorio personal ejecuta la orden:

`git config --global core.excludesfile ~/ignorar-git`

Hay ejemplos de archivos `.gitignore` en [este repositorio de GitHub](https://github.com/github/gitignore).

    Las opciones que se establecen con git config para el repositorio local se guardan en el archivo `.git/config`.





## GitHub
Para colaborar en un proyecto git es necesario recurrir a un servidor con el softawre necesario para gestionar el acceso de usuarios (con diferentes permisos) y el contenido del repositorio.





## Ejercicios
1. Crea una carpeta en tu equipo y copia en ella el capítulo [*Uso básico de git*](https://github.com/oslugr/curso-git/blob/master/texto/uso_basico.md).
2. Cambia el nombre `uso_basico` por `uso-basico`, manteniendo la extensión.
3. Crea el repositorio git.
4. Comprueba su estado.
5. Añade todos los archivos y haz tu primer `commit`.
6. Comprueba el estado del repositorio.
7. Crea el archivo `git-GUI.md`.
8. Comprueba el estado del repositorio.
9. Añade el nuevo archivo al repositorio git.
10. Comprueba el estado del repositorio.
11. Modifica el contenido de ambos archivos, guárdalos.
12. Comprueba el estado del repositorio.
13. Ejecuta el segundo `commit`.
14. Comprueba el estado del repositorio.
15. Modifica el archivo `git-GUI.md`, añadiendo información sobre alguna aplicación GUI que hayas probado (escribe todo el proceso de instalación y el uso que has hecho).
16. Comprueba el estado del repositorio.
17. Sube el repositorio a tu cuenta de GitHub (GitLab, BitBucker...).
18. Ejecuta el tercer `commit`.
19. Comprueba el estado del repositorio.
20. Sube el repositorio a tu cuenta de GitHub (...).
21. Comparte el repositorio con tus compañeros.
22. Copia la información del archivo `git-GUI.md` de cada uno de tus compañeros (no crees un nuevo archivo).
23. Actualiza el repositorio en el servidor y añade permisos de edición a tus compañeros.






## Fuentes
- *Pro Git, everything you need to know about git* (second edition), Scott Chacon and Ben Straub. Apress
- [*Git y Github, tutorial básico de uso bajo GNU/Linux*](https://victorhckinthefreeworld.com/2012/09/26/git-y-github-tutorial-basicode-uso-bajo-gnulinux/)
- [*Tutorial de Git en Español*](http://blog.santiagobasulto.com.ar/programacion/2011/11/27/tutorial-de-git-en-espanol.html)
- [*Comandos básicos para manejarse con Git y GitHub*](https://dreyacosta.com/comandos-basicos-para-manejarse-con-git-y-github/)
- [*Manual básico de Git*](https://ticket.cdmon.com/es/support/solutions/articles/7000006246-manual-b%C3%A1sico-de-git)
- [*Uso básico de git*](https://github.com/oslugr/curso-git/blob/master/texto/uso_basico.md)

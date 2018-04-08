# Segunda Parte

Hagamos un repaso... ¿Qué aprendimos en la primera parte de este curso?

## Contenido

<details>
<summary>Expandir</summary>

- Inicializar un repositorio.
- Los tres estados de git.
- Revisar los commits realizados.
- Ejemplos prácticos.
- Recuperar archivos.
- Eliminar y revertir commits.
- Inspeccionar commits

</details>

<br>

Todo lo que vimos anteriormente se enfocaba en las principales funcionalidades de git orientado al uso local.
Lo que veremos ahora será el uso más potente de git, mediante repositorios externos y trabajo colaborativo.

<br>

## Repositorios externos

Otras de las cualidades de los controles de versiones como git es su uso externo, trabajar con repositorios que están en la nube (github, gitlab, bitbucket) o en un servidor remoto.
Para los siguientes ejemplos ustilizaremos :octocat: https://GitHub.com :octocat:

<br>

## ¿Qué es GitHub?

GitHub es un servicio en la nube que permite alojar nuestros proyectos usando el control de veriosnes git.
GitHub tiene dos versiones disponibles:

- Gratis: Los repositorios son públicos pero se permite seleccionar quien puede hacer commits.
- De pago: Los repositorios son privados e ilimitados, permite seleccionar quien puede ver y hacer commits.

>Para hacer un poco más interactivo el curso, solicito puedan crear una cuenta gratuita en [GitHub](https://www.github.com)

<br>

## Creando un repositorio remoto

Una vez que estamos registrados y logueados en GitHub, crearemos nuestro primer repositorio. Para esto tenemos que ir al botón <kbd>Start a project</kbd> y crearemos un repositorio gratuito, en este caso se llamará "test".<br>
Marcamos la casilla **Initialize this repository with a README** para crear un achivo readme que será el de presentación y vamos al botón <kbd>Create repository</kbd>.

<p align="center"><img src="https://raw.githubusercontent.com/coneking/git_curso/master/images/repo_test.png" width="600" /></p>

<br>

## Clonando un repositorio remoto

Clonar un repositorio basicamente es descagarlo desde la nube con toda su configuración, esto incluye el directorio ".git" que se crea al inicializarlo.<br>
Para clonar el repositorio existen dos opciones, una es clonarlo a través de su URL y la otra es clonarlo mediante llave SSH, para este caso usaremos la primera opción.<br>
Seleccionamos el botón <kbd>Clone or download</kbd>, copiamos la URL, ejemplo: https://github.com/coneking/test.git y en un directorio de nuestro equipo ejecutamos el comando `git clone "URL"`.

<p align="center"><img src="https://raw.githubusercontent.com/coneking/gir_curso/master/images/clonar.png" width="400" /></p>

<br>

```sh
$ mkdir repo_web; cd repo_web

$ git clone https://github.com/coneking/test.git
	Cloning into 'test'...
	remote: Counting objects: 3, done.
	remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
	Unpacking objects: 100% (3/3), done.
``` 

>Al listar los directorios tendremos uno con el nombre del repositorio (test), dentro encontraremos la carpeta ".git" y el archivo README.md que se generaron al crear el repositorio en GitHub. Con esto ya podemos hacer nuestras modificaciones y commits.

<br>

## Agregando un repositorio remoto

Existe otra forma de trabajar con un repositorio remoto y es agregándolo (algo similar a clonar).<br>
Nuevamente copiamos la URL de nuestro repositorio y en un directorio nuevo ejecutamos `git init` y `git remote add origin URL`

```sh
$ mkdir repo_web; cd repo_web

$ git init
	Initialized empty Git repository in C:/Users/Git/Documents/repo_web/.git/

$ git remote add origin https://github.com/coneking/test.git

$ git pull origin master
	remote: Counting objects: 3, done.
	remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
	Unpacking objects: 100% (3/3), done.
	From https://github.com/coneking/test
	 * branch            master     -> FETCH_HEAD
	 * [new branch]      master     -> origin/master
```

>Ahora tenemos nuestro repositorio en el directorio creado y listo para hacer cambios.

<br>

## Push y Pull

Cuando tenemos nuestro repositorio agregado en nuestro equipo podemos hacer cambios al proyecto y subirlos a GitHub mediante "push".<br>
**Push**: permite subir cambios al repositorio remoto una vez que creamos un commit, los cuales tamién son exportados.<br>
**Pull**: permite descargar cambios que se hayan generado en el repositorio remoto (commits, archivos, ramas) para mantener actualizado el repositorio local.<br>

**Ejemplo Push:**

Haremos un cambio en el achivo README.md y luego un commit.

```sh
$ echo -e "# Nuestro repositorio de prueba\n Este un repositorio de prueba y haremos nuestro primer **push**." > README.md

$ git commit -am "Primer push"
	warning: LF will be replaced by CRLF in README.md.
	The file will have its original line endings in your working directory.
	[master ea849b9] Primer push
	 1 file changed, 2 insertions(+), 2 deletions(-)
```


Finalmente subiremos los cambios con push.

```sh
$ git push origin master
	Counting objects: 3, done.
	Delta compression using up to 4 threads.
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (3/3), 312 bytes | 78.00 KiB/s, done.
	Total 3 (delta 0), reused 0 (delta 0)
	To https://github.com/coneking/test.git
	   3a6c6bf..ea849b9  master -> master
```

<br>

**Ejemplo Pull:**

Haremos un cambio al archivo README.md desde la web de GitHub y luego en nuestro repositorio local lo descargaremos mediante pull.

```sh
$ git pull origin master
	remote: Counting objects: 3, done.
	remote: Compressing objects: 100% (2/2), done.
	remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
	Unpacking objects: 100% (3/3), done.
	From https://github.com/coneking/test
	* branch            master     -> FETCH_HEAD
	ea849b9..2e35a24  master     -> origin/master
	Updating ea849b9..2e35a24
	Fast-forward
	README.md | 9 +++++++--
	1 file changed, 7 insertions(+), 2 deletions(-)
```

>**Nota**: Es recomendable hacer un pull del repositorio antes de enviar nuestros cambios, esto debido a que, si el repositorio externo está más actualizado que el nuestro (debido a cambios de otras personas) no dejará que se hagan "push".

<br>

## Ramas

El concepto de ramificación puede ser uno de los puntos más fuertes de git, y es que se basa en el trabajo colaborativo paralelo de un proyecto.
Para explicar un poco más a fondo como funcionan las ramas sigan a Octocat [:octocat:](/ramas.md).<br>
Por ahora nos centraremos en la creación de ramas y la fusión entre ellas.

### Creación de Ramas

En git podemos crear cuantas ramas estimemos y una vez cumplan su función eliminarlas. Para saber en que rama nos encontramos utlizamos el comado `git branch` donde un "\*" nos notificará la rama actual.<br>
Si deseamos crear una rama usamos el comando `git branch nombre_de_la_rama`.<br>

**Ejemplo:**

```sh
$ git branch
* master

$ git branch desarrollo

$ git branch
  desarrollo
* master
```

<br>

Para cambiar a una rama existente usamos el comando `git checkout nombre_de_la_rama`.

```sh
$ git checkout desarrollo
Switched to branch 'desarrollo'

$ git branch
* desarrollo
  master
```
>Existe la opción de crear una rama y cambiarse a ella de forma automática, esto se hace ejecutando `git checkout -b nombre_de_la_rama`.

Ahora que tenemos las ramas *master* y *desarrollo* podemos trabajar de forma paralela con los mismos archivos del proyecto pero de forma independiente, esto quiere decir que los cambios que se realicen en una rama, no serán percibidos por las otras.<br>

### Ejemplo trabajo con ramas

Crearemos un archivo en la rama *desarrollo* luego haremos su respectivo commit y listaremos los archivos del proyecto.

```sh
$ git checkout desarrollo
Switched to branch 'desarrollo'

$ echo "trabajo en rama desarrollo" >> desarrollo.txt

$ git add desarrollo.txt
warning: LF will be replaced by CRLF in desarrollo.txt.
The file will have its original line endings in your working directory.

$ git commit -m "Archivo creado en la rama desarrollo"
[desarrollo 869a6ba] Archivo creado en la rama desarrollo
 1 file changed, 1 insertion(+)
 create mode 100644 desarrollo.txt

$ git log --oneline
869a6ba (HEAD -> desarrollo) Archivo creado en la rama desarrollo
2e35a24 (origin/master, master) Commit desde GitHub
ea849b9 Primer push
3a6c6bf Initial commit

$ ls
desarrollo.txt  README.md

```

<br>

Ahora cambiaremos a la rama *master* y veremos que no existirá registro del archivo y el commit hecho en *desarrollo*.

```sh
$ git checkout master
Switched to branch 'master'

$ ls
README.md

$ git log --oneline
2e35a24 (HEAD -> master, origin/master) Commit desde GitHub
ea849b9 Primer push
3a6c6bf Initial commit

```

Como pueden notar el trabajo que se haga en una rama no afecta a las demás y una vez que se quieran pasar los cambios o mejoras del proyecto a otra rama, se puede hacer mediante un *merge* o fusión.

<br>

## Merge entre ramas

Para integrar los cambios de una rama a otra se utiliza el concepto de *fusión* o *merge*. La sintaxis del comando es la siguiente y se debe ejecutar en la rama a la cual queremos integrar los cambios `git merge "rama_con_cambios_a_integrar"`.

<br>

**Ejemplo**

Si queremos fusionar los cambios que hicimos en la rama *desarrollo* a la rama *master* se haría de la siguiente manera.

```sh
$ git checkout master
Switched to branch 'master'

$ git merge desarrollo
Updating 2e35a24..869a6ba
Fast-forward
 desarrollo.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 desarrollo.txt

$ ls
desarrollo.txt  README.md

$ git log --oneline
869a6ba (HEAD -> master, desarrollo) Archivo creado en la rama desarrollo
2e35a24 (origin/master) Commit desde GitHub
ea849b9 Primer push
3a6c6bf Initial commit

```

Al ejecutar `git log --oneline` se puede notar que tanto la rama *desarrollo* como la rama *master* están apuntando al mismo commit. En este momento las ramas están fusionadas y si no requerimos más de la rama *desarrollo* la podemos eliminar.

<br>

## Eliminación de Ramas

Para eliminar una rama se ejecuta el comando `git branch -d nombre_de_la_rama`, en este caso eliminaremos la rama *desarrollo* la cual ya fue fusionada en *master*.

```sh
$ git branch -d desarrollo
Deleted branch desarrollo (was 869a6ba).
```
>**Nota**: Si la rama a eliminar tiene commits que no han sido fusionados, git notificará esto y además recomendará, si estamos seguros de eliminar la rama con sus cambios, usar el parámetro `-D`.

<br>

## Conflictos

Al trabajar con ramas, se nos puede presentar el caso de tener *conflictos*.
Esto puede deberse a que el archivo que queremos subir, se encuentra desactualizado respecto al que existe en el repositorio.

Si tratamos de realizar un push, aparece un mensaje similar al siguiente:

```
Updates were rejected because the remote contains work that you do
not have locally. This is usually caused by another repository pushing to the same ref. You may want to first integrate the remote changes
```

En este caso, git avisa del conflicto en el o los archivos y propondrá una manera de solucionarlo.

Podemos ejecutar un *git pull* para traer los cambios mas actualizados. Si el sistema no es capaz de realizar el merge o fusión, de forma automática, nos creará un escenario para que nosotros decidamos que cambio queda como definitivo.

```
git pull origin master
...
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

Si se está usando el cliente de GIT Bash para Windows, se señalará de forma gráfica, que pasamos a una rama temporal para resolver el conflicto. Se nos añadirá la etiqueta *MERGING* al nombre de la rama que estemos trabajando.

El archivo con conflicto aparecerá con etiquetas, donde indicarán los cambios actuales con la etiqueta *HEAD*.

```
# Ejemplo
<<<<<<< HEAD
Cambio dia 01 enero
=======
Cambios dia 02 enero
>>>>>>> 57894ff9df56e924521009fb95b17655c4598fe5
```

Acá podemos editar y dejar los cambios que correspondan. También deberemos eliminar las líneas agregadas para señalar las modificaciones (<<< === >>>). Luego de guardar los cambios, ya podemos ejecutar *git commit* y *git push* para sincronizarlos.

<br>

***

## Conclusión

Con esto damos por terminado el curso de git donde se abordaron varios temas, desde inicializar un repositorio local, hasta trabajarlo con herramientas web como GitHub.
Es recomendable trabajar a diario con git, ya sea, con pruebas y archivos normales o desarrollos propiamente tal, la idea es que se acostumbren a utilizar su sintaxis y aprovechar todas las bondades que posee esta herramienta.<br>
Si tienen dudas sobre algún tema en particular o algo que no se nombrara en este curso, los invito a que creen un [Issue aquí](https://github.com/coneking/git_curso/issues) y lo solucionaremos a la brevedad :thumbsup:
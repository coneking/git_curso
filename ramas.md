## Ramas

**Ejemplo**

Para explicarlo de una manera más sencilla diremos que tenemos una línea de tiempo con commits hechos por la rama **master** (rama que se crea por defecto).


<p align="center"><img src="https://raw.githubusercontent.com/coneking/git_curso/master/images/rama1.png" width="400" /></p>

Para comenzar crearemos una rama con el comando `git branch "nombre_de_la_rama"`.

```sh
$ git branch testing
```

> Para ver las ramas locales se ejecuta el comando `git branch` donde un "\*" indicará en cual rama estamos actualmente.
> Para listar todas las ramas (locales y remotas) ejecutamos el mando `git branch -a`.

<br>
<br>

<p align="center"><img src="https://raw.githubusercontent.com/coneking/git_curso/master/images/rama2.png" width="400" /></p>

Como muestra la imagen, tenemos dos ramas; ***master*** y ***testing***, ambas apuntando al mismo commit *f30ab*.<br>
Nos cambiaremos a la rama "testing" con el comando `git checkout "nombre_de_la_rama"` para trabajar en paralelo a la rama master.

```sh
$ git checkout testing
	Switched to branch 'testing'
```

<br>

<p align="center"><img src="https://raw.githubusercontent.com/coneking/git_curso/master/images/rama3.png" width="400" /></p>

>**HEAD** se mueve al cambiarse entre ramas, en este caso a **testing** y podemos observar que ambas ramas apuntan al mismo commit "f30ab".

<br>
<br>

<p align="center"><img src="https://raw.githubusercontent.com/coneking/git_curso/master/images/rama4.png" width="400" /></p>

<br>

En este ejemplo la nueva rama creó el commit *c2b9e*. Los cambios agregados en este commit no los puede ver la rama "master" ya que, si nos cambiamos a la rama master, veremos que HEAD sigue estando en el commit *f30ab*.

<br>

Continuando con el ejemplo nos devolveremos a la rama "master" y al hacer un commit la línea de tiempo se bifurcará.

```sh
$ git checkout master
	Switched to branch 'master'
	Your branch is up to date with 'origin/master'.
```

<p align="center"><img src="https://raw.githubusercontent.com/coneking/git_curso/master/images/rama5.png" width="400" /></p>

Ahora tenemos un commit creado por en la rama testing (c2b9e) y otro en la rama master (87ab2). Cada rama hará cambios en su propia línea de tiempo, los cuales al final se *fusionarán* en la rama principal del proyecto.<br>
Con esto se demuestra el trabajo colaborativo/paralelo en un proyecto mediante ramas.

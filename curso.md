# ¿Qué es git?

Git es un control de versiones distribuido. ¿Qué quiere decir esto de distribuido?
Quiere decir que no hay un servidor central como tal, varias personas tienen una copia del repositorio y así pueden contribuir con el proyecto o bien usar su proyecto como un repositorio para otras personas.


# Estados de git

Git se basa en tres estados:

* Modificado (modified)
* Preparado (added)
* Confirmado (committed)

<br>

## Inicializar un directorio

Lo primero que haremos será inicializar un directorio como un repositorio git.
Para esto crearemos un directorio cualquiera y ejecutaremos `git init`.

	$ mkdir mi_proyecto; cd mi_proyecto
	$ git init

Con esto tenemos nuestro directorio inicializado.
Lo podemos ver, ya que, se creó un directorio oculto `.git`, este directorio contiene toda la configuración necesaria para usar git.

<br>

## Primer estado (Modificado)

Lo que vamos a ver ahora es el primer estado de git.
Para ello empezaremos por crear un archivo nuevo y le añadiremos contenido.

	$ echo "Hola Mundo" > archivo.txt

<br>

Git automáticamente reconocerá que se hizo un cambio y lo podremos ver con el comando `git status`.

	$ git status
	On branch master

	No commits yet

	Untracked files:
	  (use "git add <file>..." to include in what will be committed)

	        archivo.txt

	nothing added to commit but untracked files present (use "git add" to track)

<br>

## Segundo estado (Preparado)

Como pueden ver, git dice que hay un archivo que no tiene seguimiento (Untracked) y para agregar un archivo y que tenga seguimiento se use el comando `git add`.

	git add archivo.txt

<br>

Ejecutamos nuevamente git status y veremos que ahora el archivo está "preparado" pero aún no hay commit.
También git nos dirá qué si queremos quitar el archivo añadido al área de preparación, podemos ejecutar el comando `git rm --cached <file>`

	$ git status
	On branch master

	No commits yet

	Changes to be committed:
	  (use "git rm --cached <file>..." to unstage)

	        new file:   archivo.txt


Si ejecutamos esto último, el archivo nuevamente indicará que no tiene seguimiento.

<br>

## Tercer estado (Confirmado)

Ahora lo que haremos será un commit del archivo, un commit generará un punto en el tiempo del cual podremos consultar modificaciones o volver directamente en él pero eso lo veremos más adelante.
Si se fijan en el mensaje que arroja, entregará información como por ejemplo; desde que rama se hizo el commit (en este caso desde master), le asignará un ID único, este hash es mucho más largo de lo que se muestra ahí pero git permite trabajar con los 7 primeros caracteres de un commit y también cuantos archivos fueron incluidos en el commit (en este caso uno) y que el cambio fue de `1 inserción (+)`.


	$ git commit archivo.txt

	warning: LF will be replaced by CRLF in archivo.txt.
	The file will have its original line endings in your working directory.
	[master (root-commit) f154089] Mi primer commit
	 1 file changed, 1 insertion(+)
	 create mode 100644 archivo.txt

Al ejecutar `git commit` se abrirá el editor de texto predeterminado que tengamos, en mi caso "vi" y aquí tendremos que poner un título y una descripción.
Esto nos servirá para saber que se hizo en ese commit, quien lo hizo y en que horario.
Posiblemente si no han configurado su usuario y correo, git lo solicitará antes de hacer un commit, pues como dije el commit debe mostrar quien hizo el cambio.

	$ git config --global user.name "Usuario"
	$ git config --global user.email "Correo"

<br>

Una manera más rápida de hacer un commit es con la opción "-m", con esto no se abrirá el editor y sólo podremos poner un título al commit.

	$ git commit -m "Título" archivo

<br>

Esto cumple los tres estados de git, modificar el archivo, preparar el archivo agregándolo al área de preparación (git add) y confirmar el cambio generando un commit (git commit).

<br>

## Histórico de commits 

Cada commit queda registrado y lo podemos ver con el comando git log.
git log tiene muchas opciones, ya que, permite buscar por ejemplo los últimos 3 commit, o los commit que hizo cierta persona, filtrar por fechas, etc.
Para más información `git log --help` los enviará al manual del comando.

	$ git log

Para una mirada un poco más limpia podemos ejecutar el comando git log con el parámetro `--oneline`.

	$ git log --oneline

La vista es mucho más simple y muestra lo necesario, el ID del commit, el comentario del commit, si tuviese un tag también lo mostraría.
Un tag es un identificador que le podemos dar al commit para no tener que acordarnos del id que se crea por defecto y simplificarnos un poco más la lectura.

<br>

## Agregando más commits

Digamos ahora que tenemos más archivos.
	
	for i in archivo2.txt archivo3.txt archivo4.txt; do echo "línea de prueba" >> $i; done

Ahora en nuestro directorio de trabajo tenemos cuatro archivos, sin embargo, git sólo reconoció cambios en tres (los que acabamos de crear).
Lo que podemos hacer es agregar todo los archivos que tienen cambios de una vez con el comando `git add .` pero para este ejemplo primero sólo agregaremos uno de los archivos y posteriormente los otros dos.
	
	$ git add archivo2.txt

<br>

Si ejecutamos `git status` podremos ver que sólo un archivo, en este caso archivo2.txt, está listo para hacer un commit y los otros dos aún están pendientes de agregarse al área de preparación.

	$ git status
	On branch master
	Changes to be committed:
	  (use "git reset HEAD <file>..." to unstage)

	        new file:   archivo2.txt

	Untracked files:
	  (use "git add <file>..." to include in what will be committed)

	        archivo3.txt
	        archivo4.txt

Esto sería útil cuando sabemos que el archivo que modificamos ya está listo y no necesita nada más y queremos confirmarlo lo antes posible para, por ejemplo, dejarlo en producción. Mientras que a los otros dos aún les podemos seguir haciendo cambios.
Entonces le damos un commit al "archivo2.txt" y sólo nos quedarían los otros dos archivos.

	$ git commit archivo2.txt

<br>

Ahora para agregar todos los archivos que tienen modificaciones, sí ejecutaremos `git add .`.
Podemos ver que los archivos están listos para hacer un commit.

	$ git add .

	$ git status
	On branch master
	Changes to be committed:
	  (use "git reset HEAD <file>..." to unstage)

	        new file:   archivo3.txt
	        new file:   archivo4.txt

<br>

Se podría hacer un commit por cada archivo como lo hicimos con el archivo2.txt pero en este caso queremos que ambos pertenezcan al mismo commit, así que no especificaremos el nombre.

	$ git commit -m "Agregando archivos 3 y 4"
	[master df5f162] Agregando archivos 3 y 4
	 2 files changed, 2 insertions(+)
	 create mode 100644 archivo3.txt
	 create mode 100644 archivo4.txt

<br>

Ahora al consultar con `git log --oneline` mostrará los tres commit que hemos hecho por el momento.

	$ git log --oneline
	df5f162 (HEAD -> master) Agregando archivos 3 y 4
	f552bbb agregando archivo2.txt
	f154089 Mi primer commit

<br>


## Casos prácticos de uso.

¿Por ejemplo, que pasa si no tenemos git y estamos trabajando un archivo y por alguna razón borramos parte o todo el contenido del archivo y guardamos los cambios?
***¡¡¡Perdimos la info!!!*** ... Veámoslo de la siguiente forma.
Vamos a copiar un script básico, lo agregaremos al repositorio y luego lo editaremos.

	$ cp ../valida_edad.sh .
	$ git add valida_edad.sh
	$ git commit -m "Script que valida edad"
	[master 36a4c4d] Script que valida edad
	 1 file changed, 6 insertions(+)
	 create mode 100644 valida_edad.sh

Ahora en una situación normal si borramos parte de la información del archivo... Perdimos parte del script, porque como buen admin no hicimos el respaldo del archivo.
Para nuestra suerte git nos reconoció que hubo un cambio en el archivo que él tenía bajo seguimiento y al hacer un git status nos dirá que bien podemos preparar el archivo añadiéndolo al área de preparación o revertir el cambio que sufrió el archivo con `git checkout -- valida_edad.sh`

	$ git checkout -- valida_edad.sh

Revisamos el archivo y veremos que ha vuelto a su estado original.
Y `git status` nos dirá que nuestro directorio de trabajo está limpio.

	$ git status
	On branch master
	nothing to commit (working directory clean)

<br>

Si por otro motivo, modificamos el archivo, le borramos parte del contenido y además lo preparamos con `git add` para luego hacer un commit, el comando `git checkout --` no nos servirá.
Para esto git también nos recomienda antes de hacer un commit que podemos quitarlo del área de preparación con el comando `git reset HEAD`.

	$ git reset HEAD valida_edad.sh

Veremos que con git status el archivo ya no está en el área de preparación, sino que nos ha notificado que se modificó, en este momento podremos ejecutar `git checkout --` para revertir los cambios realizados al archivo.

	$ git checkout -- valida_edad.sh
	$ cat valida_edad.sh

Como ven git en la mayoría de las veces nos recomendará cosas antes de ponernos a hacer commits y sólo es cosa de leer.

<br>

## Eliminando un commit

Este último comando que nos recomendó git (git reset) es un poco peligroso porque si bien nos ayuda a recuperar cambios, también destruye commit en el tiempo.
Este es un ejemplo; Digamos que modificamos el script y estamos seguros de los cambios, los guardamos e hicimos su commit.

	$ git commit -am "Modificando script de edad"
	[master 1ca1bad] Modificando script de edad
	 1 file changed, 1 insertion(+), 1 deletion(-)

Pero claro al ejecutar el script no funciona por los cambios que efectuamos, ahora lo que podemos hacer, y es una de las características de los sistemas de control de versiones, es que podemos volver en el tiempo un cambio.


Veamos el historial de commit.

	$ git log --oneline
	1ca1bad (HEAD -> master) Modificando script de edad
	36a4c4d Script que valida edad
	df5f162 Agregando archivos 3 y 4
	f552bbb agregando archivo2.txt
	f154089 Mi primer commit

Sabemos que en el commit anterior el archivo funcionaba bien, entonces lo que podemos hacer son dos cosas:

  - Podemos volver en el tiempo el archivo específico que está con problemas.
  - Podemos volver en el tiempo al punto donde nuestro proyecto estaba funcionando correctamente.

<br>

### Para el primer caso podemos hacer lo siguiente

Como sabemos que, en nuestro proyecto, sólo el archivo "valida_edad.sh" es el que tiene problemas, podemos ir al commit donde estaba funcionando bien y traer de vuelta sólo ese archivo con el comando `git checkout "ID_COMMIT" archivo`

	$ git checkout 36a4c4d valida_edad.sh

Al ejecutarlo el archivo tendrá la misma información que tenía en ese commit y podremos realizar un nuevo commit indicando que se corrigió el archivo.

	$ git commit -m "Se recupera script de edad" valida_edad.sh
	[master 7bda560] Se recupera script de edad
	 1 file changed, 1 insertion(+), 1 deletion(-)

<br>

### Para el segundo caso podemos hacer lo siguiente

Con el comando `git reset` agregándole el commit donde estaba funcionando todo bien, podremos volver en el tiempo a ese punto de nuestro proyecto.

	$ git reset 36a4c4d
	Unstaged changes after reset:
	M       valida_edad.sh


Al ejecutar un git status notificará que el archivo tuvo un cambio y lo podremos recuperar como lo vimos anteriormente con `git checkout --` y listo.

	$ git checkout -- valida_edad.sh

<br>

#### Principales diferencias entre estas opciones
   
   - La primera es menos invasiva puesto que sólo recuperamos uno o más archivos de un punto específico y añadimos un nuevo commit para restaurarlo.

   - La segunda modifica la línea del tiempo y esto en ocasiones puede no ser muy bueno porque si habían algunos archivos con cambios en algún commit posterior del que elegimos para volver, se perderán. :sweat:


>**Importante**: Para usar git reset se debe estar muy seguro de lo que se quiere hacer y también así conocer principalmente los parámetros `--hard` y `--soft` de este comando, ya que, `--hard` hará que al elegir volver a un commit, no preguntará si se quieren agregar al área de preparación y luego hacer un commit de los cambios en los archivos, esto lo hará automáticamente cambiando el **HEAD** a dicho commit.
Por otro lado `--soft` volverá al commit y dejará los archivos que tengan cambios listos para un nuevo commit.

<br>

## Revirtiendo un commit

También existe una tercera opción y posiblemente sea la más conveniente de realizar, la cual es deshacer cambios de commits sin eliminarlos con el comando `git revert`

Supongamos que creamos tres nuevos archivos más un cambio en el archivo valida_edad.sh y para cada uno de ellos un commit.

	$ git log --oneline
	dabe37c (HEAD -> master) Cambios en script
	d2c8ace Se agrega archivo5.txt
	68205bd Se agrega archivo4.txt
	2cf473d Se agrega archivo3.txt
	36a4c4d Script que valida edad
	df5f162 Agregando archivos 3 y 4
	f552bbb agregando archivo2.txt
	f154089 Mi primer commit


Comparo cada uno de los commit con `git diff`, por ejemplo, `git diff 36a4c4d 2cf473d` dirá que se añadió el archivo "archivo3.txt". `git diff 36a4c4d HEAD` que es lo mismo a buscar diferencias entre el commit 36a4c4d y el actual, dirá que se agregaron los tres archivos y hubo una modificación en el archivo "valida_edad.sh".

Lo que se podría hacer es un `git revert` por cada uno, pero cada vez que se ejecuta un revert, se tendrá que crear un commit, lo que puede causar mucho desorden en nuestra línea de tiempo.

Para tal caso al comando se le puede pasar el parámetro `-n` o `--no-commit` y finalmente `git revert --continue` que lo recomienda el mismo git.

	$ git revert -n dabe37c d2c8ace 68205bd 2cf473d
	$ git revert --continue

	$ git log --oneline
	226c239 (HEAD -> master) Revert "Se revierten los últimos 4 commits"
	dabe37c Cambios en script
	d2c8ace Se agrega archivo5.txt
	68205bd Se agrega archivo4.txt
	2cf473d Se agrega archivo3.txt
	36a4c4d Script que valida edad
	df5f162 Agregando archivos 3 y 4
	f552bbb agregando archivo2.txt
	f154089 Mi primer commit

Nuestro directorio de trabajo quedará como lo teníamos en el commit **36a4c4d** sin perder los commits posteriores que quizás a otra persona le parecieron buenos.

<br>

## Inspeccionar un commit

Otra cosa que nos permite hacer git es ir a un commit en particular y ver como estaba nuestro proyecto en ese momento, es como ir a inspeccionar que se hizo en ese punto de la línea de tiempo.
El comando para esto es `git checkout` seguido del commit al que queremos ir.

	$ git checkout 2cf473d
	Note: checking out '2cf473d'.

	You are in 'detached HEAD' state. You can look around, make experimental
	changes and commit them, and you can discard any commits you make in this
	state without impacting any branches by performing another checkout.

	If you want to create a new branch to retain commits you create, you may
	do so (now or later) by using -b with the checkout command again. Example:

	  git checkout -b <new-branch-name>

	HEAD is now at 2cf473d... Se agregar archivo archivos

<br>

Si ejecutamos el comando `git branch` veremos que ya no estamos en la rama "master", sino en una temporal con el nombre del commit.

	git branch
	* (HEAD detached at 2cf473d)
	  master

Desde este punto del tiempo podemos revisar cada archivo y si hacemos algún cambio no afectará a nuestra rama master, ya que, como dije es una rama temporal. Es más, al momento de crear la rama temporal nos sugiere que para guardar los commit que hagamos, creemos una nueva rama con el comando `git checkout -b nombre_de_la_rama`.

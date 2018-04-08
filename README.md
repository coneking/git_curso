# Curso Básico Git

## Control de versiones<br>

Muchas personas quizás utilizan el versionamiento sin saberlo.<br>

### ¿Cómo?
Copiando archivos antes de modificarlos (backup).<br>

### ¿Qué es un control versiones?
Un VCS (Version Control System) es un sistema que verifica y registra si uno o varios archivos han tenido modificaciones.<br>
Al registrar un cambio se puede volver a alguna de esas versiones en cualquier momento.<br>

**Desventaja:** 
* Sólo una persona puede hacer cambios en los archivos a la vez (cambios locales).

Para integrar la colaboración de más de una persona a la modificación de archivos (desarrolladores) se creó una versión mejorada de los VCSs, los **CVCS** (Centralized Version Control System).<br>

<br>

## Centralized Version Control System (CVCS).
Un CVCS utiliza un servidor central que contiene el proyecto, los usuarios descargan los archivos que necesitan para trabajarlo y posteriomente subirlos con los cambios efectuados.

**Ventajas:**
* Mejor administración, se puede saber quien hace los cambios y donde.
* Los usuarios tienen conocimiento de los cambios que se han generado en el proyecto.

**Desventaja:**
* Único punto de falla. Si falla el servidor central, falla todo.

Para atacar este problema se crearon los **DVCS** (Distributed Version Control System) como Git.<br>

**Ventajas:** 
* Cada persona que trabaja en el proyecto tiene una copia instantanea localmente.
* Permiten administrar varios flujos de trabajo.

<br>

<p align="center">
<img src="https://raw.githubusercontent.com/coneking/git_curso/master/images/DVCS.png">
</p>

>Repositorio clonado en ComputerA y ComputerB.
<br>
<br>
<br>

![alt text](https://raw.githubusercontent.com/coneking/git_curso/master/images/GitLogo.png)

<br>

## Gestión Distribuida.

* Git permite respaldar completamente un proyecto.
* Trabajar localmente en un proyecto para posteriormente enviar sus cambios al servidor remoto.
* Administrar un proyecto en base a "ramas" de trabajo.

Mediante el checksum, Git verifica si un archivo tuvo un cambio o no.<br>
Por ejemplo, en un proyecto con 3 archivos, si sólo uno fue modificado, Git no guardará nuevamente los otros dos.
Simplemente revisará que no se hicieron cambios y hará una referencia al archivo original, algo como un link simbólico, generando una instantanea del proyecto.

<br>

<p align="center">
<img src="https://raw.githubusercontent.com/coneking/git_curso/master/images/Fundamento.png">
</p>

>La imagen muestra que en la segunda versión del proyecto hubieron cambios en los archivos A y C pero B no fue modificado por lo cual se hace una referencia del archivo B de la instantánea anterior.

<br>

## Estados de Git.

1. Modificado (modified).
2. Preparado (staged o added).
3. Confirmado (committed).

Ejemplo:

* Modifico o creo el archivo "mi_archivo.txt" (modified).
```
echo "hola" > mi_archivo.txt
```

* Preparo el archivo añadiéndolo al área de preparación (staged o added).
```
git add mi_archivo.txt
```

* Confirmo el cambio realizado, guardándolo como una instantánea en nuestro directorio local Git (committed).
```
git commit -m "Mi primer commit" mi_archivo.txt
```

<br>

## Curso

Para entender mejor como funciona git vamos directo a los casos prácticos en el siguiente [curso](/curso.md).

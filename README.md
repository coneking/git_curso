# Curso Básico Git

## Control de versiones<br>

Muchas personas quizás utilizan el versionamiento sin saberlo.<br>

### ¿Cómo?
Copiando archivos antes de modificarlos (backup).

### ¿Qué es un control versiones?
Bueno un VCS (Version Control System) es un sistema que verifica y registra si uno o varios archivos han tenido modificaciones.<br>
Al registrar un cambio se puede volver a alguna de esas versiones anteriormente registradas.<br>

**Desventaja:** 
* Sólo una persona puede hacer cambios en los archivos a la vez (cambios locales).

Para integrar la colaboración de más de una persona a la modificación de archivos (desarrolladores) se creó una versión mejorada de los VCSs, los CVCS (Centralized Version Control System).<br>

## Centralized Version Control System (CVCS).
Un CVCS utiliza un servidor central que contiene el proyecto, los usuarios descargan los archivos que necesitan para trabajarlo y posteriomente subirlos con los cambios efectuados.

**Ventajas:**
* Mejor administración, se puede saber quien hace los cambios y donde.
* Los usuarios tienen conocimiento de los cambios que se han generado en el proyecto.

**Desventaja:**
* Único punto de falla. Si falla el servidor central, falla todo.
<br>
Para atacar este problema se crearon los DVCS (Distributed Version Control System) como GIT.

**Ventajas:** 
* Cada persona que trabaja en el proyecto tiene una copia instantanea de él localmente.
* Permiten administrar varios flujos de trabajo mediante ramas.
<br>


![alt text](https://github.com/coneking/git_curso/images/DVCS.png "Ejemplo")

# GIT.



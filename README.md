# Curso Básico Git

## Control de versiones<br>

Muchas personas quizás utilizan el versionamiento sin saberlo.<br>

### ¿Cómo?
Copiando archivos antes de modificarlos (backup).

<br>
### ¿Qué es un control versiones?
Bueno un VCS (Version Control System) es un sistema que verifica y registra si uno o varios archivos han tenido modificaciones.<br>
Al registrar un cambio se puede volver a alguna de esas versiones anteriormente registradas.<br>

**Desventaja:** 
* Sólo una persona puede hacer cambios en los archivos a la vez (cambios locales).

Para integrar la colaboración de más de una persona a la modificación de archivos (desarrolladores) se creó una versión mejorada de los VCSs, los CVCS (Centralized Version Control System).<br>

<br>
## Centralized Version Control System (CVCS).
Un CVCS utiliza un servidor central que contiene el proyecto, los usuarios descargan los archivos que necesitan para trabajarlo y posteriomente subirlos con los cambios efectuados.

**Ventajas:**
* Mejor administración, se puede saber quien hace los cambios y donde.
* Los usuarios tienen conocimiento de los cambios que se han generado en el proyecto.

**Desventaja:**
* Único punto de falla. Si falla el servidor central, falla todo.
<br>
Para atacar este problema se crearon los DVCS (Distributed Version Control System) como Git.

**Ventajas:** 
* Cada persona que trabaja en el proyecto tiene una copia instantanea localmente.
* Permiten administrar varios flujos de trabajo.
<br>

<p align="center">
<img src="https://github.com/coneking/git_curso/blob/desarrollo/images/DVCS.png">
</p>

<br>
<br>

![alt text](https://github.com/coneking/git_curso/blob/desarrollo/images/GitLogo.png)

<br>

Git permite respaldar completamente un proyecto.<br>
Permite trabajar localmente en un proyecto para posteriormente enviarlo al servidor remoto.<br>
En administrar un proyecto en base a "ramas" de trabajo.
Mediante el checksum, Git verifica si un archivo tuvo un cambio o no.<br>
        
Por ejemplo, en un proyecto con 5 archivos, si sólo uno fue modificado, Git no guardará nuevamente los otros cuatro.
Simplemente revisará que no se hicieron cambios y hará una referencia al archivo original, algo como un link simbólico.


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



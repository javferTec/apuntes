# CONTROL DE VERSIONES

## ¿Qué es y para qué sirve?

**Git** es un sistema de control de versiones libre y distribuido diseñado para gestionar proyectos. Su objetivo es controlar y gestionar una enorme cantidad de ficheros de forma fácil y eficiente.

Se basa en repositorios que se inicializan en un directorio concreto y tienen toda la información de los cambios realizados.

## Partes de un repositorio

El repositorio remoto puede ubicarse en GitHub, GitLab, Bitbucket, SourceForge, entre otros. Es una copia del repositorio de git que se encuentra alojado en un servidor o en un sitio distinto al local.

El repositorio local se divide en:
- **Directorio de trabajo** (working directory): donde se almacena el contenido del repositorio.
- **Área de preparación** (staging area o index o cached): donde están indicados los cambios de confirmación.
- **Repositorio local** (local repository): donde están todas las versiones de manera local.
## Estados de un fichero

- **untracked**: Son ficheros que existe en el área de trabajo pero no existen para git. *No ha sido añadido al directorio*.
- **staged**: Son ficheros modificados que se añadirán al siguiente commit. *Antes de añadirlos a staging area*.
- **committed**: Son ficheros que se guardaron en el ultimo commit y que no han sido modificados desde dicho commit. *Fichero no modificado en el repositorio*.
- **modified**: Son ficheros que se han modificado desde el último commit pero que aun no se han añadido para el próximo commit. *Ha sido editado desde el último commit y git conoce*.
- **ignored**: Son ficheros que git ignora (a través del fichero .gitignore).

Si queremos añadir un fichero al *staging area* lo hacemos con:

``` bash
git add fichero
```

Si queremos confirmar los cambios del *stage*:

``` bash
git commit -m "mensaje"
```

Si queremos quitar un fichero del stage:

``` bash
git restore --staged fichero
git reset fichero # Menos usado
```

Si queremos que un fichero vuelva al working directory:

``` bash
git rm --cached fichero
```

Si queremos que un fichero vuelva al estado del último commit tras modificaciones:

```bash
git restore fichero
git checkout fichero # Menos usado
```

Si queremos ver el estado de los fichero:

```bash
git status
```


## Sincronización de Git

Una misma rama en git puede estar en varios sitios a la vez. El repositorio es el historio donde están todos los commits que se han hecho.



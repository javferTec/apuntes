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

## Sincronización de Git y Ramas

Una misma rama en git puede estar en varios sitios a la vez. El repositorio es el histórico donde están todos los commits que se han hecho.

Explicación de las ramas suponiendo que estamos en ``master``:

- Carpeta local o **área de trabajo** o árbol de trabajo: Es donde están los ficheros con lo que trabajamos nosotros directamente mientras programamos.

- **Repositorio loca**l: Es el repositorio que tenemos en nuestro ordenador.
	- **_Rama master_**: Es donde se guardan los ficheros al hacer commit
	- **_Rama origin/master_**: Es una copia que hay del repositorio remoto. 
	
- **Repositorio remoto**: Es un repositorio que está en otra máquina.
	- **_Rama master_**: Es donde queremos copiar los commits de nuestra rama master. Al hacer referencia a una rama de un repositorio remoto, se usara la expresión ``origin master`` con un espacio en medio.


Si queremos movernos entre ramas:

```bash
git switch master
git checkout master # Comando más antiguo, se recomienda switch
```

Si queremos crear una nueva rama:

```bash
git branch <nombreRama>
```

Si queremos crear una rama y automáticamente movernos a ella:

```bash
git switch -c <nombreRama>
git checkout -b <nombreRama> # Comando antiguo, se recomienda switch
```

Si queremos movernos a un commit en concreto con ``switch``:

```bash
git switch --detach <hashDelCommit>
```

Si queremos movernos a una rama de tipo ``origin/rama`` debemos hacerlo con:

```bash
git switch --detach origin/rama
```

==_NOTA:_ **DETACH** nos informa de que no se puede crear commit al lugar al que nos movemos. Es decir, no podemos trabajar en ese lugar==

Si queremos publicar los cambios de una rama:

```bash
git push origin master
git push
```

Si queremos obtener los cambios del remoto:

```bash
git fetch origin master
git fetch

# FETCH TIENE LA OPCIÓN --PRUNE PARA BORRAR LAS CARPETAS QUE HAN SIDO BORRADAS EN REMOTO
git fetch --prune
```

Si queremos obtener y aplicar en nuestra área de trabajo los cambios del remoto:

```bash
git pull
```


> [!DANGER]
> ``git pull`` hace un fetch y un merge, lo que puede producir conflictos que posteriormente haya que solucionar y puede que el histórico se modifique.


Para _mergear_ lo que hay en la rama ``origin/master`` en  la rama ``master``:

```bash
git merge origin/master
```

Si queremos eliminar una rama en local:

```bash
git branch -d <rama>
```

Si queremos eliminar una rama en remoto:

```bash
git push origin -d <rama>
```

Para fusionar ramas tenemos dos opciones:

```bash
git merge <nombreRama>
git rebase <nombreRama>
```
#### ¿Diferencia entre Merge y Rebase?

**Merge** conserva la historia original de la rama fusionada y **rebase** reescribe la historia de la rama para que parezca que los commits se aplicaron de forma lineal. En otras palabras, **merge** fusiona e incorpora los cambios especificados a la rama actual _(donde está el HEAD)_ mientras que **rebase** mueve el HEAD a la rama especificada.

_NOTA: HEAD es donde estamos ubicados._

## Remotes

En Git un "remote" hace referencia a un servidor de Git donde subimos el código. Por defecto cuando hacemos git clone se crea un remote llamado origin.

Si queremos ver la lista de remotes:

```bash
git remote -v
```

Para añadir un remote:

``` bash
git remote add otroservidor <URL>
```

## Borrado de commits

**``GIT RESET``** modifica el estado actual de un fichero.

Tienes diferentes opciones:

- **--soft**: Vuelve a un commit y conserva los cambios en el directorio de trabajo y en el stage.
```bash
git reset --soft <hashCommit>
```

- **--mixed**: Los cambios se conservan en el stage.
```bash
git reset --mixed <hashCommit>
```

- **--hard**: Los cambios no se conservan.
```bash
git reset --hard <hashCommit>
```

|         | Borra los commits siguientes | Se modifica área de trabajo | Modifica staged area |
| ------- | :--------------------------: | :-------------------------: | :------------------: |
| --hard  |              Si              |             Si              |          Si          |
| --mixed |              Si              |             No              |          Si          |
| --soft  |              Si              |             No              |          No          |

> [!NOTA]
> La opción **HEAD~1** hace referencia al último commit.

## Deshacer commits

**``GIT REVERT``** deshace un commit y crea uno nuevo volviendo al estado del commit especificado.

```bash
git revert HEAD~1
git revert <hashCommit>
```

- Prepara un nuevo commit que deshace el último commit pero sin realmente hacer el commit. Lo que hace el modificar los ficheros y añadirlos a la staged area. Después se hace el commit. La opción **``--no-commit``** es útil porque nos permite revisar que va a hacer el commit y nos permite hacer alguna modificación más. Si no estamos interesados en hacer el commit lo podemos abortar con ``git revert --abort`` o usar el ya conocido ``git restore --staged --worktree fichero``.

```bash
git revert --no-commit HEAD~1
git commit -am "Mensaje de commit" # -a para añadir a stage & -m para el mensaje del commit
```

> [!NOTA]
 > ``git restore --staged --worktree fichero``  restaura el archivo `fichero` tanto en el área de preparación como en el directorio de trabajo a su estado en el último commit, eliminando cualquier cambio realizado.

## Configuración

#### **.gitkeep**

Por defecto Git no sube las carpetas vacías, por lo que si queremos que las suba hay que añadir algún fichero. Por convención se suele crear un fichero llamado `.gitkeep` y al ya haber algún fichero, git subirá esa carpeta.

#### **.gitignore**

El fichero `.gitignore` permite indicar que carpetas no se deben subir a git. El fichero debe estar en el raíz del proyecto de git.
#### Almacenando contraseñas

Normalmente trabajamos siempre en nuestro ordenador y no queremos todas las veces volver a poner la contraseña. En ese caso se puede decir a git que la almacene y no nos la vuelva a pedir:

- No te vuelve a pedir la contraseña en 15 min
```bash
git config --global credential.helper cache
```

- Almacena la contraseña en el disco en texto plano y nunca mas te la vuelve a pedir.
```bash
git config --global credential.helper store
```

## Stash

Es un almacén que permite guardar los cambios de los que todavía no se quiere hacer un commit.

- Guardar solo lo modificado (estén o no en el staged area):
```bash
git stash push
```

- Guarda todos los ficheros aunque NO estén en la stage area. Es decir, también los ficheros nuevos. Y al hacer el pop se restaura el estado en el staged area.
```bash
git stash push --include-untracked
```

| <br>                                                      | _Por defecto_ | `--include-untracked` | `--all` |
| --------------------------------------------------------- | :-----------: | :-------------------: | :-----: |
| Los ficheros modificados (estén o no en el _staged area_) |       ✓       |           ✓           |    ✓    |
| Los ficheros nuevos                                       |               |           ✓           |    ✓    |
| Los ficheros los ignorados                                |               |                       |    ✓    |

- Y si luego queremos recuperar los cambios se hace con:
```bash
git stash pop --index # Si no se añade --index, no se restaurará el staged area.
```


## Log

El comando git log permite ver el histórico de commits.

- Ver los commits en una única línea cada commit.
```bash
git --no-pager log --pretty=oneline
```

- Ver los commits indicando que campos queremos mostrar e indicando el formato de la fecha.
```bash
git --no-pager log --pretty=tformat:"%h %cn %cd %s" --date=format:"%d/%m/%Y %H:%M:%S"
```
![[gitLog.png]]

## Mensajes de commit

Los mensajes de commit deben seguir el siguiente formato:

```message
type(#issue):titulos

Explicación (opcional)
```
Siendo

- **`type`**
    - _feat_: Si se añade una nueva funcionalidad (feature)
    - _fix_: Si se arregla (fix) un error
    - _docs_: Si solo cambia cosas de la documentación
    - _style_: Si solo se cambia el estilo del código como tabuladores, puntos y comas, formateo, etc.
    - _refactor_: Si se cambia el código para mejorar su calidad pero sin modificar la funcionalidad. Eso se llamada refactorizar.
    - _test_: Si se cambian cosas relacionadas con test automáticos.
    - _chore_: Si se cambian cosas relacionadas con el despliegue.
- **`#issue`**: Es el Nº de la incidencia a la que hace referencia.

Ejemplos:

- Se arregla el fallo 45 que se llama "Falla si la fecha está vacía"
```message
  fix(#45):Falla si la fecha está vacía
```

- Se añade la nueva funcionalidad llamada "Mostrar el listado de los pacientes" con Nº 456
```message
feat(#456):Mostrar el listado de los pacientes
```

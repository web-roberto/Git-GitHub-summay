# Comandos de Giy y Github de DECODE
###### https://www.youtube.com/playlist?list=PLfYElkGZxzgb93uFgXw-mcCPvIYz4EFF6
### Trabajamos en el shell de GitBASH
### AREA TRABAJO     AREA ENSAYO      REPOS.LOCAL      REPOS.REMOTO
### ---git add----------> |--git commit--> | ---git push--> |
### <------ git checkout/mege ------------ | <--git fetch---|
### <----------------------git pull-------------------------|
### master --------------------------------------------- origin/maste
### si hay 6 commits delante de orgin/master, hay que hacer un push
### ¿Queremos que publiquemos el proyecto en una dirección web?
 SI: git branch  gh-pages  → crea la rama ‘gh-pages’
	git checkout gh-pages → cambia a la rama  ‘gh-pages’
	git remote add origin https://github.com/web-roberto/portfolio-cv.git
	git push -u origin  gh-pages
     LA SEGUNDA Y OTRAS VECES: git push(en lugar de git push -u origin gh-pages)
    SI NO FUNCIONA, entrar en Github y subirlo con ‘Add file’. ‘Upload file’
 NO: substituir gh-pages por master o por main
### ¿CONVERTIR UN PROYECTO DE MAIN A G-PAGES (PUBLICARLO)?
 SI:Click en ‘settings’. Abajo hasta ‘pages’.selecciones en el desplegable ‘main’, despues /root
    WEB EXTERIOR(de GithubPages) → https://web-roberto.github.io/portfolio-cv  
     INTERNAMENTE → https://github.com/web-roberto/portfolio-cv 
## VIDEO 2: Instalación en Windows
 Descargar git para windows
 git --version, git help
 cd a la carpeta deseada, editar .gitignore y añadir carpetas a no copiar, git add .
 git commit -m "first commit"
 Crear cuenta en github y crear un nuevo repositorios -> nos da las instrucciones para hacer un PUSH desde git######
 Crear un usuario: git config --global user.name 'robertoweb'   Ver un usuario: git config --global user.name
 Añadir el email: git config --global user.email "roberto.alonso.gandia@gmail.com" Ver email: git config --global user.email

## VIDEO 3: instalacion en Debian y Linux
## VIDEO 4: Comandos básicos: ADD, COMMIT y PUSH
git init -> crea un directorio .git oculto -> para verlo ls -a. No tocar nada. Borrar el .git si queremos borrar todas las copias hechas.
git status -> ver estado: ver si falta por subir algun archivo e indicar la rama en la que estamos
touch .gitignore -> crea el archivo .gitignore
## VIDEO 5: Crear, modificar, eliminar ramas: GIT BRANCH
git branch = git branch --listv -> ver todas las ramas del repositorio
git branch desarrollo -> crea una nueva rama
git checkout desarrollo -> nos movemos hacia la rama 'desarrollo' -> al final de la linea pone (desarrollo)
git status -> indica la rama en la que estamos
git push --set-upstream origin desarrollo. En github ahora se ha creado la rama 'desarrollo'
Cuando estemos seguros que los cambios en 'desarrollo' son los que queremos, haremos una fusion entre las dos ramas.
git branch -d desarrollo -> borra la rama 'desarrollo'. dice: "error: The branch is not fully merged"
git branch -D desarrollo -> confirma el borraod de 'desrrollo' aunque no se haya realizado el merged
git branch -m desrrollo development -> cambia el nombre de la rama de 'desarrollo' a 'development'

## VIDEO 6: Fusionar ramas: GIT MERGE
Creamos una rama y la subimos a github:
  git branch modificaciones
  git checkout modificaciones
  touch function.js
  touch style.css
  add .
  git commit -m "1st commit"
  git push --set-upstream origin modificaciones -> crea un repositorio en github
Fusionamos las ramas modificaciones y develpoment
  git checkout development -> nos situamos en la rama 'desarrollo'
  git merge modificaciones -> unimos la rama 'modificaciones' a la que nos encontramos ahora
      usa la estrategia 'fast-forward' : como si trajera los fichero de 'modificaciones' a mi rama actual
  Situacion: yo modifico function.js y una chica style.css
    Yo hago nano functions.js y añado un comentario //
      git commit -a -> editamos el mensaje del commit
    Ahora yo hago de chica: voy a la otra rama: git checkout modificaciones y hago nano styles.css y añado /**/
      git commit -a -> editamos el mensaje del commit
      git push
  git checkout development -> volvemos a mi rama, development
  gir merge modificaciones -> usa la estrategia 'recursive': mira linea por lineas los archivos modificados de las dos ramas y los une.
  git push -> subimos al servidor el merge de los dos (development)
Fusionamos el resultado de la fusion anterior con la rama master
  git checkout master
  git merge development -> estrategia 'fast-forward'
  git push ---> ERROR: pq no hemos hecho ningun commit ni add sobre 'master' todavía.

## VIDEO 7: Git Pull de una rama
Descargamos la copia de github y machacamos nuestro repositorio local
git pull=git fetch + git merge -> de repos remoto a local y area de trabajo (merge el repos local y remoto)

## VIDEO 8: Git Fetch y Trucos de Git Log
git branch y vemos que estamos sobre la *master
git fetch -> de master remoto a masterlocal
git branch -r -> vemos las ramas en remoto y que no tenemos en local
git checkout simulacion -> vamos a rama 'simulacion' en repositorio local
git log -> historico de los commits realizados. Salimos del comando con 'q'
git log --online -> vemos los logs en una sola linea
git log --online --graph -> vemos el grafico de division de las ramas
git log --online --graph --decorate --all -> vemos el grafico de division de las ramas, nº de commit

## VIDEO 9: Git clone + Fork. Clone vacio
Vamos a github. Code. HTTPS, copiamos 
Vamos a gitbash, "git clone" y pegamos -> git clone https://...git  ->>> descarga de la rama 'main'
y crea una carpeta en mi ordenador con el nombre del repositorio 
podemos cambiar el nombre de la carpeta que crea y donde lo descarga todo: git clone https://...git repodescargado
cd descargado -> podemos crear ramas dentro...
git branch dev
git branch development
git checkout development
git commit --allow-empty ´-m "commit inicial vacio de la rama(en development)"
git push --set-upstream origin development-> crea la rama en el repositorio remoto y sube la rama vacia de development
###Fork
FORK: vamos al github de otra persona y click sobre 'fork' y me crea una copia de ese repositorio sobre mi cuenta de github
Se usa cuando queremos mejorar el codigo de esa persona pero no tenemos permisos. Hacemos las mejoras en mi hithub y le
pedimos  esa persona un PULL REQUEST

## VIDEO 10: Deshacer un commit(de un repositorio local). Revert+Reset
git revert HEAD-> vuelve al commit anterior o a uno especificado anteriormente
git revert nºcommit -> con git log --online --decorate . para salir 'q'
     podemos modificar el mensaje de revert commit
git reset --hard HEAD~1 -> vuelve al commit anterior y borra los ficheros 
git reset --soft HEAD~1 -> vuelve al commit anterior pero no borra los fichero del ultimo commit que estan en mi carpeta
  actual preparados para subirlos a un nuevo commita otra vez.
   anterior y despues los fichero del ultimo anterior
git status para ve los commits de diferencia entre el repositorio local y el remoto
git commit --amend -m "nuevo mensaje" -> modificar el mensaje del comit anterior
## Agregar archivos a un commit
touch readme.txt, git add readme.txt, git commit --amend -m "añado el fichero readme.txt al commit"

## VIDEO 11: Rebase en Git
USAR EL REBASE A.N.T.E.S. de un PUSH (de subir al repos.remoto)
Rebase: reescribe la historio de mis commits y crea un log mas sencillo entendible
Hace los 'git merge' 'fast-forward': trae los cambios de la rama principal a tu rama de desarrollo y los reorganiza dentro de tu código.
Lo hacemos estando en 'desarrollo', sobreescribimos este historial y hacemos un rebase de 'master', para despues hacer un 
'merge' mas sencillo de 'desarrollo' hacia 'master'
git branch desarrollo, git checkout desarrollo, 
touch archivo1.txt, git add archivo1.txt, git commit -m "archivo1.txt" 
touch archivo2.txt, git add archivo2.txt, git commit -m "archivo2.txt"
git log --online --graph -10 -> 10 ultimas lineas del log de 'desarrollo'

git checkout master
touch archivo3.txt, git add archivo3.txt, git commit -m "archivo3.txt"
git log --online --graph -10 -> 10 ultimas lineas del log de 'master'

git checkout desarrollo
touch archivo4.txt, git add archivo4.txt, git commit -m "archivo4.txt"
git log --online --graph -10 -> 10 ultimas lineas del log de 'master'
git rebase master
git log --online --graph -10 -> aparece el 'archivo3.txt' de 'master' en el historial de 'desarrollo' 
             -> esto facilita el 'merge' posterior desde 'master' con 'fast-forward'
Ya hemos terminado de desarrollar y vamos a pasar a produccion, entonces lo llevamos todo a 'master'
git checkout master
git merge desarrollo -> trae todos los cambios de 'desarrollo' a 'master'
git log --online --graph -10 
ahora tenemos en 'master' los archivos:  archivo1.txt, archivo2.txt, archivo3.txt, archivo4.txt 

## VIDEO 12: Gitignore
puede ponerse una expersion general: *.txt, un directorio: midirectorio/, un comentario empezando por #
git rm <nombre_archivo> -> eliminar un archivo de un repositorio local
git rm --cached <nombre_archivo> -> eliminar un archivo de un repositorio remoto
git rm --cached <nombre_archivo> --f -> eliminar un archivo de un repositorio remoto, forzando el borrado
git status -> aparece 'deleted', 'untracked' significa que debe hacerse un 'git add'

## VIDEO 13: Tags
Tag: una manera sencilla de identificar commits, es un puntero a un commit. Podemos hacer un checkout con el tag y tambien
se usa para hacer un fix o mejora de mi código.
Usamos los 'tag' como versiones publicadas, esto facilita el mantenimiento.

Tags en repositorio local:
git tag v.0.0.1 -m "primera version" -> crea un 'tag' apuntando al HEAD de la rama actual
git log --online --graph --decorate
git tag v.0.0.1 4600cgd -m "segunda version" -> crea un 'tag' apuntando al commit con ese numero de la rama actual

Tags en repositorio remoto:
git push --tags

git checkout v.0.0.2 -> usamos este commit en mi carpeta. Tambien podemos subir usando este tag
git tag -> muestra los tag del repositiorio local actual
git tag -d v.0.0.2 -> elimina el tag. Despues habría que actualizar el repositorio remoto borrando el tag del remoto, 
   yendo a github, situandonos encima del tag y click en 'delete'

## VIDEO 14: 7 Secretos. Git profesional
1) Hace pull constantemente, asi los merge funcionan mejor y hay menos errores
2) El mensaje del commit debe ser realmente descriptivo
3) Asociar commits a tareas
4) Crear un BRANCH por cada tarea a realizar pq los MERGE funcionan muy bien. Cada tarea se asigna a un compañero, varias ramas en paralelo que corresponden con las tareas que se realizan en paralelo por varios programadores.
5) No usar: add . para no subir ficheros indeseados. Usar: git commit -a para archvios ya subidos y que se modifican. 
   Para los archivos nuevos, usar: add <archivo>
6) Solo hacer push a programas bien comprobados
7) Usar un .gitignore en cada carpeta -> *.jpg
8) Añadir el README.md  

## VIDEO DE FATZ DE MARKDOWN: https://www.youtube.com/watch?v=oxaH9CFpeEE



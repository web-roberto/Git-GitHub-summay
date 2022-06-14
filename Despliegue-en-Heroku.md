# Roberto: Despliegue en Heroku
Pasos:
Mis cuentas en Heroku:
* roberto.alonso.gandia@gmail.com/Adosat2020
* roberto.alonso.heroku1@gmail.com/Adosat2020@
* roberto.alonso.heroku2@gmail.com/Adosat2020@

* Videos relacionados:
  * [Video despliegue en Heroku de Nodejs y Mysql](https://www.youtube.com/watch?v=dw1y7qwNb4E&t=647s "Click to go to the Video")
  * [Video Using Heroku Config Vars](https://www.youtube.com/watch?v=FEK2i4f8gNU "Click to go to the Video")
___
* Software necesario:
  * Postman -> testear nuestra API
  * Sequel Pro -> acceder al Mysql remoto en Heroku
___
## El objetivo es tener en Heroku el NODEJS y el MYSQL juntos

1. Descargar Heroku CLI (heroku dev center)-- no es una app que se vea fisicamente, solo aparece cuando hacemos 'heroku login'
1. Crear una carpeta para descargar un clon de Github del proyecto Nodejs + Mysql ya correcto
1. Clonar un proyecto hecho.  Ejemplo: Nodejs y Mysql ya creado
    de Dominicode https://github.com/domini-code/node_mysql
    Descargar el zip
1. Ir a la carpeta, 'code .' para abrir en VSCode. Editar package.json y poner en 'dependencias' express y mysql
1. No hacemos 'npm install' pq no queremos ejecutarlo aqui. Suponemos que ya funciona la aplicación.
1. Hacemos 'ctrl + ñ' y hacemos 'heroku login'. Nos logeamos
1. Cambiar el codigo para usar el root y su contraseña desde una variable del sistema (asi es seguro)
1. Comprobar enlace de repositorio local al remoto de Heroku`git remote -v`
1. Creamos un repositorio remoto en Heroku con un nombre aleatorio: `heroku create`
1. Cambiamos el nombre del repositorio remoto anterior: `heroku apps:rename --app <nombre_aleatorio> <nombre_que_yo_quiero>`
1. Hacemos 'click' sobre el enlace que nos da y vemos 'Heroku. welcome to your new app'
1. Comprobamos que está creado el nuevo repositorio remoto: `git remote -v` . Ya podemos hacer un 'push' de nuestro 'master'.
Recordar que al hacer el `git clone` ser creo un git local
1. `git status` `git add package.json` `git commit -m "package changed"`
1. Subimos del repositorio local al remoto de Heroku `git push heroku master`
1. Vamos a la pagina donde publica nuestra API de node y nos dice que hay un error. Vamos a ver el log de los errores
1. `heroku logs --tail`
## en Heroku la BDD por defecto es Postgres, pero usaremos Mysql
### Cread ADDON de Mysql para la Aplicacion en Heroku
1. `heroku addson create:cleardb:ignite` Creo que pide una tarjeta de crédito para continuar (aunque es gratis).
Nos devuelve un CLEARDB_DATABASE_URL
1. `heroku config | grep CLEARDB_DATABASE_URL` y nos devuelve la URL de conexión de mi app en Node a la BDD creada en Heroku.
El formato es: mysql://<usuario>:<password>/<host>/<nombreBDD>?reconnect=true
1. Creamos la variable DATABASE_URL: `heroku config:set DATABASE_URL='<cadena de arriba de mysql://>' -> entre comillas simples `
1. Vamos al app.js y cambiamos el usuario, password, base de datos de la cadena de conexión que tenemos
1. Debemos usar variables de entorno como dice en este video y no dentro del código: 
[Video Using Heroku Config Vars](https://www.youtube.com/watch?v=FEK2i4f8gNU "Click to go to the Video")
### El addon ya está creado. Ahora necesitamos crear una tabla
1. Abrimos nuestro cliente de BDD, Heidi por ejemplo y nos conectamos a la BDD de Mysql en Heroku usando la cadena de conexión
1. Creamos mi tabla 'customers'con mis campos 'name varchar 150, city varchar 100'
1. Añadimos algun registro a la tabla
1.  `git status`
1. `git add .`
1. `git commit -m "Mysql connection set in the code of Nodejs"`
1. `git push heroku master`
1. Refrescamos la URL de mi API en el navegador y sale 'Welcome to my API' que es la respuesta a la ruta /
## Vamos a POSTMAN a probar todas la rutas
1. Copiamos la URL de nuestra API añadiendo las rutas y comprobamos un GET
1. Comprobamos un POST (nuevo registro de la tabla)
1. Comprobamos un DELETE
## Cambiamos a un fichero externo el USUARIO, CONTRASEÑA, BDD 
[Video Using Heroku Config Vars](https://www.youtube.com/watch?v=FEK2i4f8gNU "Click to go to the Video")
1. Vamos a Heroku, a nuestra aplicacion, en Settings al final pone 'Reveal Config Vars'. Ponemos un KEY y un VALUE.
Estas son las variables de entorno que yo leo dentro de mi Node con process.env.<VARIABLE_ENTORNO>
1. Cambiamos nuestro codigo y ponemos las process.env y lo subimos todo otra vez 

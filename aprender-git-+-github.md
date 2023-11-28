
# Notas Git y Git Hub (Curso by Brais Moure) tomadas con [Boostnotes](https://boostnote.io/florfa/Aprender-Git-+-GitHub-dCaba6d968dad84cc5b5cabbf2984c7d0f)

## Clase 1

Abrir Windows Powershell (tecla `Windows` + `X`)

Ver version de git
```
git
git --version
```
Ver ayuda
```
git –help
```

### Comandos para manejarse dentro de la terminal

Mostrar el directorio
```
ls
```
desplazarse entre las carpetas del directorio (cd + `tab`)
```
cd Desktop
```
para volver para atrás
```
cd ..
```
como saber el path del directorio en el que trabajo
```
pwd
```
crear carpeta
```
mkdir "Hello Git"
```
para entrar en esa carpeta 
```
cd '.\Hello Git\'
```
para limpiar la consola
```
clear
```
Para crear un archivo tengo que usar touch 
```
touch hellogit3.py
```

### Configuracion de Git global en el usuario

```
git config --global user.name "usuario"
git confit --global user.email "sdnfiosd@email.com"
```
inicializar git, se creara una carpeta oculta .git en el directorio que estemos
```
git init
```
con eso se crea una rama que se llama master y a partir de ahora puedo empezar a "sacar fotos" en distintos momentos de mi proyecto. Mi proyecto será la carpeta Hello Git que cree.

Para saber cual es el estado de mi git
```
git status
```
Ahora me aparecen los ficheros que no guarde, aparecen como Untracked files. Para generar la primera fotografia del fichero debo hacer
```
git add hellogit.py
```
(si quiero subir todos los ficheros y para evitar escribir el nombre cada vez que lo subo hago, ```git add .```)

Ahora aparece en verde los Changes to be committed, es decir, los ficheros que esta en stage. Ahora debemos lanzar la fotografia, paso siguiente
```
git commit
```
Aparece una ventana de dialogo que me pide que haga algun comentario. Podria estar haciendo alguna aclaracion o redaccion sobre lo que estoy subiendo. Una forma abreviada para que no me aparezca el editor de texto es hacer el comentario directamente en el git commit
```
git commit -m "Este es mi primer commit"
```
Ya se hizo la fotografia

Como chequearlo? Me va a decir que usuario hizo algun cambio, muestra mensaje, fecha y hora, te da el historia
```
git log
```
Si tengo cambios en los archivos, cada ves que ponga  ```git status```  me va a avisar que hay un fichero que esta modificado o que hay otros ficheros que no subi, etc. 

Si quiero ir un paso atras con el archivo uso 
```
git checkout
```
Tambien puedo usar para ver que archivos no he guardado la nueva version, y luego usar el checkout para volver a version anterior.
```
git reset
```

Si quiero ver de una manera mas ordenada y aesthetic el historial
```
git log --graph
git log --graph --pretty=oneline
git log --graph --decorate --all --oneline
```
Podemos configurar un alias, permite hacer como un local o global (como en stata) con un comando que quiero repetir siempre y para evitar escribir toda la linea le puedo poner un alias con nombre. En el ejemplo, el alias lo llamo tree
```
git config --global alias.tree "log --graph --decorate --all --oneline"
```
Entonces luego puede correr siempre lo que esta abajo, y me va a corre el git + lo que hay en el alias.
```
git tree
```
Si quiero ignorar un archivo para las funciones del add/commit, 
```
touch .gitignore
```
Ahi se crea el fichero .gitignore y adentro debo ingresar los archivos que quiero que me ignore. 
Estos se escriben  en windows como
**/(nombre del fichero que quiero ignorar)
En mac como 
**/.(nombre del fichero que quiero ignorar)

Generalmente, hay ficheros que se usan para el normal funcionamiento de la pc, pero pueden ser ignorados tranquilamente para no molestar el flujo el git add. En Mac son los archivos .DS_Store, en Windows son desktop.ini
En estos casos, se abre el  .gitignore con un procesador de texto y se escribe

**/.DS_Store
**/desktop.ini

Asi, luego hacemos un git add y un git commit y ya nos olvidamos de esos archivos de la pc que no estan relacionados al proyecto.

Ya en una misma rama, podemos ir modificando los archivos. Uno puede con un comando ver que ha ido cambiando en los archivos sin tener que hacer una fotografia. El comando te va a decir cuales fueron los cambios que hiciste en el fichero desde la ultima fotografia.
```
git diff
```
y luego me va a decir cuantas lineas cambiaron y que cosas saque o agregue, ver ejemplo en la imagen
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/588dee27a2a93f446cca339e60e0e53011092a5445d3b6d49ede2dbb593b5c66-imagen.png)

### Desplazamientos en el git
Para movernos podemos usar el git checkout y colocar el ID de la fotografia a la que queremos volver. 
```
git checkout (ID de la foto)
```
Por default git siempre esta sobre la ultima foto, por ejemplo
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/340f4353ae906005fdf9bf0a4f4ec2a3988f40af8d64da8b90e87fe7fd7081c8-imagen.png)

Ahora quiero moverme a una foto previa, supongamos a 9e8ab8d
entonces pongo
```
git checkout 9e8ab8d
git log --decorate --all --oneline
```
Si me quedaron cosas por commitear me va a aparece un cartel y no me va a cambiar la ubicacion
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/f543e9d45528be24bc9455ac03ac40adfb3bcfec71d7261619c9c861d13da039-imagen.png)
Puedo commitear  (add+commit) o descartar (restore)
Luego, cambio la foto donde estoy trabajando
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/c36905907aca0789c81740a76cbd6d5cf12c377008d181de5b58bef633eaeddd-imagen.png)
Ver donde esta el HEAD
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/7149ad0c4b448b77dbe5701b1abc806b5e1cf76dc12d8e5dfcb33eb2dd1192c6-imagen.png)
Hay ficheros que pueden aparecer y desaparecer. Estrictamente no es que se eliminan de la pc local, sino que estan como "ocultos" en el .git (que es el archivo oculto dentro del directorio). De esa forma, es siempre posible recuperar las fotos en las distintas instancias del proyecto sin eliminar o modificar archivos en el sentido estricto. Eso es el concepto de sistema distribuido.

## Clase 2

Si yo quiero borrar fotos que habia generado porque pienso que esta todo mal y quiero que el head-main queden en un punto anterior, entonces puedo usar el reset con una parametrizacion hard con el ID donde quiero ir.
```
git reset --hard (id)
```
Si hago un log luego de este comando va a aparecer como que me borró los ID que vinieron despues el ID que utilice con el hard. Es casi como que me borro las otras fotos, pero la verdad es que no es asi. Con reflog puedo ver toda la historia completa, que muestre incluso lo que hice con el reset --hard
```
git reflog
```
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/dc8d9019774a594a111798174e56083a78f651c5d6b2e40153a0e89ed9c829d9-imagen.png)
Puedo usar el reset --hard para volver a donde estaba inicialmente con el main antes de hacer el primer reset --hard
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/640b025847c8702bd20e690870f9db1aa6c1aff211164f6734aa6c98c8b4aeac-imagen.png)

Uno puede etiquetear commits. Los tags son generalmente las versiones en las app, es una manera mas sencilla de identificarlos y luego puedo usar el git ckeckout para ir a esos puntos especificos del tiempo.
```
git tag clase_1
```
Por ejemplo,
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/0dd73f794bd83c4f0d3d56c339276e98e95a368d0996f32a83554dd79d1d91e7-imagen.png)

## Ramas

Crear una rama en Git

El esquema de git es trabajar por ramas, de manera que podemos crear distintas ramas para trabajar en aspectos particulares, como un subtrabajo. Esto se veria de esta forma
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/c8069499446daae7859155694fc57029825fb9e05592a86a3f68116d72f31294-imagen.png)

Puedo crear una rama nueva
```
git branch login
```
Para cambiar de rama
```
git switch login
```
Por ejemplo, creo la branch login, luego me cambio a la branch login.
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/9992485f07d13b3ec315e6dc223e23e80982e7dae94d3cf3388e2f390b462307-imagen.png)

Modifico alguno de los archivos en esa nueva rama. Lo commiteo y veo que se genero un nuevo commit solo en esa rama. 
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/519b96c85de5507515d3586613c4350f520d2033a3847eb6d94efad99f00a681-imagen.png)
Entonces mi diagrama quedó asi (los ID de los otros commit no son los mios sino del video, pero el ultimo commit en login si es mio como muestra en la imagen anterior).
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/6b9375185aa359b3aba28ab8e1f28351adee6fad70791e014f8582e65b6bdf43-imagen.png)

Si quiero actualizar la rama login en la que estoy trabajando con lo que hizo otro equipo en la rama main.
```
git merge main 
```
La rama se ve asi 
```
 git log --graph --pretty=oneline --oneline
```
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/150b3eafcd22ad352b0d7b4e8dd7d226156afb4db9a64e8c7fdc2ebb540c169e-imagen.png)

Las ramas entonces quedaron de esta forma

![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/cb7128b51665050c1db76f6526469127aa91fc3ea7946a7d3b593e15f9750199-imagen.png)

Concepto de conflicto
Puede haber un conflicto cuando dos equipos en distintas ramas tocan la misma linea de un  archivo. En ese caso, cuando queres hacer el merge, git te va a decir que hay un conflicto porque queres mergear un archivo que tiene la linea que modificaste tambien modificada por el otro equipo. En esos casos, hay que o sacar tu modificacion o decirle que acepte la del otro. Ver ejemplo en el video de Brais Moure

Almacenamiento provisorio

Para hacer un commit temporal, sin que afecte a la rama del proyecto, sino que quede guardado temporalmente en mi local. Esto se usa cuando por ejemplo uno no termino de hacer un determinado codigo pero necesita salir momentaneamente a resolver algo en otra rama. Para evitar commitearlo porque quizas esta a medio hacer (por ejemplo, hay un error y lo estoy buscando), puedo hacerlo con stash. Sino, cuando hago switch o checkout me va a tirar un error el git y no me va a dejar salir porque dice que tengo algo pendiente que no fue commiteado.
```
git stash
```
Si quiero ver lque stash estan pendendientes
```
git stash list
```
Si quiero recuperar el stash
```
git stash pop
```
Si tirar el stash y volver a arrancar desde el utlimo commit
```
git stash drop
```

Reintegracion en el git

Quiero poner lo que desarrolle el login, puedo reponerlo en el main. Puedo hacer un merge de la login desde la rama main.

Con ``` git diff login ``` podemos comprar ramas y nos dice que hay de diferencia.

Con ``` git merge login ```, me lo traigo.

y luego debo guardarlo, asi como esta o con modificaciones, pero es necesario hacer ``` git add . ``` y ``` git commit -m "mensaje"```

Eliminar ramas cuando ya terminamos de desarrollar algo y para evitar que tenga demasiadas ramas, lo que se suele hacer es eliminarla.
```
git branch -d login
```

Para mirar que ramas tengo 
```
git branch 
```

Para mirar el log global (reflog) ahi puedo ver las ramas que "elimine" y me puedo seguir moviendo con ckeckout

## Clase 3: Introduccion de ingreso a GitHub
Git es un sistema de control de version de mi trabajo, es un sistema distribuido. Me sirve para trabajarlo en mi local. 
Por otro lado, GitHub es un servidor en la nube que permite que uno suba y comparta el codigo que va realizando. Esta bueno porque permite tener un back-up de lo que vas haciendo. Si mañana cambio la pc, puedo directamente bajarme los repositorios que tengo en github y no necesito pasarme los datos de una pc a otra con un disco o pendrive. 
Es algo asi como un OneDrive o GoogleDrive, pero especifico para codigo y ademas puedo poner repositorios publicos o privados. Puedo hacer una propia intro, sirve como portafolio para mostrar el trabajo. Combina la utilidad de un repositorio con la de una red social.

El GitHub tiene una página principal, que es el Overview, Repositories, Projects, Packages y Stars (los favoritos). 

Lo primero es generar una linda bio en el Overview que cuente quienes somos, que hacemos, nuestras redes, o links, imagenes, bla bla. 

Para eso vamos a la parte de Repositories y creamos uno nuevo. El nombre del Repositorio tiene que ser nuestro propio nombre de usuario

![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/de715f1598c0d0a62ae68be59180bc91fd69417f0326418d84d14a9f4e8fc223-imagen.png)

Siempre incluir el README y en este caso no incluir ni el gitignore ni la licencia. En este paso tambien se puede definir si el repositorio es publico o privado.
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/97d72e3071a4d974a563302ef8bce45965f1296508b0f82f086dce19f9004c94-imagen.png)

Luego se va a abrir el repositorio que creamos, con el lapicito a la derecha se puede modificar y se puede escribir y formatear utilizando [Markdown.](https://www.markdownguide.org/cheat-sheet/) 

![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/33df1202750f693b7c7fbe29a342dfbae876c4a5b88c5e4ce0f17d05e33c1936-imagen.png)

### Como autenticar mi cuenta con GitHub

Se hace mediante clave SSH. En la documentacion de [github ](https://docs.github.com/es/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)indica como hacerlo. Tambien se puede ver en el video de Brais Moure.

### Repositorio proyecto

Conectarte al remoto del github
```
git remote add origin git@github.com:florfares/aprendiendo-git.git
```
Para pasarlo a remoto
```
git push -u origin main
```
Me aparecen los ficheros en el repositorio que yo le indique mas arriba. Si vos a la parte de commits me dice todo lo que estuve trabajando en mi local, pero eso fijo, no se actualiza automaticamente. 
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/df4635a3dbd1f414d2c70303a60363f342b19ec7ccecc00b559ffd477de71c68-imagen.png)
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/fcdb51bfbfe4c6e396beb103c267ad1a5814fad2d8fe8f85d98a767a26aa28b1-imagen.png)

Como el local ya se sincronizo con el github solo tengo que hacer `git push`

Para descargar el historial de cambios 
```
git fetch
```
Para descargar historial y archivos 
```
git pull
```
Para descargarme un repositorio nuevo completamente, me paro en el path donde quiero descargarla con cd y luego git clone
```
git clone clave-ssh
```
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/67a8a51b7816b75059ac084322cb7706f7d9d96448fab6f1dd8d77bece564591-imagen.png)

Que pasa si no tengo permisos para trabajar en un proyecto? Me lo puedo copiar en mi propio github. Eso se llama hacer un fork (bifurcacion). Copio exactamente lo mismo como un repositorio mio y luego puedo con la clave ssh clonarlo a mi local y trabajar en él ya que es una copia mia, no voy a estar modificando el original.
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/b33196718ae18b9143a0ec2d4dc6176481f4f228b2b54a48a585775a52367e7e-imagen.png)
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/74183ff13467f365a03952a9580c22885fb3142f7c78cf93cac6937974680c50-imagen.png)

Luego si quiero enviarle mi modificacion al usuario que tiene el repo original, le puedo mandar una pull request. 
Una vez que subo el codigo a mi github, en mi repositorio copiado del original debe estar perfectamente sincronizado y presiono en contribute
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/30298a560af26aab5088017c0a3ec41d3ba85d4c5ccccb12e53ed31a0a11d2e3-imagen.png)

![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/1967a65982ad449bb2f1aa2ca72a8a748c51d577eb96ea86378eae9fea33d749-imagen.png)

Al otro usuario le va a parecer la Pull request y me puede aceptar, o contestar.

![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/4875cc278ff71088838ee844c28336c530703d225c95543a6081124d562290f4-imagen.png)

Asi aparecen las opciones 

![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/0054731761c1c92eaa22466edf6e30c7449fdee42c48b3e74fe08f39d3cdd3b5-imagen.png)

En el usuario que pidio el pull request se abre una ventana  de dialogo 

![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/986efa189439e2d2fcfc103c69a588aae6c756c167d2689fae55dbdbd709e330-imagen.png)

El usuario con el repositorio original solo tiene que poner merge pull request si quiere sumarlo a su repositorio y listo.

Sobre manejar conflictos en el github, se puede modificar el fichero desde el github y se indica cual es el conflicto. Uno acepta o modifica, lo commitea y lo mergea.

Sincronizacion de Fork. Se hace desde el github en el extremo derecho como se muestra 
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/5010562f07cf298b22c5ca423ec7740381c7295204286334ebe85fb506c3f691-imagen.png)

## Flujo git-flow

Es un criterio bastante usado que indica un orden y uso de un numero especifico de ramas para trabajar en un proyecto. 

- *Main:* rama principal sobre la que no se trabaja, solo tiene commits de punto especificos de un proyecto. Por ejem, para desarrollo de apps, cada commit en el main es la version de la app (generalmente tiene un tag indicando la version).
* *Develop:* es la rama donde se van haciendo los cambios de la app y en cada momento esta listo el proeycto para lanzarlo a la main.
- *Feature:* ramas que se crean y borran donda se desarrollan pequeños aspectos sobre la app, es donde realmente se trabaja. 
- *Release:* es una rama de transicion entre la develpo y la main.
- *Hotfix:* es una rama que aparece para solucionar un problema puntual y urgente del funcionamiento del proeyecto.

Diagrama
![imagen.png](https://boostnote.io/api/teams/_1wsa1JHU/files/b23f5cf3e91d131e5208c2da5d24c01188e507e1b6146d1dcc7417e8fdb5b07a-imagen.png)

### Git avanzado: modificaciones en git 

Los comandos siguientes deben usarse con mucha cautela

Para traerte una parte de un codigo que hiciste en alguna rama,

```
git cherry-pick ed85685(nombre del commit)
```

Para traerte una rama entera
```
git rebase ed85685
```

### Otras aplicaciones de GitHub

- GitHub pages
- Automatizaciones

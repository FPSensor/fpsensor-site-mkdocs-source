# Guia para Git/Github/Gitlab

esta guia te ayudar  para empezar con git y algunos comandos    
es basica por lo que no debes pretender que ser s un experto despues    
debes tener una cuenta de un sitio con git    
deberias tener instalado git     

## inicializando mi primer repo

nuevo repo    

```
mkdir repo
cd repo
git init
```

## quien sos?

con la informaci"n que diste para crear la cuenta rellena estos comandos:    

```
git config --global user.name
git config --global user.email
```

haciendo nuestro primer cambio

```
git branch -M master
touch hola
echo 1 > hola
git add hola
git commit -m "primer lanzamiento publico de hola"
```

## publicando a nuestro repositorio

en nuestro github debemos crear un repositorio con el nombre que le queramos a$adir    
quiero aclarar que yo utilizo github porque es el mas com#n, pero es lo mismo para todos     

```
git remote add origin https://github.com/FPSensor/hola
git push -f -u origin HEAD:master
```

## primer capitulo completado, algunas cosas a aclarar

1: queremos que seas explicito con los cambios, que se modifico, que archivo, que seccion de la fuente, absolutamente todo, incluso en la descripci"n deberias decir porque hiciste lo que hiciste.
2: no necesitas poner -m en git commit, si no a$ades -m se abrir  el editor, esto es mejor para mensajes de commit largos.
3: ese comando largo de publicaci"n es solo para ramas nuevas, deberia haber otra manera pero si clonas el repositorio de nuevo un "git push" deberia ser suficiente.

## clonar un repositorio

tan simple como "git clone LINK -b master Descargas/hola"    

## quien hizo esto?

agarre un cambio de otra persona, como reconocer su trabajo?    
en la comunidad de android no queremos gente que no a$ade los autores a los cambios y ser s como basura para ellos (lo digo por experiencia)     
debemos a$adir quien hizo esto.    
esto ser  aplicado para el cambio anterior, te ense$a como hacerlo para otros commits mas adelante.    

```
git commit --amend --author="FPSensor <gkartyt@gmail.com>"
```

pero como conseguimos esa informacion?    
en el enlace del commit a$adir .patch al final    
esto literalmente hara que el commit sea un archivo patch, algo de lo que hablaremos despues, pero el punto es:    
lo podemos utilizar para obtener el autor, revisalo    

## i want a cherry

un cherry-pick es literalmente cuando agarras commits de otro repositorio    
para hacerlo es bastante simple    
tenemos que inicializar el repositorio donde esta el commit y sus cambios con sus hash de commits    

```
git remote add cherrypick https://github.com/FPSensor/FPSensor
git fetch cherrypick
git cherry-pick hfwdhuwhfuiwuihfvuiwfhefhruifhfuihiuwe
```

puedes simplemente copiar el hash del commit    
tengo que agarrar 300 commits, como lo hago?    
cosas a tener en cuenta?    
es un commit de inicio y un commit final, todo lo que este despues del commit inicial y antes del commit final sera agregado, no importa que sea     

```
git cherry-pick commit-1~..commit-300
```

oh, no    
tenemos un conflicto de contexto en el archivo hola     

como lo resolvemos?     
un conflicto en git sucede cuando git no sabe que hacer ya que tu fuente y la fuente del otro repositorio antes del commit en cuesti"n son diferentes     
esto es bastante simple     

```
<<<<<<< tu fuente [HEAD]
======= la source de el otro  repositorio mas el commit aplicado[HASH]
>>>>>>> final del conflicto
```

no queremos aplicar un commit porque tiene demasiados conflictos y no tienes ganas de arreglarlos?    

```
git cherry-pick --ship
```

## continuara

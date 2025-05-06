# La guia de compilacion de Android

En esta guia te explica como encontrar los arboles de dispositivos, requerimientos, preparacion del entorno de compilacion y mucho mas.    

!!! abstract "Requisitos"

     - Un procesador decente de 64Bits    
     - Linux corriendo (recomiendo Ubuntu)     
     - 32GB de RAM     
     - 500GB+ HDD (recomiendo SSD)     
     - un buen internet (o al menos uno muy estable durante mucho tiempo)     
     - sentido comun     
     - algo de conocimiento en el manejo de la terminal de linux     

puedes usar especificaci"nes menores? si, estas son las mas recomendadas pero puedes probar otras, puedes por ejemplo utilizar una cantidad enorme de swap o esperar 3 dias para compilar una rom pero con estas especificaciones puedes estar seguro de que no tendras problemas     
otra recomendacion es que si te vas a armar una pc para compiolar siempre busques AMD, la compilacion es un trabajo que exige a todo el CPU en conjunto y un buen procesador multi nucleo hace la diferencia    

!!! tip "Recomendaciones"

     - Haz solo Lineage     
        * para el primer intento te recomiendo que pruebes una rom simple, no pruebes aospa, yaap y roms que no tengan bases seguras     
     - [Aprende git](git.md)     
        * no es necesario para crear la rom pero lo necesitaras cuando quieras hacer cambios y no quieres publicar cambios sin autores y "update x.x" i no quieres que la comunidad te odie     
     - no pidas el puesto de mantenedor     
        * hiciste tu rom? felicidades! pero todavia tienes mucho que aprender antes de ser un mantenedor de una rom, un mantenedor es una persona que puede actualizar la rom constantemente y puede arreglar bugs leyendo registros y haciendo cambios, no quieres que los creadores de roms te pongan en una lista negra     

## Consiguiendo servidor     
si no tienes las especificaciones que nombre recien necesitaras un server    
para eso tenemos algunas opciones      

 - comprar un servidor     
   - ya que ningun venddedor de servidores me promoci"na no te puedo recomendar ninguno pero es realmente facil encontrar un vendedor en telegram. ellos usualmente se manejan con paypal     
 - [Prueba gratuita de Google Cloud Platform](https://cloud.google.com/)     
   - crea una cuenta de google nueva ya que cuando te qedes sin ceditos deberas removerla     
   - necesitaras una tarjeta de credito (no te preocupes, no hay costos en absoluto)     

## consiguiendo los arboles de dispositvos

no tiene sentido sincronizar una rom si no hay arboles de dispositivos para mi dispositivo por lo que el proximo paso sera buscar un arbol de dispositivos    
pero como planeamos conseguirlo?    

 - primer inteto, XDA     
   Yo tengo un Xiaomi Redmi Note 7 [lavender]     
   ahora buscaremos su XDA     
   Redmi Note 7 XDA en google      
   ahora en el XDA     
   vamos a buscar por el tema de ROMs o desarrollo android     
   ahora si hay buscaremos por lineage o una rom basada en la misma     
   entonces buscaremos por las fuentes del kernel (siempre estaran disponibles por GPLv2)     

XDA no tuvo suerte?    
probemos otra cosa     
ve a github.com     
ve al boton de buscar y busca kernel_marca_dispositivo(o _soc ej sdm660)    

si encontraste tus fuentes de kernel entonces continuemos con el proximo paso     
si no tuviste suerte entonces puedes [contactarme](https://t.me/FPSensor) para ver si tenemos suerte, de lo contrario la guia termina aqui para ti     

cuando tengamos el kernel iremos al perfil de github de la persona y buscaremos por:     

 - device_marca_dispositivo     
 - vendor_marca_dispositivo    
 - kernel_marca_dispositivo (tambien puede ser kernel_marca_soc ej: sdm660) (que ya lo tenemos)     
 - device_marca_soc-common (si existe)     
 - vendor_marca_soc-common (si existe)     
   - por los repositorios de vendor si encontraste los arboles de dispositivo y kernel en la organizacion de lineage estaran en la organizacion TheMuppets     
 - hardware_marca (si existe, de lo contrario lo tomaremos de la organizaci"n de LineageOS)     

en algunos casos los repositorios tendran android_ o proprietary_, es lo mismo, no te preocupes     

si logramos encontrar un repo local_manifests muy bien, porque lo podremos usar pronto. guardalo, podria ser importante     

## preparando el entorno
yo te recomiendo Ubuntu (yo uso 20.04 pero otros deberian funci"nar)    

```
sudo apt install bc bison build-essential ccache curl flex g++-multilib gcc-multil>
mkdir ~/bin
PATH=~/bin:$PATH
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo

# crea una cuenta de github y completa el nombre y email
git config --global user.name 
git config --global user.email 
```

## sincronizar la rom

haremos un directorio para la rom    

```
mkdir LineageOS
cd LineageOS
```

iniciaremos la sincronizacion de la rom:    

ESPERA ESPERA ESPERA    
tienes un local_manifests?    
haz esto    

```
git clone LINK .repo/local_manifests
```

ahora vamos a sincronizar la rom     
preparate para un largo tiempo de descarga, ten un buen internet en ese momento     

```
repo init -u https://github.com/LineageOS/android.git -b lineage-XX (replace XX wi>
repo sync -c --no-clone-bundle -j12 --force-sync
```

!!! success

    deberias obtener un mensaje "repo sync succesfully"     

ok entonces, si tenemos local_manifests todo lo que necesitamos ya deberia estar clonado
de lo contrario vamos a mirar en los repositorios que obtuvimos
hare un comando de ejemplo y ustedes repetiran

```
git clone https://github.com/android_device_motorola_rhode device/motorola/rhode -b lineage-21 [la rama debe ser la misma que la de lineage or la versi"n de android]
```

!!! example

    ```
    git clone https://github.com/android_device_xiaomi_lavender device/xiaomi/lavender -b lineage-21
    ```

android_device_xiaomi_lavender     
en la ruta de descarga ponemos esto    
device/xiaomi/lavender     
entonces ignoramos el android_ o proprietary_ y reemplazamos los _ con /      
repetiremos esto con todos los repositorios que encontramos en el paso de la busqueda de los arboles de dispositivos     

## preparar los arboles de dispositivos para la rom

nos moveremos a device/marca/devicename    
si vemos que xx_devicename.mk es lineage_devicename.mk omitiremos los siguientes pasos     
ahora buscaremos el archivo AndroidProducts.mk     
dentro reemplazaremos todos los xx_devicename por lineage_devicename    
guardaremos y nos moveremos a xx_devicename.mk el cual renombraremos como lineage_devicename     
dentro de lineage_devicename.mk editaremos todos l$os xx_devicename por lineage_devicename     
ademas reemplazaremos vendor/xx por vendor/lineage      
ahora en BoardConfig.mk o si tenemos -common nos moveremos al -common/BoardConfigCommon.mk     
dentro verificaremos si hay alguna definicion de vendor/xx y la cambiaremos a vendor/lineage    

## momento de compilar
haremos esto en el directorio principal de la rom:    

```
. build/envsetup.sh
lunch lineage_devicename-userdebug
m bacon
```

!!! success

    si todo va bien tendremos el zip en out/target/product/devicename/    
    ahora prueba y buena suerte    

muchas graciasr    

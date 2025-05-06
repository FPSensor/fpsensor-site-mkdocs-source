# La guia de CRB

En esta guia vamos a mirar dentro de CRB Android Kitchen, sus funciones y como usarla para hacer sorprendentes modificaciones a nuestra ROM/Firmware

## COnsiguiendo la herramienta

Para obtener la herramienta CRB Android Kitchen debes ir a [Este Link](https://xdaforums.com/t/crb-android-kitchen-windows-tool-v3-4-0.3947779/) y siga las instrucciones provistas en el post

Es bueno aclarar que la version gratuita tiene algunas funciones faltantes, en esta guia vamos a hablar sobre todas las funciones pero es bueno que sepas que la version gratuita no tendra: 

 - F2FS     
 - EroFS    
 - Deodexer    
 - Compilar Imagen Super    
 - Compilar Image Bulk    
 - AMLogic extraer/reempaquetar    
 - Magisk patch	    
 - Herramientas de VBMeta	    
 - Administrador de archivos Tar    

## WSL

cuando usemos la app por primera vez nos pedira una instalacion WSL

 - Ve a "Panel De Control"    
 - Desinstalar un programa    
 - Activar o desactivar caracteristicas de Windows    
 - Habilita las siguientes funciones    
    * Hyper-V    
    * plataforma de Maquina Virtual    
    * Subsistema de windows para linux    
 - Esper que se instale y reinicie    
 - Instala el sistema WSL provisto por CRB
 - Reinicia de nuevo    

## Primer proyecto

en el panel izquierdo en el primer boton tendremos opciones para crear o eliminar un proyecto, para empezar a trabajar necesitamos un proyecto, necesitas un proyecto para cada Firmware/ROM que quieras modificar    
debes darle un nombre al proyecto y puedes cambiar entre proyectos con la flecha abajo debajo del CRB de la izquierda    
CRB va a crear una carpeta llamada "Projects" dentro de la ruta del programa, dentro de la carpeta podras ver carpetas con los nombres de los proyectos    
Para eliminar un proyecto solo selecciona el boton "Delete Project" del panel izquierdo primer boton, selecciona el proyecto y el boton de la papelera     

!!! tip

    en el panel izquierdo segundo boton tenemos opciones para entrar a las capetas incluidas en el proyecto

## unpack our firmware

in he left panel first button we will select "Extract ROM (auto)" button, bellow the black rectangle we will see 2 buttons, the first is to select the firmware/ROM file and the seccond is to extract it    
it will give for us inside the project path a folder called "Output" that will have folders with the names of the extracted partitions, inside these folders we will find all the files stored on that unpacked partition    

## Delete partitions

in the left panel first button you will find a option called "Delete partition"    
this option is helpful for cases like GSI where the product partition has no sense to be included and can be deleted to maximize the size of the system partition, to do this go to to the Delete Partition button after extracted the rom and them select the partition and touch the Recycle Bin icon

## Custom Scripts

In the thierd button of the menu with the logo "#!" u can add or modify custom scripts for your personal usage t automatize proccess wen modifying the ROM/Firmware

## APKs edit

in the quarter button with :Android: icon u can modify the APKs with options like

 - Debloater
    * remove apps from the firmware/rom
 - Smali patcher
    * Android framework modifier in simple words
 - deodex
    * Deodexing is basically repackaging of these APKs in a certain way, such that they are reassembled into classes.dex files. By doing that, all pieces of an application package are put together back in one place, thus eliminating the worry of a modified APK conflicting with some separate odexed parts.

## AMLogic

As the name says it unpack or repack the images of device AMLogic, most android TVs

## boot partitions and tools

in the 6th button of left panel u have a lot of options that i will explain bellow:

 - Androidboot editor
    * extract, repack and edit boot, vendor_boot, recovery, vbmeta and dtbo images
 - Android Verified Boot
    * Patch AVB of the partitions listed in the right
 - Patch Boot 
    * With options like Ramdisk editor and fstab patch u can patch boot image such as boot, vendor_boot, etc
 -  Magisk Patch
    * Install Magisk on the selected images
 - AVB/DM-Verity/Forceencrypt
    * Patch VB/DM-Verity/Forceencrypt  with a automated script that disables all verifications
 - Make disabled vbmeta images
    * as the name says its a tool that makes a disabled vbmeta image to disable partitions AVB modifications
 - Force Encryption disabler
    * disables data partition encryption directly from fstab
 - Samsung ROM Disam
    * Debloat system
    * Debloat prism & product
    * Disable SCS service
    * Mod System build.prop
    * Disable FRP
    * Disable Encryption
    * Disable CASS
    * Disable PROCA
    * Disable VAULTKEEPER
    * Disable WSM
    * SafetyNet Fix
    * BT Patchig
    * All-in-One Script
 - Unpack/repack boot

## Build

In the 7th button aka build button u can do the next things

 - Build Image
    * Building partitions as .img files for flashing, u can select the filesystem, type [RAW, Sparse, Sparse Data Image, Sparse Data Image + Brotli and Sparse + LZ4]
 - Build Image Bulk
 - Build Super Image
    * with the options [RAW, Sparse, RAW + LZ$ and Sparse + LZ4] u can build a super partition for dynamic partition devices
 - Tar File Manager
    * U can make or unpack Tar images used by odin

## Settings

the 8th option is the settings button, where u can change the next settings:

 - Open debloater in afloating window: On/Off
 - Exclude Overlay Path in debloater: On/Off
 - Check md5 checksum: On/Off
 - Hide Tool tips on buttons: On/Off
 - Make sparse images without using img2simg: On/Off
 - Keep RAW images after extrract in source folder: On/Off
 - WSL Setup: On/Off

## Last Options

 9th and 10th options are Credits of the App and exit buttons

## End of the guide

!!! abstract "credits"

    - [Elite](https://t.me/EliteUI) helper
    - [daubfy](https://t.me/ItzDaubfy) the guide idea

Thanks for reading and feel free to give feedback in comments

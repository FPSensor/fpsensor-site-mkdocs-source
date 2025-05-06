# The android build guide

on this guide i will explain u how to find device trees, prepare the env, requeriments, and more    

!!! abstract "Reqs"    
     - 64bit decent cpu    
     - 32GB of RAM    
     - 500GB+ space (SSD recommended)    
     - a good internet (or much patienceand a very stable internet)    
     - common sense     
     - a bit of knowledge of linux terminal     

can u use lowest specifications? ye, these ae the most recommended but u can try others. u can by example to use a lot of swap or waiting 3 days to the rom to be compiled but with these specifications u cant be sure that u wont have problems, another recomendation are that if u are going to make a PC to buildalways search AMD, the compilation is a work that uses the whole CPU at the same time and on long periods and for that a good AMD multicore is the best    

!!! tip "recomendations"    
     - do just Lineage    
        * for the first try i recommend u that u try a simple rom, dont try aospa, aosp, etc. do a rom that all of us know that works well    
     - learn git    
        * its not necesary to make the rom but u will need it wen u want to do changes and u dont want to push commits without author and "update x.x" if u dont want the community hates u    
     - dont ask for mainteinership    
        * u did your rom? congrats, but u still have to learn a lot to be a maintainer of a rom, a maintainer is a person that can update the rom constantly and can fix reported bugs reading logs and making changes in trees. u dont want that the creators of the rom to put u in a blacklist    

## getting server

if u dont have the specs mentioned before u will need a server    
for that we have some options    

 - buy a server    
   - since no one of server sellers promote me i wont send u anyone but its really easy to find a server seller in telegram, they usually manages on paypal    
 - [Google Cloud Platform Free triel](https://cloud.google.com/)     
   - make a new google account since wen u have 0 credits u have to delete it    
   - u need a credit card (dw, no costs at all)    

## getting device trees

doesnt makes sense that we sync a rom if there is not device trees for my device so the next step is to look for a device tree    
how we plan to do that?    

 - first try, XDA     
   i have a Xiaomi Redmi Note 7 [lavender]    
   now we will ook for the xda     
   Redmi note 7 XDA    
   now in the xda    
   we will search for the topic roms or android development    
   now if there are we will search for lineage os or based roms    
   then we will search for kernel source (it will be always since its GPLv2 req)    

xda has no luck?    
lets try another    

go to github.com    
go to search button and search kernel_brand_device(or _soc ex ssm660)     

if u found your kernel tree then lets come with the next step    
if u have no luck then can [contact me](https://t.me/FPSensor) to see if we have luck, else the guide ends here for u    

wen we have his kernel we will go to his github profile and look for these:    

 - device_brand_name    
 - vendor_brand_name    
 - kernel_brand_name (it can be kernel_brand_soc ex: sdm660) (that we already have)    
 - device_brand_soc-common (if exist)    
 - vendor_brand_soc-common (if exist)    
   - for vendor repos if u found device and kernel from lineage org then there will be on TheMuppets org probably    
 - hardware_brand (if exist, else we will take it from LineageOS organization)    

in some cases it will have android_ or proprietary_, its the same, dont worry    

if we can find a local_manifests repo very good cuz we can use it, save it cuz will be important    

## preparing the env

i recommend u to use Ubuntu (i use 20.04 but others should work too)

```
sudo apt install bc bison build-essential ccache curl flex g++-multilib gcc-multilib git git-lfs gnupg gperf imagemagick lib32ncurses5-dev lib32readline-dev lib32z1-dev liblz4-tool libncurses5 libncurses5-dev libsdl1.2-dev libssl-dev libwxgtk3.0-gtk3-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev python
mkdir ~/bin
PATH=~/bin:$PATH
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo

# make a github account and fil the name and email
git config --global user.name 
git config --global user.email 
```

## sync the rom

we will make a directory for the rom    

```
mkdir LineageOS
cd LineageOS
```

we will start the rom sync    

BUT WAIT WAIT WAIT    
you got a local_manifests repo?    
do this    

```
git clone LINK .repo/local_manifests
```

now lets sync the rom    
be ready for a long time of downloading, have a good internet in that moment    

```
repo init -u https://github.com/LineageOS/android.git -b lineage-XX (replace XX with lineage version, should be same as tree adroid version)
repo sync -c --no-clone-bundle -j12 --force-sync
```

!!! success

    u should get a message like "Repo sync succesfully"    

ok so if we have local_manifests all things we need are cloned    
else we will take a look on the repos we got    
i will do a command for example and then u guys will reply    

```
git clone https://github.com/android_device_brand_device device/brand/device -b [the branch should be the same as lineage or android version]
```

for example

!!! example

    ```
    git clone https://github.com/1/android_device_xiaomi_lavender device/xiaomi/lavender -b lineage-21
    ```

android_device_xiaomi_lavender    
in the clkone path we do this    
device/xiaomi/lavender    
so we ignore the android_ or the proprietary_ and we replace these _ with /    
done, we have all clonned    
we will do this with all the repos we found in the search of dts    

## prepare device trees for the rom

we will move to device/brand/devicename    
if we see that xx_devicename.mk is linege_devicename.mk we will skip these next steps    
now we will look for AndroidProducts.mk     
we will replace all xx_devicename with lineage_devicename    
save and now we will search for xx_devicename.mk and rename as lineage_devicename.mk    
in lineage_devicename.mk we will edit all xx_devicename with lineage_devicename    
also we will replace vendor/xx with vendor/lineage    
now in BoardConfig.mk or if we have a -common tree will move to the -common/BoardConfigCommon.mk     
on it we will look if there is any vendor/xx definition and will replace with vendor/lineage    
done, we will move back to main folder    

## time to build

we will do this on the main build directory    

```
. build/envsetup.sh
lunch lineage_devicename-userdebug
m bacon
```

!!! success

    if everything goes well we will have the zip on out/target/product/devicename/    
    now test and good luck    

thank you    

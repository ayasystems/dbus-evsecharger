# dbus-open-evse
Integración cargador OpenEvSe en Victron Venus OS
El código original está disponible aquí -> https://github.com/JuWorkshop/dbus-evsecharger
Esta modificación del original permite utilizar las nuevas versiones de firmware (ESP32 4.X)

La minima versión de firmware del ESP32 del openevse es 4.1.x
![image](https://user-images.githubusercontent.com/7864168/192815573-25d378bc-108c-481e-b4b8-eeb2356c2248.png)

## Purpose

Este script lee los valores del Openevse. También permite cambiar el estado del cargador

### Pictures
![Remote Console - Overview](img/1-DeviceList.png) 
![](img/2-EVSE.png)
![](img/3-Device.png)
![](img/4-VRM_Portal.png)
![](img/5-VRM_Devices.png)
![](img/6-VRM_Graph.png)

## Install & Configuration
### Get the code
Simplemente copia el código bajo el directorio  `/data/` por ejemplo `/data/dbus-evsecharger`.
Después ejecuta el instalador install.sh


El siguiente script hará todo por ti:
```
wget https://github.com/ayasystems/dbus-evsecharger/archive/refs/heads/main.zip
unzip main.zip "dbus-evsecharger-main/*" -d /data
mv /data/dbus-evsecharger-main /data/dbus-evsecharger
chmod a+x /data/dbus-evsecharger/install.sh
/data/dbus-evsecharger/install.sh
rm main.zip
```
⚠️ Check configuration after that - because service is already installed an running and with wrong connection data (host) you will spam the log-file

Cambia la configuración del fichero config.ini para ello haremos lo siguiente
```
cd /data/dbus-evsecharger
nano config.ini
```
Una vez cambiados nuestros valores pulsaremos la tecla control y sin soltarla pulsaremos X. Nos preguntará si queremos guardar los cambios y le diremos que sí
Y reiniciaremos el driver para que tome los nuevos valores
```
./restart.sh
```
### Change config.ini
Within the project there is a file `/data/dbus-evsecharger/config.ini` - just change the values - most important is the deviceinstance under "DEFAULT" and host in section "ONPREMISE". More details below:
| Section  | Config vlaue | Explanation |
| ------------- | ------------- | ------------- |
| DEFAULT  | AccessType | Fixed value 'OnPremise' |
| DEFAULT  | SignOfLifeLog  | Time in minutes how often a status is added to the log-file `current.log` with log-level INFO |
| DEFAULT  | Deviceinstance | Unique ID identifying the EvCharger |
| DEFAULT  | position | 0 OUT / 1 IN |
| ONPREMISE  | Host | IP or hostname of on-premise OpenEVSE (note use user password if it is needed |


## Usefull links
Many thanks. @vikt0rm, @fabian-lauer and @trixing project:
- https://github.com/trixing/venus.dbus-twc3
- https://github.com/fabian-lauer/dbus-shelly-3em-smartmeter
- https://github.com/vikt0rm/dbus-goecharger
- https://github.com/JuWorkshop/dbus-evsecharger
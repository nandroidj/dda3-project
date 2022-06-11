# dda3-project

## Estructura

1. Implementacion de nodo embebido

2. Aplicar criterios de ciberseguridad

3. Desarrollo full stack 

4. Repo en Github

5. Presentacion del trabajo: 15 diapos en 15 minutos


### Recomendaciones

1. Vinculacion con su trabajo final

2. Integracion con servicio Cloud


## Infraestructura de Software


[project infrastructure](https://github.com/nandroidj/dda3-project/blob/main/imgs/project-infrastructure.png)



## Instalacion

Se sigue el paso a paso propuesto en la documentacion de [ESP-ESPRESSIF](https://docs.espressif.com/projects/esp-idf/en/v4.4.1/esp32/get-started/index.html#step-2-get-esp-idf) teniendo las siguientes consideraciones para una correcta instalacion en mac os.

1. En el **3er. paso**, previo a correr el comando `./install.sh esp32`, se debe crear el entorno virtual tq la herramiento python-env pueda hacer uso de la misma en la carpeta *.espressif* instalada en la rama *home* del ordenador. Para ello se debe ejecutar la siguiente linea: `python -m venv /home/user/.espressif/python_env/idf4.2_py3.8_env`.

2. Hasta el momento se comentaron las lineas 12 y 13 del archivo `requirements.txt` dentro de la carpeta `esp/esp-idf/` debido a que no reconoce su correcta instalacion. Se ha descargado e instalado por fuera del scope de `esp-idf` sin suerte.

```
ERROR: Could not find a version that satisfies the requirement cryptography>=2.1.4 (from -r /Users/nandroid/esp/esp-idf/requirements.txt (line 12)) (from versions: none)
ERROR: No matching distribution found for cryptography>=2.1.4 (from -r /Users/nandroid/esp/esp-idf/requirements.txt (line 12))
```

La solucion fue instalar la biblioteca cryptography manualmente:

1. Correr el comando `pip install -U pip`.

2. `python -m pip install cryptography`

**IMPORTANTE**: Se setea el alias `alias idf='. $HOME/esp/esp-idf/export.sh'` para utilizar el entorno esp-idf.

## Pruebas

1. Se setea el entorno de esp-idf utilizando el alias `idf`.

2. Se configura el integrado de interes: 

```
idf.py set-target esp32

idf.py menuconfig
```

La configuracion del integrado **esp32** se realiza por unica vez siempre y cuando el proyecto a desarrollar contenga los *builds* y configuracion determinadas. Se recomiendo setear una variable de entorno global tq se omita este paso.


3. Se construye el proyecto `idf.py build`

4. Se busca el puerto serie asignado para el ESP32 segun el comando `ls /dev/cu.*` dando como resultado:

```
/dev/cu.BLTH                    /dev/cu.Bluetooth-Incoming-Port /dev/cu.Venue                   /dev/cu.usbserial-0001
```

5. Se realiza la conexion haciendo `idf.py -p /dev/cu.usbserial-0001 flash`.

Si la conexion falla con mensajes del tipo *A fatal error occurred: Failed to connect to ESP32: No serial data received.* o *A fatal error occurred: Failed to connect to ESP32: Invalid head of packet *, visitar esta pagina, [[SOLVED] Failed to connect to ESP32: Timed out waiting for packet header
](https://randomnerdtutorials.com/solved-failed-to-connect-to-esp32-timed-out-waiting-for-packet-header/). 


6. Se monitorean las tareas que se estan realizando en el kit, `idf.py -p /dev/cu.usbserial-0001 monitor`.


### Links de interes

- https://github.com/espressif/esp-idf/issues/5383

- https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/

- https://github.com/pyca/cryptography/issues/6018

- https://stackoverflow.com/questions/65573853/modulenotfounderror-no-module-named-cryptography

- https://stackoverflow.com/questions/66118337/how-to-get-rid-of-cryptography-build-error























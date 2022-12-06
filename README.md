# Instalacion_y_Ejecucion_de_openhab
En este repositorio se hace la instalación de openhab y se elabora un ejercicios para entender su funcionamiento.



Autor: Victor Zuriel Dominguez Salvador



Recomendaciones para el entendimiento del ejercicio



-Leer la documentación de openhab:


https://www.openhab.org/docs/installation/linux.html



## Instalación de openhab



Se ejecutan lo siuientes comandos de manera ordenada:



-curl -fsSL "https://openhab.jfrog.io/artifactory/api/gpg/key/public" | gpg --dearmor > openhab.gpg



-sudo mkdir /usr/share/keyrings



-sudo mv openhab.gpg /usr/share/keyrings



-sudo chmod u=rw,g=r,o=r /usr/share/keyrings/openhab.gpg




Posteriormente se ejecuta el siguiente comando:



echo 'deb [signed-by=/usr/share/keyrings/openhab.gpg] https://openhab.jfrog.io/artifactory/openhab-linuxpkg stable main' | sudo tee /etc/apt/sources.list.d/openhab.list




Finalmente se actualiza y se intsala:



-sudo apt-get update


-sudo apt-get install openhab



*Nota: La instalación por snap no se recomienda para este tipo de ejercicios porque de ser así es necesario modificar algunos archivos internos*


### Ejercicio:


Se elebora un modelo un canal con su respectivo sensor y ubicación, posteriormente la ubicación que se establezca en este caso el departamento, con el sensor de temperatura tomara lecturas.



Se publica en los siguientes temas: 


mosquito_pub -h localhost -t codigoIoT/openhab/Departamento/Sala/Comedor/DTH11/Temperatura -m 16



#### Evidencias:


Semantic Model


[![Ejercicio-23-de-noviembre-2022.png](https://i.postimg.cc/SKbPZCDH/Ejercicio-23-de-noviembre-2022.png)](https://postimg.cc/DS550JVc)



Locations


[![Ejercicio-2-23-de-noviembre-2022.png](https://i.postimg.cc/6prcpSf1/Ejercicio-2-23-de-noviembre-2022.png)](https://postimg.cc/rDpxhfbS)



Consultado desde el Smartphone.


[![Ejercicio-3-23-de-noviembre-2022.jpg](https://i.postimg.cc/Z55PJR00/Ejercicio-3-23-de-noviembre-2022.jpg)](https://postimg.cc/BXRPgJTG)







### Ejercicio 2



Por medio de openhab logremos mandar una comunicación para la activación de un aire acondicionado (Representado por un LED).



1. Realizar los siguientes dispositivos en OpenHab



   - Sensor de temperatura


   - Sensor de humedad


   - LED


   - Switch


   - Cada uno con su canal de información


   - Agregar un equipamiento con su canal para cada dispositivo



   - Recordar configurar el type del switch y del led con On/Off Switch


   - El switch no lleva state topic, lleva command topic


   - El switch lleva activada la función Is Command


   - Configurar las categorías y propiedades semánticas de acuerdo a cada dispositivo




-----------------------------------------------------------------------------------------------------------------


Sensor de Humedad Thing


Unique ID: SensorHumedadDHT11


Identifier: mqtt:topic:SensorHumedadDHT11


Label: Sensor Humedad DHT11


Location: Comedor


Bridge: MQTT Broker


Channel Identifier: SensorHumedadChannelIdentifier


Label: Sensor Humedad Channel Identifier


Channel Type: Number Value


MQTT State Topic: codigoIoT/openhab/Departamento/Sala/Comedor/DTH11/Humedad 


Absolute minimum: 0


Absolute Maximum: 100


Unit of Measurement: %




Sensor de Humedad Equipamiento


Thing: Sensor Humedad DHT11


Name: SensorHumedadDHT11Equipment


Label: Sensor Humedad DHT11 Equipment


Category: humidity


Semantic Class: Sensor


Channel: Sensor Humedad Channel Identifier


Name: SensorHumedadDHT11Equipment_SensorHumedadChannelIdentifier


Label: Sensor Humedad Channel Identifier


Type: Number


Category: humidity


Semantic class: Measurement


Semantic Property: Humidity



-----------------------------------------------------------------------------------------------------------------




Switch Thing


Unique ID: Switch1


Identifier: mqtt:topic:Switch1


Label: Switch 1


Location: Comedor

Bridge: MQTT Broker


Channel Switch 1


Channel Identifier: Switch1ChannelIdentifier


Label: Switch 1 Channel


Channel Type: On/Off Switch


MQTT Command Topic: codigoIoT/openHab/Departamento/Sala/Escritorio/Switch1


Is Command: On





Switch Equipamiento


Thing: Switch 1


Name: Switch1Equipment


Label: Switch 1 Equipment


Category: Switch


Semantic Class: Equipment


Channel: Switch 1 Channel


Name: Switch1Equipment_Switch1ChannelEquipment


Label: Switch 1 Channel Equipment


Type: Switch


Category: switch


Semantic Class: Switch


Semantic Property: None


-----------------------------------------------------------------------------------------------------------------




Thing LED


Unique ID: LEDSala


Identifier: mqtt:topic:LEDSala


Label: LED Sala


Location: Comedor


Bridge: MQTT Broker



Channel LED


Channel Identifier: LEDSalaChannelIdentifier


Label: LED Sala Channel Identifier


Channel Type: On/Off Switch



MQTT StateTopic: codigoIoT/openhab/Departamento/Sala/Comedor/DTH11/LED01




Equipment



Thing: LED Sala


Name: LEDSalaEquipment


Label: LED Sala Equipment


Category: Light


Semantic Class: Lightbulb


Channel: LED Sala Channel Identifier


Name: LEDSalaEquipment_LEDSalaChannelIdentifier


Label: LED Sala Channel Identifier


Type: Switch


Category: Light


Semantic Class: Switch


Semantic Property: Light



#### Comprobación del funcionamiento

Temperatura:


mosquito_pub -h localhost -t codigoIoT/openhab/Departamento/Sala/Comedor/DTH11/Temperatura -m 16





Humedad:


mosquito_pub -h localhost -t codigoIoT/openhab/Departamento/Sala/Comedor/DTH11/Humedad -m 47



Switch:


En este caso se hace una subcripcion: 


mosquito_sub -h localhost -t codigoIoT/openhab/Departamento/Sala/Comedor/DTH11/Switch




Led01



mosquitto_pub -h localhost -t codigoIoT/openhab/Departamento/Sala/Comedor/DTH11/LED01 -m "ON"


mosquitto_pub -h localhost -t codigoIoT/openhab/Departamento/Sala/Comedor/DTH11/LED01 -m "OFF"





Posteriormente realizaremos la reglas y la programación por bloques. 


### Evidencias:



Activación de Led cuando 


[![Ejercicio-1-25-nov-2022.png](https://i.postimg.cc/rw06k94z/Ejercicio-1-25-nov-2022.png)](https://postimg.cc/Snh1LCDp)



Progrmación por bloques:


[![Ejercicio-2-25-nov-2022.png](https://i.postimg.cc/x8x7rkTK/Ejercicio-2-25-nov-2022.png)](https://postimg.cc/sGWK7gWX)



Locations:


[![Ejercicio-3-25-nov-2022.png](https://i.postimg.cc/v845hDx7/Ejercicio-3-25-nov-2022.png)](https://postimg.cc/F1QfsrZ1)














# Instalacion_y_Ejecucion_de_openhab
En este repositorio se hace la instalación de openhab y se elabora un ejercicio para entender su funcionamiento.



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

















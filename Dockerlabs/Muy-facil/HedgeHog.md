# DockerLabs - HedgeHog
## Resumen 
* **Dificultad:** Muy facil
* **Tiempo:** 
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
| Puerto | Servicio | Version |
|--------|--------|-------|
| 22 | SSH | OpenSSH 9.6p1 |
| 80 | HTTP | httpd 2.4.58 |

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

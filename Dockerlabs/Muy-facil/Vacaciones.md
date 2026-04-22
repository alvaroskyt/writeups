# DockerLabs - Vacaciones
## Resumen
* **Dificultad:** Muy facil
* **Tiempo:** ~30 minutos
* **Fecha:** 22/04/26
## Escaneo de puertos 
Ejecutamos ```nmap``` para ver que puertos estan abiertos.
```bash
nmap -sCV 172.17.0.2
```
| Puerto | Servicio | Version |
|--------|--------|-------|
| 22 | SSH | OpenSSH 7.6p1 |
| 80 | HTTP | httpd 2.4.29 |
## Visualizacion de la web
Entramos por web a la direccion ```http://172.17.0.2```, nada mas entrar no vemos nada pero si inspeccionamos el codigo fuente de la pagina con ```Ctrl + U``` podemos ver el siguiente mensaje.
<img width="577" height="66" alt="image" src="https://github.com/user-attachments/assets/f8653cb8-17de-48c0-aa55-b37c40b23121" />

Esto nos da dos pistas, el usuario puede ser Juan o Camilo.
## Ataque por fuerza bruta a SSH
Con ```hydra``` intentamos sacar la contraseña de alguno de los dos usuarios por fuerza bruta.
```bash
hydra -l camilo -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2
```
Con camilo nos encuentra una contraseña.
<img width="897" height="162" alt="image" src="https://github.com/user-attachments/assets/11e6ba51-a9bd-43c7-8a2d-85bc56e37e23" />

## Acceso por SSH
Como sabemos el usuario y contraseña ya nos podemos conectar por SSH.
```bash
ssh camilo@172.17.0.2
# Password: password1
```
## Escalada de privilegios
Ejecutamos un ```sudo -l```.
<img width="521" height="68" alt="image" src="https://github.com/user-attachments/assets/c03f118a-f792-47e6-9f04-4bcc04fa8575" />

Como se puede ver no tiene permisos para ello.
Si hacemnos un ```cd ..``` podemos ver que hay otros dos usuarios.
<img width="318" height="104" alt="image" src="https://github.com/user-attachments/assets/9836b37d-7928-445d-9078-0576e40d39e6" />

Si nos acordamos del mensaje que ponia en el codigo fuente de la web ponia que nos mando un correo juan, buscamos entre directorios y podemos encontrar dentro de ```/var/mail``` un correo.txt
<img width="717" height="185" alt="image" src="https://github.com/user-attachments/assets/d6bc6303-3e13-4c07-9698-3fb31afd3e99" />

Si le hacemos un ```cat``` el mensaje es el siguiente.
<img width="936" height="84" alt="image" src="https://github.com/user-attachments/assets/b5d6ff52-0bea-4821-8d85-9e6e6854d72f" />

Ahora, podemos acceder al usuario de juan.
```bash
su juan
```



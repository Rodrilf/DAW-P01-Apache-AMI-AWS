# PRÁCTICA 1 - APACHE EN AMI AWS

### PASO 1
Actualizamos e instalamos Apache:

```bash
sudo dnf update -y
sudo dnf install httpd -y
```
![image alt](https://github.com/Rodrilf/DAW-P01-Apache-AMI-AWS/blob/2588b911950d819a2c31e7e8cdc24d307c631903/Capturas/apache_intalacion.png)

### PASO 2
Iniciamos Apache, habilitamos el arranque automático y comprobamos su estado:

```bash
sudo systemctl start httpd
sudo systemctl enable httpd
sudo systemctl status httpd
```

![image alt](https://github.com/Rodrilf/DAW-P01-Apache-AMI-AWS/blob/2588b911950d819a2c31e7e8cdc24d307c631903/Capturas/Iniciado_y_arranque.png)

### PASO 3
Creamos la página web por defecto en:

```bash
sudo nano /var/www/html/index.html
```

Y entramos para editar con el contenido de preferencia, por ejemplo:

![image alt](https://github.com/Rodrilf/DAW-P01-Apache-AMI-AWS/blob/cd687a5b9d93407384cbbaf3fc490a5126c407ee/Capturas/index_html.png)

### PASO 4

Comprobamos el funcionamiento en el navegador:

```
http://IP_PUBLICA
```

![image alt](https://github.com/Rodrilf/DAW-P01-Apache-AMI-AWS/blob/1569fee9fb3734e9ec9a8fb550fc21874110b6dd/Capturas/http_ip_test.png)

### PASO 5

Crear el directorio de la web:

```bash
sudo mkdir -p /var/www/rodri
```

Y creamos la página principal:

```bash
sudo nano /var/www/rodri/index.html
```
Rellenamos con los datos que más nos interesen:

![image alt](https://github.com/Rodrilf/DAW-P01-Apache-AMI-AWS/blob/d4e00505d52bf5d7ab7ff01db82f2967c2e9962f/Capturas/virtual_host.png)

### PASO 6

Creamos el archivo de configuración:

```bash
sudo nano /etc/httpd/conf.d/rodri.conf
```
Y le pasamos los siguientes valores para que funcione correctamente:

![image alt](https://github.com/Rodrilf/DAW-P01-Apache-AMI-AWS/blob/bb31a14f4a1fbe7b7fe66146075a7315b5c0d87a/Capturas/archivo_conf.png)

### PASO 7

En la carpeta de System32 para Windows 11 tenemos que encontrar en **driver/etc** el archivo **hosts** y editarlo con la ip pública de la EC2 y con los nombres de dominio necesarios:

![image alt](https://github.com/Rodrilf/DAW-P01-Apache-AMI-AWS/blob/0d2230b9c5adcd47da2900a19c9733575271a3c4/Capturas/archivo_system32_hosts_editado.png)

Es muy importante que para entrar usemos el bloc de notas abierto como administrador y en la opción de **abrir** entremos a la carpeta y sobreescribamos el archivo de hosts dándole a guardar como, si no, no funciona correctamente.

### PASO 8

Creamos el directorio donde almacenaremos las imágenes públicas y configuramos sus permisos.

```bash
sudo mkdir -p /imagenespublicas/usuarios/usuario1
sudo chmod -R 755 /imagenespublicas
```
### PASO 9

Creamos el archivo .svg (imagen convertida a svg) y pegamos su código XML para generar la imagen.

```bash
sudo nano /imagenespublicas/usuarios/usuario1/nombre_imagen.svg
```

### PASO 10

Modificamos el archivo .conf para poder recoger las imágenes

![image alt](https://github.com/Rodrilf/DAW-P01-Apache-AMI-AWS/blob/143ba0865cca88fab0efe9e60636118aaf76169f/Capturas/archivo_conf_modificado_para_imagenes.png)

### PASO 11

Probamos a acceder a:

```
http://54.226.179.114/imagenes/El_Fary.svg
```

Al estar configurado correctamente nos manda a:

![image alt](https://github.com/Rodrilf/DAW-P01-Apache-AMI-AWS/blob/87960d1d92f2f3edacbabd52d8d7745c3db08af6/Capturas/fary_svg_web.png)

### PASO 12

Vamos a configurar las páginas según el idioma, primero Español:

```bash
sudo nano /var/www/rodri/index.html.es
```

Y editamos el HTML:

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Rodri - Español</title>
</head>
<body>
    <h1>Bienvenido a Rodri.com</h1>
    <p>Esta página está en español.</p>
</body>
</html>
```

Ahora en Inglés:

```bash
sudo nano /var/www/rodri/index.html.en
```

Y editamos de nuevo el HTML:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Rodri - English</title>
</head>
<body>
    <h1>Welcome to Rodri.com</h1>
    <p>This page is in English.</p>
</body>
</html>
```

### PASO 13

Tenemos que editar de nuevo el VirtualHost para que funcione, entramos y lo editamos así:

```
<VirtualHost *:80>

    # DOMINIOS
    ServerName rodri.com
    ServerAlias www.rodri.com rodri.es www.rodri.es

    # DIRECTORIO PRINCIPAL
    DocumentRoot /var/www/rodri

    <Directory /var/www/rodri>
        Options +MultiViews
        Require all granted
    </Directory>

    # IDIOMAS
    DirectoryIndex index.html
    AddLanguage es .es
    AddLanguage en .en

    # IMAGENES PUBLICAS
    Alias /imagenes/ /imagenespublicas/usuarios/usuario1/

    <Directory /imagenespublicas/usuarios/usuario1>
        Options +Indexes
        Require all granted
    </Directory>

    # LOGS INDEPENDIENTES
    ErrorLog /var/log/httpd/rodri_error.log
    CustomLog /var/log/httpd/rodri_access.log combined

</VirtualHost>
```
Importante renombrar el index porque si no, apache enseña esa en vez la de por idioma:

```bash
sudo mv /var/www/rodri/index.html /var/www/rodri/index.html.bak
```

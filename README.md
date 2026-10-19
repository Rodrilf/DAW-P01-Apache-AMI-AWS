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


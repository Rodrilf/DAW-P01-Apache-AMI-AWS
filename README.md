# PRÁCTICA 1 - APACHE EN AMI AWS

#### PASO 1
Actualizamos e instalamos Apache:

```bash
sudo dnf update -y
sudo dnf install httpd -y
```
![image alt](https://github.com/Rodrilf/DAW-P01-Apache-AMI-AWS/blob/2588b911950d819a2c31e7e8cdc24d307c631903/Capturas/apache_intalacion.png)

#### PASO 2
Iniciamos Apache, habilitamos el arranque automático y comprobamos su estado:

```bash
sudo systemctl start httpd
sudo systemctl enable httpd
sudo systemctl status httpd
```

![image alt](https://github.com/Rodrilf/DAW-P01-Apache-AMI-AWS/blob/2588b911950d819a2c31e7e8cdc24d307c631903/Capturas/Iniciado_y_arranque.png)

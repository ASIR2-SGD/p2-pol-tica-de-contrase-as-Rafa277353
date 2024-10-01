# Política de contraseñas

## Contexto
Por defecto, la mayoría de sistemas operativos, vienene con una política de contraseña muy laxa, una contraseña segura presenta una barrera más al atacante, que en su intento de acceder al sistema, indudablemete dejará más rastro y en algunos casos a provocar el abandondo de ataque.

## Objetivos
* Entender el sistema de contraseñas del sistema operativo linux
* Entender el PAM (Plugable authentication Module)
* Instalar y configurar la libreria _pwquality_
* Comprobar y verificar que se ha llevado la práctica de forma correcta
* Documentar la práctica.

## Desarrollo 
### Sistema de contraseñas de Linux
#### Lista de usuarios
/etc/passwd: se guardan los nombres de usuarios, contraseñas, uid, gid y GECOS

#### Contraseñas ocultas y cifradas
/etc/shadow: se guardan los usuarios, contraseñas cifradas y varios campos que administran el veciminto de la contraseña

#### Lista de grupos
/etc/group: se guardan los nombres de grupo, contraseñas(opcional), gid y lista de miembros

### PAM (Plugable authentication Module)
PAM (Pluggable Authentication Module) es un sistema modular de autenticación usado en Linux y Unix. Permite integrar distintos métodos de autenticación sin modificar las aplicaciones. Funciona con módulos que gestionan la autenticación, autorización y sesiones. Los administradores pueden configurar diferentes métodos, como contraseñas o biometría, de manera flexible. Esto facilita la gestión y seguridad del acceso al sistema.


### Configuración del servidor
Instalamos el programa
```bash
sudo apt install libpwquality-tools libpam-pwquality
```
Entramos al archivo de configuración
```bash
sudo nano /etc/security/pwquality.conf
```
Y lo cambiamos
```bash
minlen = 6, 8, 12
dcredit = -1
ucredit = -1
lcredit = -1
ocredit = -1
```
Para asegurarnos de que las configuraciones estén aplicadas
```bash
sudo nano /etc/pam.d/common-password
```
Y debemos contener la siguiente línea
```bash
password requisite pam_pwquality.so retry=3
```

### Comprobación PAM (Plugable authentication Module)
Para comprobar que va el PAM
```bash
sudo passwd vagrant
```
Introducimos una contraseña que no cumpla con los requisitos y debería recharzarla. Cuando introduzcamos una contraseña que cumpla las política, debería aceptarla.
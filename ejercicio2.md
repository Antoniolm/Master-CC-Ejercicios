s## Ejercicios 2 - Antonio David López Machado

### 1-Instalar chef-solo en la máquina virtual que vayamos a usar.

Para realizar la instalación debemos introducir la siguiente linea de comandos

```
curl -L https://www.opscode.com/chef/install.sh | bash
```

Una vez instalado podemos comprobar que se ha instalado correctamente chequeando su versión

![ej1t2](https://user-images.githubusercontent.com/11316534/31940721-6c7d01b8-b8bf-11e7-85c5-4ca5fa5d230d.png)

### 2-Crear una receta para instalar nginx, tu editor favorito y algún directorio y fichero que uses de forma habitual.

Se ha utilizado para dicho ejercicio una maquina virtual de ubuntu 16.04 desde amazon web service.
Creamos la receta default.rb

```
  package 'nginx'
  package 'emacs'
  directory '/home/ubuntu/github'
  directory '/home/ubuntu/github/CC'
  file "/home/ubuntu/github/prueba" do
  	owner "ubuntu"
  	group "ubuntu"
  	mode 00544
  	action :create
  	content "Instalacion de nginx y emacs - Antoniolm"
  end
```

Creamos el directorio que contendra nuestra receta

```
  mkdir -p chef/cookbooks/nginx/recipes
```

Creamos el fichero node.json en el directorio chef:

```
  {
    "run_list":["recipe[nginx]"]
  }
```

Por ultimo creamos el fichero de configuración solo.rb

```
  file_cache_path "/home/ubuntu/chef"
  cookbook_path "/home/ubuntu/chef/cookbooks"
  json_attribs "/home/ubuntu/chef/node.json"
```

Por último lo ejecutamos

```
  sudo chef-solo -c chef/solo.rb
```

Como podemos ver en los resultados la máquina virtual de amazon ya tenia instalado Git por lo que no realiza dicha instalación

![ejer2right](https://user-images.githubusercontent.com/11316534/32222133-5c8afc3c-be38-11e7-8157-2105d4f02926.png)

### 3-Escribir en YAML la siguiente estructura de datos en JSON { uno: "dos", tres: [ 4, 5, "Seis", { siete: 8, nueve: [ 10, 11 ] } ] }

Su traducción a YAML sería

```
---
uno: dos
tres:
- 4
- 5
- Seis
- siete: 8
  nueve:
  - 10
  - 11
```
### 5-Desplegar los fuentes de una aplicación cualquiera, propia o libre, que se encuentre en un servidor git público en la máquina virtual Azure (o una máquina virtual local) usando ansible.

El primer paso a realizar es añadir nuestra maquina virtual a los hosts de ansible ( /etc/ansible/hosts ).

```
[testAnsi]

18.216.7.130 ansible_user=ubuntu
```

Una vez indicada la maquina virtual que provisionaremos comienzo la instalación de los diferentes paquetes para desplegar el proyecto. He tenido que forzar la installacion (parametro -y) ya que sino me pedia verificación y no podía realizar la instalación utilizando ansible.

```
ansible testAnsi -m command -a "sudo apt-get install -y git apache2 mysql-server php libapache2-mod-php php-mcrypt php-mysql"
```

Una vez instalado clonamos el repositorio del proyecto y copiamos el contenido al servidor apache. Para realizar la copia he
cambiado los permisos del usuario "Ubuntu" en esa ruta, ya que no me permitia realizar la clonación por ello.
```
ansible testAnsi -m  git -a "repo=https://github.com/Antoniolm/grado_informatica-PW.git dest=/var/www/html/gitdeploy/ version=HEAD"

```
Como podemos ver en la figura la clonación se ha realizado con exito.

![successclonerepo](https://user-images.githubusercontent.com/11316534/32167322-d76781f8-bd68-11e7-9620-c65ba525243f.png)

### 6-Desplegar la aplicación que se haya usado anteriormente con todos los módulos necesarios usando un playbook de Ansible.

La receta para el despliegue de la aplicación ha sido:
```
---
- hosts: 18.216.7.130
  sudo: yes
  tasks:
  - name: Install package
    apt: name=git state=present
    apt: name=apache2 state=present
    apt: name=mysql-server state=present
    apt: name=php state=present
    apt: name=libapache2-mod-php state=present
    apt: name=php-mcrypt state=present
    apt: name=php-mysql state=present
  - name: Clone project
    git: repo=https://github.com/Antoniolm/grado_informatica-PW.git dest=/var/www/html/gitDeploy/ clone=yes
```
Y como podemos ver en la resultados he podido provisionar correctamente la maquina virtual
![ejer6](https://user-images.githubusercontent.com/11316534/32167293-c6fd9e92-bd68-11e7-9e7e-837a3616dd32.png)

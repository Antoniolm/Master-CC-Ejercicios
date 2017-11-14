## Ejercicios 3 - Antonio David López Machado

### 1- Crear una máquina virtual Ubuntu e instalar en ella un servidor nginx para poder acceder mediante web.

He utilizado el cliente de azure en su versión 2.0 para realizar este ejercicio.
El primer paso ha sido crear la máquina virtual con el comando

```
az vm create -g CCGroupEU -n Ejercicios --image UbuntuLTS
```

Como podemos ver en la imagen se ha podido crear la maquina virtual correctamente.

![creacionazurevm](https://user-images.githubusercontent.com/11316534/32768878-ec7ca6ba-c919-11e7-8b80-ff14f8502587.png)


Una vez creada la máquina virtual nos conectamos por ssh a ella

```
ssh antoniolm@52.157.178.82
```

Ahora realizamos la instalación de nginx con los comandos


```
sudo apt-get update
sudo apt-get install nginx
```

Como podemos observar en la imagen el servidor nginx está activo

![nginxrunning](https://user-images.githubusercontent.com/11316534/32769037-9210b03a-c91a-11e7-8b62-9a1226382db9.png)

Una vez finalizado el ejercicio procedemos a parar la máquina virtual

```
az vm stop -g CCGroupEU -n Ejercicios
```

### 2- Crear una instancia de una máquina virtual Debian y provisionarla usando alguna de las aplicaciones vistas en el tema sobre herramientas de aprovisionamiento

He utilizado el cliente de azure en su versión 2.0 para realizar este ejercicio.
El primer paso ha sido crear la máquina virtual con el comando

```
az vm create -g CCGroupEU -n Ejercicio2 --image Debian
```

Como podemos ver en la imagen se ha podido crear la maquina virtual correctamente.

![debiancreated](https://user-images.githubusercontent.com/11316534/32770254-4044eef6-c91f-11e7-83ee-4a87e4baa3ed.png)

Tras tener lista la máquina a provisionar debemos añadir nuestra máquina virtual a los hosts de ansible ( /etc/ansible/hosts ).

```
[project]

52.233.196.141 ansible_user=antoniolm
```

La receta que se ha utilizado para el provisionamiento ha sido:
```
---
- hosts: 52.233.196.141
  sudo: yes

  tasks:
    ##
    # Actualización del sistema
    ##
    - name: Actualización de repositorios
      apt:
          update_cache: yes
    ##
    # Instalación de paquetes necesarios.
    ##
    - name: Instalación de paquetes requeridos.
      apt: name=git state=present
      apt: name=python3 state=present
      apt: name=python3-pip state=present

    ##
    # Configuración de python3-pip
    ##
    - name: Configuración de python3-pip
      shell: export LC_ALL=C

    ##
    # Instalación de paquetes de pip
    ##
    - name: Instalación de paquetes pip
      shell: pip3 install django djangorestframework pytest boto3
```
Como podemos ver en la imagen hemos podido provisionar correctamente la máquina virtual

![provisiondoneazure](https://user-images.githubusercontent.com/11316534/32770223-23dd2422-c91f-11e7-8582-2673d98f07f7.png)

Una vez finalizado el ejercicio procedemos a parar la máquina virtual

```
az vm stop -g CCGroupEU -n Ejercicio2
```

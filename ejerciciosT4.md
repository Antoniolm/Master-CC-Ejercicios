## Ejercicios Tema 4 - Antonio David López Machado

### 1- Instalar una máquina virtual Debian usando Vagrant y conectar con ella.
```
vagrant box add debian http://www.emken.biz/vagrant-boxes/debsqueeze64.box
```
![Imagen](imgs/debianCreated.png)

Una vez creada debemos initializarla para ello:
```
vagrant init debian
```
![Imagen](imgs/debianInit.png)

Despues levantamos la maquina virtual:
```
vagrant up
```
![Imagen](imgs/debianUp.png)

Y por último conectamos con ella:
```
vagrant ssh
```
![Imagen](imgs/debianSSH.png)

#### 2- Instalar una máquina virtual ArchLinux o FreeBSD para KVM, otro hipervisor libre, usando Vagrant y conectar con ella.
```
vagrant box add ArchlinuxKVM https://vagrant-kvm-boxes.s3.amazonaws.com/archlinux-kvm.box

```

### 3- Crear un script para provisionar de forma básica una máquina virtual para el proyecto que se esté llevando a cabo en la asignatura.

### 4- Configurar tu máquina virtual usando `vagrant` con el provisionador ansible

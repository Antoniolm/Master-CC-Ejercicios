## Ejercicios 3 - Antonio David López Machado

### 1- Crear una máquina virtual Ubuntu e instalar en ella un servidor nginx para poder acceder mediante web.

He utilizado el cliente de azure en su version 2.0 para realizar este ejercicio.
Para ello primero debemos crear la máquina virtual con el comando.

```
az vm create -g CCGroupEU -n Ejercicios --image UbuntuLTS
```

Como podemos ver en se ha podido crear la maquina virtual correctamente.

![creacionazurevm](https://user-images.githubusercontent.com/11316534/32768878-ec7ca6ba-c919-11e7-8b80-ff14f8502587.png)


Una vez creada la maquina virtual nos conectamos por ssh a ella

```
ssh antoniolm@52.157.178.82
```

Ahora realizamos la instalación de nginx con los comandos


```
sudo apt-get update
sudo apt-get install nginx
```

Como podemos observar en la imagen el servidor nginx esta activo

![nginxrunning](https://user-images.githubusercontent.com/11316534/32769037-9210b03a-c91a-11e7-8b62-9a1226382db9.png)

Una vez finalizado el ejercicio procedemos a parar la maquina virtual

```
az vm stop -g CCGroupEU -n Ejercicios
```

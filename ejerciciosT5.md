## Ejercicios Tema 4 - Antonio David López Machado


#### 4- Buscar alguna demo interesante de Docker y ejecutarla localmente, o en su defecto, ejecutar la imagen anterior y ver cómo funciona y los procesos que se llevan a cabo la primera vez que se ejecuta y las siguientes ocasiones.

La imagen seleccionada ha sido : https://hub.docker.com/r/frolvlad/alpine-python3/ la cual es una imagen interesante ya que
su tamaño es muy reducido (~61mb) y tiene instalado tanto python3 como su gestor de paquetes pip3.

Para ejecutarlo primero debemos descargarla para ello:

```
sudo docker pull frolvlad/alpine-python3
```
![Imagen](imgs/T5-1-0.png)

Tras esto podemos ver la imagen descargada con el comando:

```
sudo docker images
```
![Imagen](imgs/T5-1-1.png)

Tras esto, podemos trabajar con python3 a traves del contenedor de una forma sencilla como podemos ver a continuación:
```
sudo docker run --rm frolvlad/alpine-python3 python3 -c 'print("Hello World")'
```
![Imagen](imgs/T5-1-2.png)

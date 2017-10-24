## Ejercicios 2 - Antonio David López Machado

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
  package 'git'
  directory '/home/ubuntu/github'
  directory '/home/ubuntu/github/CC'
  file "/home/ubuntu/github/prueba" do
  	owner "ubuntu"
  	group "ubuntu"
  	mode 00544
  	action :create
  	content "Instalaccion de nginx y github by Antoniolm"
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

![eje2t2](https://user-images.githubusercontent.com/11316534/31940739-789371e4-b8bf-11e7-8645-541f8358cef0.png)

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

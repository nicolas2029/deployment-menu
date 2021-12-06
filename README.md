# deployment-menu

Este proyecto utiliza 3 microservicios para almacenar, editar y mostrar el menu de platillos de un restaura, existirá un usuario que podrá crear, editar y eliminar los platillos del menu, cualquier persona que visite la pagina de inicio podrá ver el menu.

## Microservicios

Todas las imagenes creadas se encuentran en Docker Hub y cuentan con el tag latest y alpine

### menu

Se encarga de mostrar los platillos.

**Repositorios:**

- [https://github.com/nicolas2029/menu](https://github.com/nicolas2029/menu)
- [https://hub.docker.com/r/nicolas2029/get-menu](https://hub.docker.com/r/nicolas2029/get-menu)

### menu-admin

Permite el inicio de sesion del administrador, actualizacion de contraseña, editar, eliminar y crear nuevos platillos.

**Repositorios:**

- [https://github.com/nicolas2029/menu-admin](https://github.com/nicolas2029/menu-admin)
- [https://hub.docker.com/r/nicolas2029/menu-admin](https://hub.docker.com/r/nicolas2029/menu-admin)

### frontend-beerparacreer

Utiliza boostrap, html, js, css y golang para montan un servidor que tenga todo el diseño y UI necesarios para interaccionar con los otros microservicios.

**Repositorios:**

- [https://github.com/nicolas2029/frontend-beerparacreer](https://github.com/nicolas2029/frontend-beerparacreer)
- <https://hub.docker.com/r/nicolas2029/front-beerparacreer>

## Despliegue

### Iniciar Docker

> systemctl start docker

### Iniciar Minikube

> minikube start

### Instalar Istio

Este paso solo se realiza la primera vez que se ejecuta istio sobre el cluster de kubernetes

> istioctl install --set profile=demo -y

> kubectl label namespace default istio-injection=enabled

Para comprobar que todo se ejecuta correctamente podemos ejecutar el siguiente comando:

> kubectl -n istio-system get pods

### Iniciar Software

- Clonar el repositorio
- Agregar los certificados ssh (rsa y rsa.pub) como secretos en kubernetes, se puede hacer esto con el siguiente comando, es necesario especificar la ruta correctamente:

> kubectl create secret generic ssh-key-secret --from-file=ssh-privatekey=$PWD/deployment-menu/certificates/app.rsa --from-file=ssh-publickey=$PWD/deployment-menu/certificates/app.rsa.pub

- Aplicar todos los archivos configmap y secret.

> kubectl apply -f postgres-configmap.yml

> kubectl apply -f postgres-secret.yaml

- Aplicar el archivo postgres.yaml.

> kubectl apply -f postgres.yaml

- Aplicar los archivos yaml restantes.

> kubectl apply -f menu.yaml

> kubectl apply -f menu-admin.yaml

> kubectl apply -f front.yaml

Realizando los pasos anteriores se podra realizar el despliegue de la aplicación web.

### Visualizar dashboard

> istioctl dashboard kiali

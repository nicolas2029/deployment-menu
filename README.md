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


## Despliegue

Para poder utilizar este programa es necesario tener kubernetes.

1. Clonar el repositorio
2. Iniciar la red de nodos de kubernetes.
3. Agregar los certificados ssh (rsa y rsa.pub) como secretos en kubernetes, se puede hacer esto con el siguiente comando: 

> kubectl create secret generic ssh-key-secret --from-file=ssh-privatekey=/root/deployment-menu/certificates/app.rsa --from-file=ssh-publickey=/root/deployment-menu/certificates/app.rsa.pub

4. Aplicar todos los configmap y secret.
5. Aplicar el archivo postgres.yaml.
6. Aplicar los archivos yaml restantes.

Realizando los pasos anteriores se podra realizar el despliegue de la aplicación web.

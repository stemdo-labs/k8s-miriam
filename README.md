# KUBERNETES

>Para la creación del clúster he hecho uso de un [workflow](https://github.com/stemdo-labs/final-project-common-resources/actions/workflows/tf_apply.yml) del siguiente repositorio: [final-project-common-resources](https://github.com/stemdo-labs/final-project-common-resources).

## Aplicativo Laravel

- Con la creación del clúster, el ``Namespace`` llamado ``laravel`` ya está creado, pero se ejecutaría el siguiente comando para crearlo:

    ```bash
    kubectl create namespace <nombre_namespace>
    ```

- Lo siguiente es la creación del archivo `laravel-deployment.yml` y `laravel-service.yml` y se aplican con los siguientes comandos:

    ```bash
    kubectl apply -f laravel-deployment.yml
    ```
    ```bash
    kubectl apply -f laravel-service.yml
    ```

- Para comprobar el estado del pod:
    - Muestra lista de pods levantados:
        ```bash
        kubectl get pods -n <namespace>
        ```
    - Muestra pod en concreto:
        ```bash
        kubectl describe pod <nombre-del-pod> -n <namespace>
        ```

- Para verificar que tiene ``ip externa`` se utliza el siguiente comando:

    ```bash
    kubectl get svc -n <namespace>
    ```

- MySQL es la base de datos elegida para el ejercicio, creamos el archivo `mysql-deployment.yml` y el `mysql-service.yml`. Para la contraseña de la BBDD he creado un secreto en kubernetes llamado `mysql-secret` con el siguiente comando:

    ```bash
    kubectl create secret generic <nombre-secreto> --from-literal=MYSQL_ROOT_PASSWORD=<contraseña> -n <namespace>
    ```

- Añadimos al archivo `laravel-deployment.yml` las credenciales de la BBDD, para ello creamos un secreto llamado `laravel-secret` con el usuario y la contraseña con el siguiente comando: 

    ```bash
    kubectl create secret generic <nombre_secreto> --from-literal=DB_USERNAME=<usuario> --from-literal=DB_PASSWORD=<contraseña> -n <namespace>
    ```

- Para comprobar que todo va correctamente necesitamos hacer un port forwarding para redirigir el puerto local a el del pod y poder acceder desde el navegador:

    ```bash
    kubectl port-forward pod/<nombre_pod> <puerto_pod>:<puerto_local> -n <namespace>
    ```

![alt text](images/portforward-laravel.png)

![alt text](images/laravel.png)

## Aplicativo phpMyAdmin

- Con la creación del clúster, el ``Namespace`` llamado ``phpmyadmin`` ya está creado, pero se ejecutaría el siguiente comando para crearlo:

    ```bash
    kubectl create namespace <nombre_namespace>
    ```

- Lo siguiente es la creación de los archivos `phpmyadmin-deployment.yml` y `phpmyadmin-service.yml` y se aplican con los siguientes comandos:

    ```bash
    kubectl apply -f phpmyadmin-deployment.yml
    ```
    ```bash
    kubectl apply -f phpmyadmin-service.yml
    ```

- También se van a hacer uso del archivo `mysql-service.yml`. Como este pertenece al namespace de `laravel` se utiliza de la siguiente manera:
    ```
    <nombre-archivo>.<namespace>
    mysql-service.laravel
    ```

- Para que no pida autenticación, creamos de nuevo los secretos anteriores para se que conecte automáticamente a la base de datos, ya que no se pueden utilizar los mismos porque pertenecen a distintos `namespaces` y se encuentran aislados.

- Por último, hacemos `port-forward` para poder acceder desde el navegador a la base de datos:

![alt text](images/portforward-phpmyadmin.png)

![alt text](images/phpmyadmin.png)
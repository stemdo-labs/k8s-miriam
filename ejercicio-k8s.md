# Ejercicio Semanal

## ¡Importante!

Ten mucho cuidado con los valores sensibles que puedas exponer en tus soluciones. Recuerda que otras personas pueden ver la información de tus entregables y, por lo tanto, acceder a este tipo de información. ¡Siempre trata de mantener la seguridad de tus datos y de los datos de tus clientes!


## Enunciado

Se desea desplegar en nuestro cluster lo siguiente:

- Un aplicativo `laravel` con los siguientes requisitos:
    - Todos los elementos deben desplegarse en un namespace con el nombre `laravel`.
    - Se usará la imagen de  bitnami/laravel en la versión mas reciente a la entrega de este ejercicio.
    - Se usará una BBDD compatible (libre elección) con nuestro Laravel usando la imagen **``oficial``** de la BBDD que elijas.
    - Se debe desplegar todo elemento kubernetes necesario para que Laravel pueda conectarse a la BBDD y nosotros podamos acceder a laravel desde un navegador.

- Un aplicativo `phpmyadmin` con los siguientes requisitos:
    - Todos los elementos deben desplegarse en un namespace con el nombre `phpmyadmin`.
    - Se usará la imagen **``oficial``** de phpmyadmin.
    - Se debe desplegar todo elemento kubernetes necesario para que phpmyadmin pueda conectarse a la BBDD y nosotros podamos acceder a phpmyadmin desde un navegador.
    - phpmyadmin debe ser accesible sin requerir autenticación (con fines de desarrollo).


Todo este despligue debe consumir como máximo, el 60% de los recursos de CPU y GPU de nuestro cluster.

## Nota

Como aún no se ha tratado, no nos preocuparemos por la persistencia de los datos.
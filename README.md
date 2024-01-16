# Instalación y Manejo de Odoo

Para instalar Odoo con el uso de Docker, se debe tener instalado Docker y Docker Compose.

## 1. Estructura del Docker Compose:

```yml
version: '3.1'

services:
  #servicio de la aplicacion
  dam_odoo:
    image: odoo:16.0
    #servicio de base de datos que utiliza la plicacion
    #esta aplicacion depende de este servicio
    #no arrancará hasta que el servicio este levantado
    depends_on:
      - dam_postgresOdoo
    #mapeo de puertos para acceder a la aplicacion en mi maquina
    ports:
      - 8069:8069
    #variables de entorno para la aplicacion
    environment:
      #nombre o la IP del gestor de base de datos
      - HOST=dam_postgresOdoo
      # usuario (administrador del gestor de la base de datos)
      - USER=castelao
      # contraseña del ADMIN (superusuario) del gestor de base de datos
      - PASSWORD=castelao

  #servicio gestor de base de datos
  dam_postgresOdoo:
    #imagen utilizada y su version
    image: postgres:15
    #mapeo de puertos para acceder a las bases de datos desde el IDE
    ports:
      - 5432:5432
    #variables de entorno de la imagen postgres 15
    environment:
      #nombre de la base de datos predeterminada
      - POSTGRES_DB=postgres
      #contraseña del administrador
      - POSTGRES_PASSWORD=castelao
      #usuario administrador
      - POSTGRES_USER=castelao
```

Como se puede observar, se está utilizando la imagen de Odoo 16.0, la cual se encuentra en Docker Hub. Además, se está utilizando una base de datos de Postgres, la cual se encuentra en el mismo Docker Compose.

## 2. Integración de PostgreSQL con nuestro IDE:

> [!NOTE]
> Previo a la integración, es necesario que nuestro contenedor este levantado. Para ello empleamos nuestro comando:
> *docker compose up -d*

En el apartado superior derecho de nuestro IDE, encontraqmos la opción de "Database". En este encontramos el signo +, el cual nos permite añadir una nueva conexión.

![img_1.png](media%2Fimg_1.png)

Una vez dentro, debemos rellenar los campos con los datos de nuestro contenedor de PostgreSQL.




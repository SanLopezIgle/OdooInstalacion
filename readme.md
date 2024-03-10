# Odoo Instalación

## Configuración de Docker Compose

El archivo `docker-compose.yml` contiene la configuración de los servicios de PostgreSQL y Odoo.

### Servicios

```
version: '3'
services:
  db:
    image: postgres:latest
    environment:
      POSTGRES_DB: postgres
      POSTGRES_USER: odoo
      POSTGRES_PASSWORD: odoo
    ports:
      - "5432:5432"
    volumes:
      - db_data:/var/lib/postgresql/data

  odoo:
    image: odoo:latest
    depends_on:
      - db
    ports:
      - "8069:8069"
    volumes:
      - ./addons:/mnt/extra-addons


```

### Volumes

```
volumes:
  db_data:
  odoo_data:
```

## Ejecución de los Contenedores


```
docker-compose up -d
```

Esto iniciará los servicios de PostgreSQL y Odoo en segundo plano.

## Enlace de PyCharm con Docker y PostgreSQL

Para enlazar PyCharm con Docker y la base de datos PostgreSQL, sigue los siguientes pasos:

1. **Instala el plugin de Docker en PyCharm.**
2. Abre PyCharm y ve a Configuración de Ejecución (Run/Debug Configurations).
3. Configura una nueva ejecución de Docker para tu proyecto.
4. Configura una nueva conexión a la base de datos PostgreSQL dentro de PyCharm utilizando las credenciales definidas en el archivo `docker-compose.yml`.

## ¿Qué hacer si el puerto 5432 está ocupado?

Si el puerto `5432` está ocupado en tu ordenador local, puedes solucionarlo modificando el mapeo de puertos en el archivo `docker-compose.yml`. Cambia el puerto del servicio PostgreSQL en el host a uno disponible en tu máquina.

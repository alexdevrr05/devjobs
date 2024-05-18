# Aplicación para la búsqueda de empleo construida con Laravel y Docker (sail)

Comando para no tener que escribir el path del binario sail (esta linea se coloca en el bash o zsh, depende qué usemos):

alias sail='[ -f sail ] && bash sail || bash vendor/bin/sail'

### Pasos a seguir para su instalación

Clonar el repositorio

```bash
git clone https://github.com/alexdevrr05/devjobs.git
```

Ingresar a la carpeta del proyecto

```bash
cd project-name
```

Copiar el archivo de las variables de entorno de ejemplo

```bash
cp .env.example .env
```

Configurar las variables de entorno en el archivo `.env`
Aseguramos de que las siguientes variables estén correctamente configuradas:

```
APP_NAME=Laravel
APP_ENV=local
APP_KEY=base64:generated_key_here
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=nombre_base_de_datos
DB_USERNAME=usuario
DB_PASSWORD=password
```

Para ejecutar el proyecto `sail up`
Para no tener el error común de los puertos en uso, agregamos la siguiente linea de código en el archivo `.env`:

```
FORWARD_DB_PORT=3307
```

A su vez, la tenemos que cambiar en el archivo `docker-compose.yaml`:

```bash
'${FORWARD_DB_PORT:-3307}:3306'
```

Una vez levantado el proyecto, con los contenedores de Docker corriendo, haremos la conexión a nuestra base de datos.

Ingresamos las credenciales de las variables del archivo `.env`

```
DB_PORT
DB_DATABASE
DB_USERNAME
DB_PASSWORD
```

Y hacemos el test de conexión en el gestor de base de datos que estemos utilizando. (En mi caso "TablePlus")

## Si el test de conexión falla y nos muestra un mensaje de error del tipo:

```bash
Access denied for user 'sail'@'%' to database 'devjobs'
```

Entonces no hicimos bien la configuración, verificamos uno de los pasos anteriores que tiene que ver con el archivo `docker-compose.yaml` y el puerto

### O creamos nosotros mismos la DB y los permisos del usuario (Opción no recomendada):

Entramos al MySQL del contenedor

```bash
sail exec mysql bash
```

Dentro, coloamos el comando

```bash
mysql -u root -p
```

_Digitamos la password_

Y asignamos todos los permisos al usuario en la base de datos:

```
GRANT ALL PRIVILEGES ON devjobs.\* TO 'sail'@'%';
FLUSH PRIVILEGES;
```

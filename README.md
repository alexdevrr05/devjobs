# Aplicación para la búsqueda de empleo construida con Laravel y Docker (sail)

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

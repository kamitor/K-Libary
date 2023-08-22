---
quickshare-date: 2023-04-12 14:02:28
quickshare-url: "https://noteshare.space/note/clgdn6ae5344901pj27wqnbj0#8V9spJrhXKfrBSw1+TdRNIIW46d+2ZDXJ63Ci5dCSBc"
---
```

```


[[Ruitenberg Proposal]]
[[Chris Stack]]

PLACEHOLDER

Step 1: 1.  First, install Docker and Docker Compose on the server with the following commands:

```
sudo apt-get update
sudo apt-get install -y docker docker-compose
```

Step 2: 2.  Create a new directory to store the Docker configuration files:

```
sudo mkdir /opt/warehouse
cd /opt/warehouse
```

Step 3: 3.  Create a new file named `.env` in the directory with the following contents:

```
POSTGRES_PASSWORD=RuitenbergLinux100!
RABBITMQ_DEFAULT_USER=admin
RABBITMQ_DEFAULT_PASS=RuitenbergLinux100!
REDIS_PASSWORD=RuitenbergLinux100!
SECRET_KEY=RuitenbergLinux100!

```



Step 4: 4.  Create a new file named `docker-compose.yml` in the same directory with the following contents:
```

version: '3'

services:
  nginx:
    image: nginx:latest
    container_name: nginx
    restart: always
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf
      - ./nginx/ssl:/etc/nginx/ssl
      - ./wagtail:/var/www/wagtail
      - ./logs/nginx:/var/log/nginx

  wagtail:
    build:
      context: ./wagtail
      dockerfile: Dockerfile
    container_name: wagtail
    depends_on:
      - db
    restart: always
    volumes:
      - ./wagtail:/var/www/wagtail
      - ./wagtail/media:/var/www/wagtail/media
    environment:
      - SECRET_KEY=RuitenbergLinux100!
      - DEBUG=False
      - ALLOWED_HOSTS=tonomy.nl
    ports:
      - "8000:8000"

  db:
    image: postgres:latest
    container_name: wagtail-db
    restart: always
    environment:
      - POSTGRES_USER=root
      - POSTGRES_PASSWORD=RuitenbergLinux100!
      - POSTGRES_DB=wagtail
    volumes:
      - ./postgres-data:/var/lib/postgresql/data

  rabbitmq:
    image: rabbitmq:management-alpine
    container_name: rabbitmq
    restart: always
    ports:
      - "15672:15672"
      - "5672:5672"
    environment:
      - RABBITMQ_DEFAULT_USER=root
      - RABBITMQ_DEFAULT_PASS=RuitenbergLinux100!

  nextcloud:
    image: nextcloud:fpm-alpine
    container_name: nextcloud
    restart: always
    depends_on:
      - db
    volumes:
      - ./nextcloud:/var/www/html
      - ./nextcloud-data:/var/www/html/data
      - ./nextcloud-config:/var/www/html/config
      - ./nextcloud-apps:/var/www/html/custom_apps
      - ./nextcloud-logs:/var/log/nginx
    environment:
      - MYSQL_HOST=db
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=root
      - MYSQL_PASSWORD=RuitenbergLinux100!
      - NEXTCLOUD_ADMIN_USER=admin
      - NEXTCLOUD_ADMIN_PASSWORD=RuitenbergLinux100!
    ports:
      - "8080:80"

```


Create a directory named `wagtail` and navigate into it:

```
mkdir wagtail
cd wagtail


```

Create a new file named `Dockerfile` with the following content: 


```
# Base image
FROM python:3.8-slim-buster

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Set the working directory
WORKDIR /wagtail

# Copy the requirements file
COPY requirements.txt /wagtail

# Install the required packages
RUN pip install --no-cache-dir -r requirements.txt

# Copy the project files
COPY . /wagtail

# Expose the port
EXPOSE 8000

# Run the command
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]


```

This Dockerfile specifies the Python version, sets some environment variables, sets the working directory, installs the required packages, and exposes the port used by the Wagtail server.

Create a new file named `docker-compose.yml` with the following content:


```
version: "3"

services:
  wagtail:
    build: .
    container_name: wagtail
    restart: always
    ports:
      - "8000:8000"
    depends_on:
      - db
      - redis
    environment:
      - SECRET_KEY=RuitenbergLinux100!
      - DEBUG=1
      - ALLOWED_HOSTS=.tonomy.nl
      - DATABASE_URL=postgres://postgres:Password123!!!@db:5432/wagtail
      - REDIS_URL=redis://redis:6379/0

  db:
    image: postgres:13-alpine
    container_name: wagtail-db
    restart: always
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=Password123!!!
      - POSTGRES_DB=wagtail

  redis:
    image: redis:6-alpine
    container_name: wagtail-redis
    restart: always
    ports:
      - "6379:6379"

```

This docker-compose file specifies the version, defines three services (wagtail, db, and redis), sets the build context for the wagtail service, sets some environment variables for the wagtail service, specifies the database and Redis URL, and exposes the Redis port.

Build and start the containers:

```
docker-compose up -d

```

This command builds the containers and starts them in the background.

Check the container status:

```
docker ps

```

This command should list the three containers that were created

Create superuser for Wagtail

```
docker exec -it wagtail python manage.py createsuperuser

```

5.    
    This command creates a superuser account that can be used to log in to the Wagtail admin interface.

## nginx Reverse proxy 

1.  Configure NGINX as a reverse proxy:
sudo apt-get update
sudo apt-get install nginx


## 12  Grafana

Create a new file named `wagtail.conf` in the `/etc/nginx/sites-available/` directory with the following content:

1.  Create a `grafana` directory in the project folder
2.  Create a `Dockerfile` in the `grafana` directory with the following content:

```
FROM grafana/grafana:latest

USER root

# Install required packages
RUN apt-get update && \
    apt-get install -y \
        curl \
        gnupg \
        libfontconfig1

# Install plugins
RUN grafana-cli plugins install grafana-piechart-panel && \
    grafana-cli plugins install grafana-worldmap-panel && \
    grafana-cli plugins install briangann-gauge-panel && \
    grafana-cli plugins install grafana-clock-panel && \
    grafana-cli plugins install vonage-status-panel && \
    grafana-cli plugins install yesoreyeram-boomtable-panel && \
    grafana-cli plugins install natel-discrete-panel && \
    grafana-cli plugins install neocat-cal-heatmap-panel && \
    grafana-cli plugins install michaeldmoore-multistat-panel && \
    grafana-cli plugins install btplc-trend-box-panel && \
    grafana-cli plugins install ryantxu-ajax-panel && \
    grafana-cli plugins install simpod-json-datasource

# Expose ports
EXPOSE 3000

# Start Grafana
CMD [ "/usr/sbin/grafana-server", "--config=/etc/grafana/grafana.ini", "--homepath=/usr/share/grafana", "cfg:default.paths.data=/var/lib/grafana", "cfg:default.paths.logs=/var/log/grafana", "cfg:default.paths.plugins=/var/lib/grafana/plugins" ]


```

Build Grafana 
`` docker build -t openwarehouse/grafana -f Dockerfile.grafana .


Create a new `docker-compose.yml` file in the root directory with the following content:

```

version: '3'

services:
  rabbitmq:
    image: rabbitmq:3-management
    ports:
      - "5672:5672"
      - "15672:15672"
    environment:
      RABBITMQ_DEFAULT_USER: "root"
      RABBITMQ_DEFAULT_PASS: "RuitenbergLinux100!"

  postgres:
    image: postgres:12-alpine
    ports:
      - "5432:5432"
    environment:
      POSTGRES_USER: "root"
      POSTGRES_PASSWORD: "RuitenbergLinux100!"
      POSTGRES_DB: "openwarehouse"
    volumes:
      - postgres_data:/var/lib/postgresql/data

  redis:
    image: redis:latest
    ports:
      - "6379:6379"
    command: redis-server --requirepass RuitenbergLinux100!

  nextcloud:
    image: nextcloud:fpm-alpine
    ports:
      - "8080:80"
    environment:
      POSTGRES_HOST: "postgres"
      POSTGRES_USER: "root"
      POSTGRES_PASSWORD: "RuitenbergLinux100!"
      POSTGRES_DB: "nextcloud"
      REDIS_HOST: "redis"
      REDIS_PASSWORD: "RuitenbergLinux100!"
      NEXTCLOUD_ADMIN_USER: "admin"
      NEXTCLOUD_ADMIN_PASSWORD: "RuitenbergLinux100!"
      NEXTCLOUD_TRUSTED_DOMAINS: "Ruitenberg.tonomy.nl

```


## Wagtaill Web Provider

Setting up Wagtail as the website provider: a. Create a new directory called `wagtail` and navigate into it. b. Create a new file called `Dockerfile` and add the following code:


```
# Base image
FROM python:3.9-slim

# Set working directory
WORKDIR /app

# Copy requirements.txt and install dependencies
COPY requirements.txt .
RUN pip install -r requirements.txt

# Copy the rest of the application code
COPY . .

# Expose port 8000
EXPOSE 8000

# Set environment variables
ENV DJANGO_SETTINGS_MODULE=mysite.settings.production
ENV SECRET_KEY=RuitenbergLinux100!
ENV DEBUG=False
ENV ALLOWED_HOSTS=tonomy.nl

# Collect static files
RUN python manage.py collectstatic --noinput

# Start the web server
CMD gunicorn mysite.wsgi:application --bind 0.0.0.0:8000

```


c. Create a new file called `requirements.txt` and add the following code: `wagtail` d. Create a new directory called `mysite` and navigate into it. e. Run the following command to start a new Wagtail project: `wagtail start mysite .` f. Edit the `settings/production.py` file and modify the `ALLOWED_HOSTS` setting to include `tonomy.nl`: `ALLOWED_HOSTS = ['tonomy.nl']` g. Edit the `mysite/wsgi.py` file and modify the `application` variable to use the production settings: `os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'mysite.settings.production')` h. Build and run the Wagtail container with the following commands: `docker build -t wagtail . docker run -d --name wagtail -p 8000:8000 wagtail` i. Navigate to `https://tonomy.nl:8000` to access the Wagtail website.
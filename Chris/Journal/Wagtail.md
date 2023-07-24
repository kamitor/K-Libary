[[2023-04-09 To Do]]
[[Chris Stack]]
[[wagtail setup]]

sudo apt update -y
sudo apt install -y software-properties-common
sudo apt install -y build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev wget
sudo add-apt-repository ppa:deadsnakes/ppa -y
sudo apt install -y python3.10 


sudo apt install -y python3-pip
sudo apt install -y build-essential libssl-dev libffi-dev python3-dev
sudo apt install -y python3-venv
mkdir environments
cd environments
python3 -m venv my_env

python -m venv mysite/env
source mysite/env/bin/activate
pip install wagtail
wagtail start mysite mysitewagtail

cd mysite
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver


## DOcker

shh root@209.38.244.17
sudo apt update -y && sudo apt-get upgrade -y

python3 -m venv venv  
source venv/bin/activate
pip install --upgrade pip  
pip install pipenv

sudo apt install -y software-properties-common
sudo apt install -y build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev wget apt-utils
sudo apt install -y python3-pip
sudo apt install -y build-essential libssl-dev libffi-dev python3-dev
sudo apt install -y python3-venv
sudo apt install -y docker docker-compose

pip install wagtail
wagtail start mysite
cd mysite
docker build -t mysite .
docker run -p 8000:8000 mysite

Source: https://medium.com/@Gidsey/hosting-a-wagtail-site-on-digital-ocean-with-caprover-e71306e8d053
mkdir mysite
python3 -m venv venv  
source venv/bin/activate

pipenv install wagtail==3.0.1 django-environ==0.9.0   
wagtail start base mysite



# GPT

sudo apt update -y
sudo apt upgrade


docker pull wagtail/wagtail:latest


````
``
```
#!/bin/bash

# Prompt user for domain name
echo "Enter the domain name (without https://):"
read domain

# Prompt user for Docker Hub credentials
echo "Enter your Docker Hub username:"
read docker_user
echo "Enter your Docker Hub password:"
read -s docker_password

# Create Docker network
docker network create wagtail

# Start PostgreSQL container
docker run -d \
    --name wagtail-db \
    --restart always \
    --network wagtail \
    -e POSTGRES_USER=wagtail \
    -e POSTGRES_PASSWORD=wagtail \
    -e POSTGRES_DB=wagtail \
    postgres:13

# Start Redis container
docker run -d \
    --name wagtail-redis \
    --restart always \
    --network wagtail \
    redis:6

# Start Certbot container to obtain SSL certificate
docker run -it --rm \
    --name certbot \
    --network wagtail \
    -v "/etc/letsencrypt:/etc/letsencrypt" \
    -v "/var/lib/letsencrypt:/var/lib/letsencrypt" \
    certbot/certbot certonly \
    --non-interactive \
    --agree-tos \
    --email webmaster@$domain \
    --standalone \
    -d $domain

# Start Nginx container with SSL configuration
docker run -d \
    --name wagtail-nginx \
    --restart always \
    --network wagtail \
    -p 80:80 \
    -p 443:443 \
    -v "$(pwd)/wagtail-nginx.conf:/etc/nginx/conf.d/default.conf:ro" \
    -v "/etc/letsencrypt:/etc/letsencrypt:ro" \
    nginx:stable-alpine

# Start Wagtail container with environment variables
docker run -d \
    --name wagtail \
    --restart always \
    --network wagtail \
    -v "$(pwd)/wagtail:/app" \
    -e DJANGO_SETTINGS_MODULE=wagtail.settings.production \
    -e DATABASE_URL=postgres://wagtail:wagtail@wagtail-db/wagtail \
    -e REDIS_URL=redis://wagtail-redis:6379/0 \
    -e SECRET_KEY=$(openssl rand -base64 32) \
    -e ALLOWED_HOSTS=$domain \
    -e DOCKER_USERNAME=$docker_user \
    -e DOCKER_PASSWORD=$docker_password \
    -e DOCKER_REGISTRY=docker.io \
    -e DOCKER_REPOSITORY=$docker_user/wagtail \
    -p 8000:8000 \
    wagtail:latest

```
`` 
``
``



```

#!/bin/bash

# Prompt user for domain name
echo "Enter the domain name (without https://):"
read domain

# Prompt user for Docker Hub credentials
echo "Enter your Docker Hub username:"
read docker_user
echo "Enter your Docker Hub password:"
read -s docker_password

# Create Docker network
docker network create wagtail

# Start PostgreSQL container
docker run -d \
    --name wagtail-db \
    --restart always \
    --network wagtail \
    -e POSTGRES_USER=wagtail \
    -e POSTGRES_PASSWORD=wagtail \
    -e POSTGRES_DB=wagtail \
    postgres:13

# Start Redis container
docker run -d \
    --name wagtail-redis \
    --restart always \
    --network wagtail \
    redis:6

# Start Certbot container to obtain SSL certificate
docker run -it --rm \
    --name certbot \
    --network wagtail \
    -v "/etc/letsencrypt:/etc/letsencrypt" \
    -v "/var/lib/letsencrypt:/var/lib/letsencrypt" \
    certbot/certbot certonly \
    --non-interactive \
    --agree-tos \
    --email webmaster@$domain \
    --standalone \
    -d $domain

# Start Nginx container with SSL configuration
docker run -d \
    --name wagtail-nginx \
    --restart always \
    --network wagtail \
    -p 80:80 \
    -p 443:443 \
    -v "$(pwd)/wagtail-nginx.conf:/etc/nginx/conf.d/default.conf:ro" \
    -v "/etc/letsencrypt:/etc/letsencrypt:ro" \
    nginx:stable-alpine

# Start Wagtail container with environment variables
docker run -d \
    --name wagtail \
    --restart always \
    --network wagtail \
    -v "$(pwd)/wagtail:/app" \
    -e DJANGO_SETTINGS_MODULE=wagtail.settings.production \
    -e DATABASE_URL=postgres://wagtail:wagtail@wagtail-db/wagtail \
    -e REDIS_URL=redis://wagtail-redis:6379/0 \
    -e SECRET_KEY=$(openssl rand -base64 32) \
    -e ALLOWED_HOSTS=$domain \
    -e DOCKER_USERNAME=$docker_user \
    -e DOCKER_PASSWORD=$docker_password \
    -e DOCKER_REGISTRY=docker.io \
    -e DOCKER_REPOSITORY=$docker_user/wagtail \
    -p 8000:8000 \
    wagtail:latest

```
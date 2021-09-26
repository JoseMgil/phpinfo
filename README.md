# phpinfo

DOWNLOAD GITHUB REPOSITORY
```
git clone https://github.com/academiaonline/phpinfo
cd phpinfo
git checkout main
```
## TRADITIONAL DEPLOYMENT (WITHOUT CONTAINERS)
RUN THE APPLICATION WITHOUT CONTAINERIZATION (AFTER INSTALLING PHP IN YOUR SYSTEM)
```
php -f src/index.php -S 0.0.0.0:8080
```
TEST THE RUNNING APPLICATION (AFTER INSTALLING CURL IN YOUR SYSTEM)
```
curl localhost:8080/src/index.php
```
## MODERN DEPLOYMENT (WITH CONTAINERS)
CHECKOUT THE BRANCH WITH THE CONTAINERIZED APPLICATION
```
git checkout 2021-10
git pull
```
BUILD THE DOCKER IMAGE
```
mkdir /build-context/
docker build --file Dockerfile --tag academiaonline/phpinfo:latest /build-context/
```
(ALTERNATIVE WAY) BUILD THE DOCKER IMAGE USING DOCKERIGNORE
```
docker build --file Dockerfile --tag academiaonline/phpinfo:latest .
```
RUN THE CONTAINER CREATING A (HOST BIND) VOLUME TO INCLUDE THE ARTIFACT (NOT INCLUDED INSIDE THE IMAGE)
```
PHP_HOST=0.0.0.0
PHP_PORT=8080
NODE_PORT=8000
docker run --publish ${NODE_PORT}:${PHP_PORT} --volume ${PWD}/src/index.php:/src/index.php academiaonline/phpinfo:latest -f src/index.php -S ${PHP_HOST}:${PHP_PORT}
```

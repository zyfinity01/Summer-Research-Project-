Docker Installation:
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
apt-get update
apt-get install -y docker-ce
```


Now docker is installed and ready to use:

Now we can install some containers: 

Portainer: 
```
docker run -d -p 8000:8000 -p 9443:9443 -p 9000:9000 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ee:latest
```

NGINX Proxy Manager:
```
docker run -d \
    --name=nginx-proxy-manager \
    -p 81:8181 \
    -p 80:8080 \
    -p 443:4443 \
    -v /containers/nginx-proxy-manager:/config:rw \
    --network="host" \
    jlesage/nginx-proxy-manager
```

Cowrie SSH Honeypot:
```
docker run -p 2222:2222/tcp cowrie/cowrie
```


Silverstripe CMS:

Docker compose file for both the database and the frontend containers:
```
version: "3.8"
services:
  silverstripe:
    user: root
    build:
      context: ./myproject
      dockerfile: Dockerfile
    working_dir: /var/www/
    volumes:
       - ./myproject/website:/var/www
    depends_on:
       - database
    environment:
       - DOCUMENT_ROOT=/var/www/public
       - SS_TRUSTED_PROXY_IPS=*
       - SS_ENVIRONMENT_TYPE=dev
       - SS_DATABASE_SERVER=database
       - SS_DATABASE_NAME=SS_mysite
       - SS_DATABASE_USERNAME=root
       - SS_DATABASE_PASSWORD=
       - SS_DEFAULT_ADMIN_USERNAME=admin
       - SS_DEFAULT_ADMIN_PASSWORD=g6ilh69vjlzd
    ports:
      - "8080:80"

  database:
    image: mysql:5.7
    environment:
       - MYSQL_ALLOW_EMPTY_PASSWORD=yes
    volumes:
       - ./db-data:/var/lib/mysql
```
```
docker-compose build
docker-compose update
docker-compose ps
docker exec -it <containerid> bash
compose create-project silverstripe/installer .
chown -R www-data:www-data /var/www
```
Increase file upload limit to 999MB:
```
cat <<EOF > php.ini
; Maximum allowed size for uploaded files.
upload_max_filesize = 999M
post_max_size = 999M
EOF
docker cp php.ini <containerid>:/usr/local/etc/php/php.ini
```
Now visit here to build DB: http://localhost:8000/dev/build

Now the silverstripe container should be up and operational, alongside being accesible at:
http://localhost:8000

With the default admin credentials being in the docker compose config file created above.

The upload file limit has also been increased to 999MB.




Installing the user forms module:
```
docker exec -it <containerid> bash
composer require silverstripe/userforms
```

then visit to rebuild DB: http://localhost:8000/dev/build










How to mount samba share:
```
sudo apt install cifs-utils
nano /etc/fstab
sudo sh -c 'echo "//<NAS-IP>/data /mnt/data cifs rw,username=<SAMBA-SHARE-USERNAME>,password=<SAMBA-SHARE-PASSWORD>,iocharset=utf8,file_mode=0777,dir_mode=0777 0 0" >> /etc/fstab'
mount /mnt/data
```


Do note that "/data"/ in the following is the shares location setup on the synology NAS and "/mnt/data" is the location on the linux machine where this is added.






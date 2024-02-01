Docker Installation:

While loggin in to the Ubuntu VM within Proxmox, we will follow these steps:

```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

#Verify that the Docker Engine installation is successful by running the hello-world image.

sudo docker run hello-world

```


Now docker is installed and ready to use:

Now we can install some containers: 

First, create the volume that Portainer Server will use to store its database:

```
docker volume create portainer_data
```

Then, download and install the Portainer Server container:

```
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```
Now that the installation is complete, you can log into your Portainer Server instance by opening a web browser and going to:

```
https://localhost:9443
```

Using the guideline from this video "https://www.youtube.com/watch?v=fCJbw75DCZw" we will install NGINX Proxy Manager.

After successful installation, we can access the proxy manager using our machine IP with :81

```
130.195.10.178:81 
```
Default login creds for NGINX are as follows:

```
Email:    admin@example.com
Password: changeme
```

Then upon appearing the pop-up, update the details and Password.

Full Name: Ian Welch, Nickname: Ian

Email:

```
ian.welch@ecs.vuw.ac.nz
```

Effortlessly Install and Secure Nextcloud with Portainer and NGINX Proxy Manager by following the video

```
https://www.youtube.com/watch?v=vAlgkKEvBMQ&t=332s
```

Nextcloud container info:

```
PUID: 1000
PGI: 1000
TZ: Pacific/Auckland
```

Nextcoud_database container info:

```
PUID: 1000
PGI: 1000
TZ: Pacific/Auckland
MYSQL_ROOT_PASSWORD: @dPr0xm0x
MYSQL_DATABASE: nextcloud
MYSQL_USER: nextcloud
MYSQL_PASSWORD: @dPr0xM0x
```

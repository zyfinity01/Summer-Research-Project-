Hey Ian,

The best way to view the containers and make changes would be from the webui manager portainer: http://portainer.tetiimarae.maori.nz/

And if you wanted to fully recreate the container and modify it, you can do so by modifying the docker compose file as demonstrated here: https://gitlab.ecs.vuw.ac.nz/ian/datacentre/-/blob/main/documentation.md

The username for the synology NAS should be: 
User: admin-1
Pass:  D5BrBMxNvMetWV

And I have reset your password for your SSH credentials:
Public SSH IP: 103.196.108.44
Port: 22
User: ian
Pass: changeme

I have just created a new administrator account for you in nginx proxy manager:

Email: ian.welch@vuw.ac.nz
Password: temp12345

And you should be able to change the password after logging in!

http://tetiimarae.maori.nz:81/login


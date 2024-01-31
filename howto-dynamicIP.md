### Running the system with dynamic IP

For the systems deployed at places like Waitangi we have to work with a dynamic IP address.

I have registered the main domains with the New Zealand company iwantmyname but use cloudflare nameservers because it allows a separation between ownership of domain and control.

I am currently using this setup on my home system and use the [[https://ddclient.net/][ddclient]].

I installed this in Ubuntu 22.04 LTS.

    sudo apt install ddclient

I configured the daemon using this file.

```
daemon=300 \
protocol=cloudflare \
use=web, web=https://ipinfo.io/ip \
zone=ianwelch.nz \
ttl=600 \
login={MY_LOGIN_EMAIL_CLOUDFLARE} \
password={MY_GLOBAL_API} \
ianwelch.nz,nextcloud.ianwelch.nz,portainer.ianwelch.nz
```

This works for ddclient 3.9 available for my version of Ubuntu, later versions will work with API tokens that can provide fine-grained access.

Checking it works, run ddclient to see if you get errors.

    sudo ddclient -daemon=0 -debug -verbose -noquiet

Restart the service, just in case.

    sudo systemctl ddclient

Checking the status of the service.

    sudo systemctl ddclient

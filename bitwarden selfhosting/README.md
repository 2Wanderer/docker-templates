

# all-in-one docker template for running vaultwarden in docker

template contains:
- Nginx proxymanager with letsencrypt plugin.
- Vaultwarden server, a hosted password vault.
- Portainer, a web-based docker interface. do not expose the portainer gui, the CE is not supporting MFA. 
- Watchtower, automated pull image and recreate container.

The Vaultwarden container can be replace for whatever application you want to run inside this environment. 

prerequisits:

- Docker
- Docker-Compose

# Install guide:

clone the repo and run `docker-compose up -d`

visit http://yourip:81

login on the ProxyManger gui with the default credentials
User: admin@example.com 
Passwd: changeme

add proxyhosts 
- http://vaultwarden:80  Note: the vaultwarden public domain needs to be on ssl/tls (https) inorder to initialize Vaultwarden
- http://portainer:9000

optional, you can point the proxymanager gui to itself by adding:  http://vaultwarden_proxymanager_1:81 and commenting the port forward out in the docker-compose.yml
now almost everything will run over the docker network without touching the host. 

For security purposes you can add the [SELKS](https://www.stamus-networks.com/blog/selks-on-docker) stack to monitor the traffic that is traveling throug the host and docker network. this will require some additional resources. Use the provided easy-install script configure the host and docker-interface from the vaultwarden container to monitor the whole route from host interface to container.

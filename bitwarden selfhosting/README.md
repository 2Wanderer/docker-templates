

# all-in-one docker template for running vaultwarden in docker

This template contains:
- Nginx proxymanager with letsencrypt plugin.
- Vaultwarden server, a hosted password vault.
- Portainer, a web-based docker interface. do not expose the portainer gui, the CE is not supporting MFA!. 
- Watchtower, automated pull image and recreate container.

The Vaultwarden container can be replaced for whatever application you want to run inside this environment. 

# prerequisits
installed and running:

- Docker
- Docker-Compose

# Install Guide:

clone the repo and run `docker-compose up -d`

visit http://your-server-ip:81

login on the ProxyManger gui with the default credentials
User: admin@example.com 
Passwd: changeme

add the proxyhosts:
- http://vaultwarden:80  
- http://portainer:9000
- http://vaultwarden_proxymanager_1:81 (optional)

NB: you can point the proxymanager gui to itself and commenting out the port forward in the docker-compose.yml
this setup will use the docker network as much as possible, adding an extra network security layer to the host. 

Note: the vaultwarden public domain needs to be on ssl/tls (https) inorder to initialize the webvault 
for futher setup see [Vaultwarden wiki](https://github.com/dani-garcia/vaultwarden/wiki)

For security purposes you can add the [SELKS](https://www.stamus-networks.com/blog/selks-on-docker) stack to monitor the traffic that is traveling throug the host and docker network(s). This will require some additional resources. Clone the repo and use the provided easy-install script, configure the host and container networkinterface to monitor the whole route from host to container.



# All-in-one docker template for running Vaultwarden in Docker

This template contains:
- Nginx proxymanager with letsencrypt plugin.
- Vaultwarden server, a hosted password vault.
- Portainer, a web-based docker interface. do not expose the portainer gui, the CE is not supporting MFA!. 
- Watchtower, automated pull image and recreate container.

The Vaultwarden container can be replaced for whatever application you want to run inside this environment. 

# Prerequisits
installed and running:

- Docker
- Docker-Compose

# Install Guide:

Clone the repo and run `docker-compose up -d`

Visit http://your-server-ip:81

Login on the ProxyManager gui with the default credentials
User: admin@example.com 
Passwd: changeme

Add the proxyhosts:
- http://vaultwarden:80  
- http://portainer:9000
- http://vaultwarden_proxymanager_1:81*

You can point the proxymanager gui to itself and commenting out the port forward in the docker-compose.yml
this setup will use the docker network as much as possible, adding an extra network security layer to the host. 

Note: the vaultwarden public domain needs to be on ssl/tls (https) inorder to initialize the webvault 
for futher setup see the [Vaultwarden wiki](https://github.com/dani-garcia/vaultwarden/wiki)

For security purposes you can add the [SELKS](https://www.stamus-networks.com/blog/selks-on-docker) stack to monitor the traffic that is traveling throug the host and docker network(s). This will require some additional resources. Clone the repo and use the provided easy-install script, configure the host and container networkinterface to monitor the whole route from host to container.

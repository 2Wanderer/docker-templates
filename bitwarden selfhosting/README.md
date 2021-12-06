

# all-in-one docker template for running vaultwarden in docker

template contains:
- nginx proxymanager with letsencrypt plugin.
- vaultwarden server, a hosted password vault.
- portainer, a web-based docker interface. do not expose the portainer gui, the CE is not supporting MFA. 
- watchtower, automated pull image and recreate container.

The Vaultwarden container can be replace for whatever application you want to run inside this environment. 

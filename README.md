## How to host orbitgis over https in local environment
brew tap lstellway/formulae
brew update \
    && brew install lstellway/formulae/acert

## create root certificate
acert authority -trust -san '/certs/acert-orbitgis'

## create certificates for domains
acert client -parent /certs/acert-orbitgis.ca.cert.pem -key /certs/acert-orbitgis.ca.key.pem -san 'orbitgis.com,*.orbitgis.com'

## start docke-compose with nginx 
``` docker-compose up ```

## sysadmin should add following to the /etc/hosts file
```
# 192.168.0.12 should be replaced with server ip
192.168.0.12    api.orbitgis.com
192.168.0.12    viewer.orbitgis.com
```
# !! IMPORTANT !! 
This repository has been migrated to the newgeneration-sr account

this repository is archived.

For any contribution or issue, refer to the new repository !!!

---
# OpenLDAP + Fusiondirectory on Alpine Linux + S6 Overlay

# Auto configuration parameters :

- ADMIN_PASS=admin ( OpenLDAP Administrator Password )
- CONFIG_PASS= ( OpenLDAP Config Password )
- DOMAIN=example.org  ( OpenLDAP Base DN, dc=exemple,dc=org is calculated  )
- LOG_LEVEL=256   ( OpenLDAP Log Level )
- REAPPLY_PLUGIN_SCHEMAS=TRUE ( Reapply Fusiondirectory plugin schema on each container start )
- FD_ADMIN=fd-admin ( FusionDirectory Admin username )
- FD_PASS=admin ( FusionDirectory Admin password )
- INSTANCE=exemple ( FusionDirectory instance name )

# Compose file exemple

```

version: '3.1'

services:

  openldap-fd:
    image: samirkherraz/fusiondirectory
    environment:
      - ADMIN_PASS=password
      - CONFIG_PASS=password
      - DOMAIN=exemple.org
      - FD_ADMIN=fd-admin
      - FD_PASS=password
      - INSTANCE=exemple
    ports:
      - 8000:80
      - 389:389
    volumes:
      - openldap-data:/var/lib/openldap/
      - openldap-config:/etc/openldap/
    networks:
      default:
    deploy:
      resources:
        limits:
          memory: 256M
      restart_policy:
        condition: on-failure
      mode: global


volumes:
    openldap-data:
    openldap-config:

```

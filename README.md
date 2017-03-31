# minion-vm

This rework is based on promising unmaintaned mozilla project [minion-vm](https://github.com/mozilla/minion-vm)

USE ONLY FOR TESTING PURPOSES

What compose file contains
-----------------------------

- Official mongo image
- Official rabbitmq image
- SMTP relay image by @juanluisbaptiste
- Slapd image by @nickstenning for LDAP authentication (see details below)
- Dockerfile for [my minion-frontend fork](https://github.com/ilyaglow/minion-frontend) (branch docker-ready)
- Dockerfile for [my minion-backend fork](https://github.com/ilyaglow/minion-backed) (branch docker-ready too)

How to give it a try
--------------------

First of all, build all images:

```
docker-compose up
```

Add administrator user (you should have python and requests package):

```
wget -O- https://raw.githubusercontent.com/mozilla/minion-backend/master/scripts/minion-create-user | python - minion@example.com "Minion Admin" administrator
```

Login as user `minion` and password `MinionBuiltin` on `http://localhost:8080`

Fill database with test data
----------------------------

You can use [this script](https://github.com/mozilla/minion-backend/blob/master/scripts/minion-db-init) from minion-backend repo


LDAP authentication
-------------------

For this compose I made OpenLDAP db with predefined user that mounts to slapd docker.

If you want to add another user you can use ldapadd:

```
ldapadd -D "cn=admin,dc=example,dc=com" -w password -f user.ldif -H ldap://localhost:3389
```

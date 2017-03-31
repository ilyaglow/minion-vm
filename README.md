<<<<<<< HEAD
# Docker minion-vm

This rework is based on promising unmaintaned mozilla project [minion](https://github.com/mozilla/minion) developed by amazing April King (april@mozilla.com)
=======
# minion-vm

This rework is based on promising unmaintaned mozilla project [minion-vm](https://github.com/mozilla/minion-vm) developed by amazing April King (april@mozilla.com)
>>>>>>> f248e341ebf4f85530f8e0f2bd65026427aba17b

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

You can use [this script](https://gist.github.com/ilyaglow/b20be35fab7a32c51480f9d96d869ebb) from my gist


LDAP authentication
-------------------

For this compose I made OpenLDAP database with two predefined users (`admin`:`password` and `minion`:`MinionBuiltin`) that mounts to slapd docker (BE AWARE OF THIS PREDEFINED CREDENTIALS).

<<<<<<< HEAD
If you want to add another user you can use `ldapadd`:
=======
If you want to add another user you can use ldapadd:
>>>>>>> f248e341ebf4f85530f8e0f2bd65026427aba17b

```
ldapadd -D "cn=admin,dc=example,dc=com" -w password -f user.ldif -H ldap://localhost:3389
```

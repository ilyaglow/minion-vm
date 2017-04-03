# Docker minion-vm

This rework is based on promising unmaintaned mozilla project [minion](https://github.com/mozilla/minion) developed by amazing April King (april@mozilla.com)

**USE ONLY FOR TESTING PURPOSES**

What compose file contains
-----------------------------

- Official mongo image
- Official rabbitmq image
- SMTP relay image by @juanluisbaptiste
- Slapd image by @nickstenning for LDAP authentication (see details below)
- Dockerfile for [my minion-frontend fork](https://github.com/ilyaglow/minion-frontend/tree/docker-ready) (branch docker-ready)
- Dockerfile for [my minion-backend fork](https://github.com/ilyaglow/minion-backend/tree/docker-ready) (branch docker-ready too)

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

Add minion admin user to ldap database (**BE AWARE OF THIS PREDEFINED CREDENTIALS FOR LDAP AND MINION ADMIN USERS**):

```
ldapadd -D "cn=admin,dc=example,dc=com" -w password -f minion-admin.ldif -H ldap://localhost:10389
```

Login as user `minion` and password `MinionBuiltin` on `http://localhost:8080`

Fill database with test data
----------------------------

You can use [this script](https://gist.github.com/ilyaglow/b20be35fab7a32c51480f9d96d869ebb) from my gist

LDAP authentication
-------------------

If you want to add another user you can use `ldapadd`:

```
ldapadd -D "cn=admin,dc=example,dc=com" -w password -f user.ldif -H ldap://localhost:10389
```

Use `minion-admin.ldif` file as an example

Start mongodb

```
docker run -d --name my-mongo mongodb
```

Start rabbitmq

```
docker run -d --name my-rabbit rabbitmq
```

Start backend:

```
docker run -it -p 8383:8383 --link my-mongo:mongodb --link my-rabbit:rabbitmq --name my-minion-backend my-minion-backend
```

Start ldap:

```
docker run -e LDAP_DOMAIN=example.com -e LDAP_ORGANISATION="My Mega Corporation" -e LDAP_ROOTPASS=password -p 10389:389 nickstenning/slapd
```

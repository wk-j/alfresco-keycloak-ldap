## Alfresco and Keycloak Integration

- [Alfresco Identity Service](https://community.alfresco.com/people/gravitonian/blog/2018/07/17/getting-started-with-alfresco-identity-service-ea-keycloak)
- [Source](https://github.com/gravitonian/alfresco-dbp-keycloak-integration)

- http://localhost:8081/share
- http://localhost:8080/auth/admin/master/console
- http://localhost:8080/auth/realms/alfresco-dbp

#### Restart Content Service

```bash
docker-compose stop content
docker-compose rm content
y
docker-compose up -d --no-deps content
```

#### Test Authentication

```bash
curl http://localhost:8080/auth/realms/alfresco-dbp

curl -d 'client_id=alfresco-client' \
    -d 'username=wk@gmail.com' \
    -d 'password=1234' \
    -d 'grant_type=password' \
    'http://localhost:8080/auth/realms/alfresco-dbp/protocol/openid-connect/token' | python -m json.tool

curl -d 'client_id=alfresco-client' \
    -d 'username=admin' \
    -d 'password=admin' \
    -d 'grant_type=password' \
    'http://localhost:8080/auth/realms/alfresco-dbp/protocol/openid-connect/token' | python -m json.tool
```

```bash
curl http://localhost:8082/alfresco/api/-default-/public/alfresco/versions/1/nodes/-root-/children \
    -H "Authorization: bearer <TOKEN>" | python -m json.tool
```
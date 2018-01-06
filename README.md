[![Build Status](https://travis-ci.org/ptrivedi9400/oauth2-auth-server-spring-boot.svg?branch=master)](https://travis-ci.org/ptrivedi9400/oauth2-auth-server-spring-boot)

# Build and Run
```java
mvn clean install -DskipTests spring-boot:run
```
# Usage
### Checking app is deployed sucessfullly
```sh
curl -i http://localhost:8080/api/hello
Hello User!
```
### Access secure resource with token
```sh
curl -i http://localhost:8080/api/secure

{"timestamp":1444985908768,"status":401,"error":"Unauthorized","message":"Access Denied","path":"/api/secure"}
```
### Fetching client_credentials
```sh
curl -vu prerakapp:secret -X POST 'http://localhost:8080/api/oauth/token?username=admin&password=admin&grant_type=client_credentials'

{"access_token":"295a37a9-159d-4514-9341-994bd33a559c","token_type":"bearer","expires_in":1799,"scope":"read write"}
```

### Fetching refresh_token
```sh
curl -vu prerakapp:secret -X POST 'http://localhost:8080/api/oauth/token?username=admin&password=admin&grant_type=password'

{"access_token":"91202244-431f-444a-b053-7f50716f2012","token_type":"bearer","refresh_token":"e6f8624f-213d-4343-a971-980e83f734be","expires_in":1738,"scope":"read write"}
```

### Fetching acess_token by submitting refresh_token
```sh
curl -vu prerakapp:secret -X POST 'http://localhost:8080/api/oauth/token?grant_type=refresh_token&refresh_token=<refresh_token>'

{"access_token":"821c99d4-2c9f-4990-b68d-18eacaff54b2","token_type":"bearer","refresh_token":"e6f8624f-213d-4343-a971-980e83f734be","expires_in":1799,"scope":"read write"}
```

### Access secure resource sucessfully
```sh
curl -i -H "Authorization: Bearer <access_token>" http://localhost:8080/api/secure

Secure Hello!
```

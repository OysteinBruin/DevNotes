


This guide is for using Docker desktop on Windows.


Troubleshooting communication between containers

Enter running container terminal tab in docker desktop

ping: 
install ping in container: `apt-get update && apt-get install iputils-ping`

curl:
install curl in container: `apt-get update && apt-get install curl`

use container name as host name in curl command: `curl http://<container name>/path/to/api`

E.g: `curl https://identity-server/.well-known/openid-configuration`

curl https://localhost:7105/.well-known/openid-configuration

curl https://localhost:7104/Catalog/debug

`curl https://jsonplaceholder.typicode.com/todos/1`

`curl http://localhost:5105/.well-known/openid-configuration`

`curl http://identity-server/.well-known/openid-configuration`  
`curl https://identity-server/.well-known/openid-configuration`

`curl http://basket-api/WeatherForecast`


`curl http://catalog-api/Catalog/items?itemCategory=speaker&pageSize=10&pageIndex=0`  

`curl http://catalog-api/Catalog/items?itemCategory=speaker&pageSize=10&pageIndex=0`

`curl http://catalog-api/Catalog/items?itemCategory=speaker&pageSize=10&pageIndex=0`

curl https://catalog-api/Catalog/debug/



`curl https://host.docker.internal:7105/.well-known/openid-configuration`

`curl http://host.docker.internal:5105/.well-known/openid-configuration`
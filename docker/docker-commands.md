### Docker Build


```powershell	
-f #dockerfile path  
-t #image tag  
```	

```powershell	
# show values computed by helm
helm get all release-name
```	

```powershell	
# show values computed by helm
helm get all release-name
```	


`docker build -f ./Path/To/Dockerfile -t myname/my-img-name:0.1.0 .` 
`docker build -f ./Weather.Service/Dockerfile -t oysteinbruin/weather-service:0.1.1 .`

`docker images`


### Docker Run

```powershell	
-rm #remove intermediate images
-p port mapping
-e environment varialbles
-d detached
```	

`docker run -d --restart=always -p 8080:80 image_name:version` oysteinbruin/weather-service:0.1.0 
`docker build -f ./Weather.Service/Dockerfile -t oysteinbruin/weather-service:0.1.1 .`

`docker run -d --rm -p 5000:5000 -p 5001:5001 -e ASPNETCORE_HTTP_PORT=https://+:5001 -e ASPNETCORE_URLS=http://+:5000 -e ASPNET
CORE_ENVIRONMENT=development oysteinbruin/weather-service:0.1.1`



`docker-compose up -d` run detached (keeps the terminal free for use, no docker output)

How to get docker-compose to always re-create containers from fresh images
`docker-compose build --no-cache`

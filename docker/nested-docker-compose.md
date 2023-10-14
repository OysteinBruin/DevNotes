Reference addtional docker-compose files from a docker-compose file.

```yaml
service-one:
  extends:
    file: ./path/to/docker-compose.yaml
    service: service-one

service-two:
  extends:
    file: ./path/to/docker-compose.yaml
    service: service-two
  environment:
    - BACKEND=some_other_value
```



https://stackoverflow.com/questions/33408118/inheritance-or-nesting-with-docker-compose
### Execute queries from influxdb docker container

- From docker continer, open Exec tab in docker desktop
- Following command selects all for the last minute:
  - `influx query 'from(bucket:"YOUR_BUCKET_NAME") |> range(start:-1m)'`

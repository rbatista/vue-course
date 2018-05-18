# vue-course

## Running
Run a docker with nginx sharing a volume with the html:
```
docker run --name nginx-node -v /code/vue:/usr/share/ngix/html:ro -d -p 8080:80 nginx
```

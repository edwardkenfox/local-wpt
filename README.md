# local-wpt

https://medium.com/@francis.john/local-webpagetest-using-docker-90441d7c2513

## Getting started

```sh
# setup server
$ docker build -t local-wptserver ./server/

# setup agent
$ chmod u+x agent/script.sh
$ docker build -t local-wptagent ./agent/

# run server + agent
$ docker run -d -p 4000:80 local-wptserver
$ docker run -d -p 4001:80 --net="host" -e "SERVER_URL=http://localhost:4000/work/" -e "LOCATION=Test" local-wptagent

# or run server + agent with charles (not working)
$ docker run -d -p 4000:80 -e HTTP_PROXY="http://localhost:8888" -e HTTPS_PROXY="https://localhost:8888" local-wptserver
$ docker run -d -p 4001:80 --net="host" -e "SERVER_URL=http://localhost:4000/work/" -e "LOCATION=Test" -e HTTP_PROXY="http://localhost:8888" -e HTTPS_PROXY="https://localhost:8888" local-wptagent
```

## Related

- https://docs.docker.com/network/proxy/#configure-the-docker-client
- https://github.com/WPO-Foundation/wptagent/blob/master/Dockerfile
- https://docs.docker.com/network/proxy/
- https://github.com/codekitchen/dinghy
- https://github.com/codekitchen/dinghy-http-proxy
- https://github.com/nginx-proxy/nginx-proxy#custom-nginx-configuration

docker build -t devopsbathinasirisha28/nginx:v1 .
(docker build -t nginx:v1 .)

docker run -dit -p 80:80 nginx:v1
Tag image
docker tag nginx:latest nginx:v1
To login dockerhub
 docker login

 docker tag nginx:v1 devopsbathinasirisha28/nginx:v1
 docker push devopsbathiansirisha28/nginx:v1


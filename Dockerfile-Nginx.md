```sh 
# Use the official Nginx image as the base image
FROM nginx:latest

# Remove the default Nginx website
RUN rm -rf /usr/share/nginx/html/*

# Copy the application files to the Nginx html directory
COPY index.html  /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start Nginx when the container launches
CMD ["nginx", "-g", "daemon off;"]
```

```sh
docker build -t devopsbathinasirisha28/nginxapp:latest .
```
```sh
docker run -d -p 80:80 --name my-app devopsbathinasirisha28/nginxapp:latest
```
```sh
docker push devopsbathinasirisha28/nginxapp:latest
```
```sh
docker login
```


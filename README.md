# Generate keys
docker run --rm --entrypoint="" \
  -v $(pwd):/mnt \
  matrixdotorg/dendrite-monolith:latest \
  /usr/bin/generate-keys \
  -private-key /mnt/matrix_key.pem \
  -tls-cert /mnt/server.crt \
  -tls-key /mnt/server.key

## You can custom the config in config/dendrite.yaml

# Run docker compose
docker compose up -d && docker compose logs -f

### Check http://localhost:8008/

# Run Cinny or run Element
docker run -d -p 8080:80 mrbghndevops/cinny:v1
docker run -d -p 80:80 mrbghndevops/element-web:v1

### You can clone Cinny and build your own image
https://github.com/cinnyapp/cinny
### You can clone Element and build your own image
https://github.com/element-hq/element-web

# Create new user
docker exec -it <container matrix> /bin/sh
## To create admin user
/usr/bin/create-account -config /etc/dendrite/dendrite.yaml -username <username_here> -admin
## To create normal user
/usr/bin/create-account -config /etc/dendrite/dendrite.yaml -username <username_here>

# Access http://localhost:8080/
Homeserver: http://localhost:8008/
Login with your username and password!

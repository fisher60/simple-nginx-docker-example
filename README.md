## Summary
This is a simple example project that allows someone to quickly host a static site using Nginx with Docker Compose.
This version is intentionally simplified. This container can also have the ability to reverse proxy to any service
running on the local machine by removing the `ports` from the docker-compose file and instead running this container
in network mode and writing templates for the proxies in the mounted template volume.

## Sample usage:
`docker compose up`
Then visit `localhost` on your current computer. You can also access this site from any device on the local network.

## Configuration
If you wish to host dynamic sites and use this Nginx container as ingress for your entire server, you may wish to
remove the `ports` bindings and instead run the container with `network_mode: host`. This will allow the container
to access your machine's interfaces as if it were running on the host machine. This means you no longer need to
bind to specific ports and you can reference other services running on the machine.

Example:
I have a web service running in a Docker container and it exposes port `8000` and I own the
domain `testdomain.com`. I can add this configuration to my templates directory and proxy to the service:
```
server {
    listen       80;
    listen       [::]:80;
    server_name  my_website.testdomain.com;

    location / {
        proxy_pass http://127.0.0.1:8000/;
    }
}
```
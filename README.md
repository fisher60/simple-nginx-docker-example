## Summary
This is a simple example project that allows someone to quickly host a static site using Nginx with Docker Compose.
This version is intentionally simplified. This container can also have the ability to reverse proxy to any service
running on the local machine by removing the `ports` from the docker-compose file and instead running this container
in network mode and writing templates for the proxies in the mounted template volume.

Sample usage:
`docker compose up`
Then visit `localhost` on your current computer. You can also access this site from any device on the local network.
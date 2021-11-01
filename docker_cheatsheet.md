# Docker Cheatsheet
## Containers
- List exited containers: `docker ps -q -f 'status=exited'`
- Remove exited containers: `docker rm $(docker ps -q -f 'status=exited')`
## Images
- List dangling images: `docker images -q -f "dangling=true" `
## Volumes
- List dangling volumes: `docker volume ls -qf dangling=true`
- Removing dangling volumes: `docker volume rm $(docker volume ls -qf dangling=true)` or `docker volume ls -qf dangling=true | xargs -r docker volume rm`

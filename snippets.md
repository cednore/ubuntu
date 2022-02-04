# Useful snippets

```sh
# Clear recent files list on nautilus
rm ~/.local/share/recently-used.xbel

# Get local IP address of all docker containers
docker inspect -f "{{.Name}} - {{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}" $(docker ps -aq)

# Clean everything on your local docker environment
docker system df && docker system prune --all --volumes --force && docker system df

# ls with numerical chmod permissions
ls -l | awk '{k=0;for(i=0;i<=8;i++)k+=((substr($1,i+2,1)~/[rwx]/) *2^(8-i));if(k)printf("%0o ",k);print}'
```

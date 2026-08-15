# docker-images
Place to store my docker images.

## run

### docker
```shell
  docker run -it --rm 
         --network host \
         --security-opt label=disable \
         --userns=keep-id \
         -v "$(pwd):/home/opencode/workspace:Z" \
         -v "$HOME/.config/opencode/opencode.json:/home/opencode/.config/opencode/opencode.json:ro" \
         -v opencode-cache:/home/opencode/.cache/opencode \
         -w /home/opencode/workspace \
         opencode-alpine
```
### podman
```shell
  podman run -it --rm \
         --network host \
         --security-opt label=disable \
         --userns=keep-id \
         -v "$(pwd):/home/opencode/workspace:Z" \
         -v "$HOME/.config/opencode/opencode.json:/home/opencode/.config/opencode/opencode.json:ro" \
         -v opencode-data:/home/opencode/.local/share/opencode \
         -w /home/opencode/workspace \
         opencode-alpine
```
## build image
### docker
```shell
  docker build -t opencode-alpine .
```
### podman
```shell
  podman build -t opencode-alpine .
```

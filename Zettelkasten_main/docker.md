cleaning
https://stackoverflow.com/questions/46672001/is-it-safe-to-clean-docker-overlay2

clean images
```bash
docker image prune
```


clean build artefacts and caches
```bash
docker buildx prune --all
docker builder prune --all
```


removes:
- all stopped containers
- all networks not used by at least one container
- all volumes not used by at least one container
- all images without at least one container

```bash
docker system prune
```
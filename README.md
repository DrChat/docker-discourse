# Alternate Discourse launcher
TLDR: This splits out the `launcher` script so that it is no longer required to deploy a Discourse instance.

In other words, you can now fully build your own Discourse image, publish it into a Docker container registry, and a server can launch that image directly.

_Note:_ The Discourse team is also working on a new launcher script [here](https://github.com/discourse/launcher).

## Build and Deploy
```
python ./build.py build app.yaml

# To publish to Azure CR:
docker tag local_discourse/app <registry>.azurecr.io/discourse:latest
docker push <registry>.azurecr.io/discourse:latest
```

## Local testing commands
### Create an admin account
```
python ./build.py enter app.local.yaml
cd /var/www/discourse
rake admin:create
```

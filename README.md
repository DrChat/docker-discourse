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

## Prebuilt Image
You can use the [prebuilt image](https://github.com/users/DrChat/packages/container/package/docker-discourse) instead of building one yourself.
The image is built from `app.yaml`, and apart from some compatibility patches for Azure, it is a clean copy of Discourse's official image.

You will need to specify some settings using environment variables; see the `env` block in `app.local.yml` for reference.

You can also use the `start-cmd` mode from the build script to dump out a command-line you can start from.

```
python ./build.py start-cmd app.local.yml
```

## Local testing commands
### Build and deploy a local instance
```
python ./build.py build app.local.yaml
python ./build.py start app.local.yaml
```

Discourse will be available at http://localhost

### Create an admin account
```
python ./build.py enter app.local.yaml
cd /var/www/discourse
rake admin:create
```

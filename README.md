# vcl-portainer
Customised derived portainer images


## About

We can customise a portainer on start-up with a specified logo and applications feed. Provide a set of custom set-ups, eg for all OU apps, or just the apps  associated with a specific module.


### Running portainer

`docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer-ce`

Port 8000 is for the portainer edge agent.

### Customising portainer at runtime

Customise on start using [portainer CLI options](https://documentation.portainer.io/v2.0/deploy/cli/):

`docker run -d -p 9000:9000 -p 8000:8000 -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer-ce --templates http://my-host.my-domain/templates.json`

Useful flags:

- `--logo`: URL for custom logo (size: 155px by 55px )
- `--templates`, `-t`: URL for custom app template

We could use this approach to provide a new `CMD` in a derived container to use custom specificed paths.


### Cross-building portainer image (`docker buildx`)

Portainer build / Docker push script: https://github.com/portainer/portainer/blob/develop/build.sh

If we make changes to the portainer, we can grapb a quick image from it as:

`docker commit portainer wip/portainer`

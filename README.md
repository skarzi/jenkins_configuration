# jenkins_casc

Jenkins master configuration as a code

## Deployment

`docker` and `docker-compose` is needed to deploy Jenkins master with
`docker-plugin` cloud.


### Environment variables

Firstly run following command to populate environment variables:

```bash
cp -R .envs/.dist .envs/.production
```

Then edit it carefully and fill all required values (environment variables
with `!!SET_VALUE!!` value):

+ `.envs/.production/.master`:
    + `VIRTUAL_HOST` -  Jenkins' master host


### Secrets

Populate all secrets defined in `docker-compose.yml`:

+ `.secrets/admin_password` - Jenkins' admin password
+ `.secrets/delfina_password` - Delfina's password
+ `.secrets/skarzi_docker_hub_password` - properly encrypted by Jenkins,
  personal access token or password to
  [`skarzi` docker hub](https://hub.docker.com/u/skarzi) where Jenkins' slave
  image is hosted


### Docker compose override

Create `docker-compose.override.yml`:

```bash
cp docker-compose.override.yml.example docker-compose.override.yml
```

Now fill all required values (with `!!SET_VALUE!!` value) inside newly created
file:

+ `DOCKER_GID` - `docker` group GID from your system. You can get this value
  by checking it in `/etc/group` file or running following command:
  `getent group docker | cut -d : -f 3`


### Run services

Use `docker-compose` to run Jenkins' master and slaves behind nginx reverse
proxy.

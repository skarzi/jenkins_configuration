# jenkins_casc

Jenkins master configuration as a code

## Deployment

`docker` and `docker-compose` is needed to deploy Jenkins master with 2 slaves.

### Environment variables

Firstly run following command to populate environment variables:

```bash
cp -R .envs/.dist .envs/.production
```

Then edit it carefully and fill all required values (environment variables
with `!!SET_VALUE!!` value):

+ `.envs/.production/.master`:
    + `VIRTUAL_HOST` -  Jenkins' master host
+ `.envs/.production/.slave-{i}`:
    + `JENKINS_URL` - Jenkins' master URL
    + `JENKINS_SECRET` - Jenkins' slave/node secret


### Secrets

Populate all secrets defined in `docker-compose.yml`:

+ `.secrets/admin_password` - Jenkins' admin password


### Run services

Use `docker-compose` to run Jenkins' master and slaves behind nginx reverse
proxy.

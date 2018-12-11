# Using vagrant within docker as validator

## Build container

In git root directory:

```bash
docker build . -t vagrant-dev -f contrib/docker/Dockerfile

```

it should produce docker image tagged `vagrant-dev`

## Use container as validator

We run docker and mount inside current directory under `/srv` as read only.
Then we must copy Vagrantfile to writable location inside container, and then we can run commands,
for example `vaidate` with `-p` option to ignore providers:

```bash
docker run -v "$(pwd):/srv/:ro" \
    --entrypoint /bin/bash \
    -it vagrant-dev \
    -c "cp /srv/Vagrantfile /tmp/Vagrantfile && cd /tmp/ && /usr/src/vagrant/exec/vagrant validate -p"
```

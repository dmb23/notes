#Devcontainer in VSCode - container platform

One of the ways to evade the eternal struggle against the gods of ARM64 might be to use development containers in VS Code. Those should be possible to set up with a different architecture (as long as performeance is not becoming painful).

So far, some key steps I discovered:

- use a `docker-compose.yml`, because this allows to specify `platform: linux/amd64`.
    - this is also possible as a commandline flag to `docker build`, but not in `devcontainer.json`
- set `"features": {"buildkit": false}` in the docker engine config. Otherwise there is a [bug with docker compose](https://github.com/docker/compose/issues/8449)

# Devcontainers in VS Code - SSH on Mac

VS Code forwards the keys stored in the ssh-agent on the host machine to the container. This should allow to access any private repository, which the host machine has access to. 

HOWEVER, 

- Mac OS Monterey (12./ * ) does not read any key into the ssh-agent on startup, but only fills the agent lazily, when a key is required. 
- If I read all keys into the agent via `ssh-add -A` before starting the devcontainer, I have multiple keys in the agent, but the config which key to use when is lost.

So at this point I can:

- explicitly forward the ssh-agent as described in [this issue](https://github.com/microsoft/vscode-remote-release/issues/4024). Unfortunately it does not work for me. Possibly some problem with `SSH_AUTH_SOCK` on newer Macs (coming from another issue)? I don't know.

``` json
    "mounts": [
        "source=/run/host-services/ssh-auth.sock,target=/run/host-services/ssh-auth.sock,type=bind,consistency=cached"
    ],
    "containerEnv": {
        "SSH_AUTH_SOCK": "/run/host-services/ssh-auth.sock"
    },
```

- include the relevant key via an "initializeCommand" manually in the container. Requires hardcoding the path to the key for the specific container. 
- ssh once from a terminal outside of the container to the relevant repo. This lazily loads the correct key into the agent, which is then available inside the container and the only key present. Bleurgh. But I will probably do this.

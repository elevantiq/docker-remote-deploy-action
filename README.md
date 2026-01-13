# Docker Swarm Deploy Action

A [GitHub Action](https://github.com/features/actions) that enables you to publish your app as a [Docker stack](https://docs.docker.com/engine/swarm/stack-deploy/) to a remote Docker swarm.

## Example

Below is a brief example on how the action can be used:

```yaml
- name: Deploy to swarm
  uses: elevantiq/docker-remote-deploy-action@master
  with:
    remote_host: ssh://user@myswarm.com
    ssh_private_key: ${{ secrets.DOCKER_SSH_PRIVATE_KEY }}
    ssh_public_key: ${{ secrets.DOCKER_SSH_PUBLIC_KEY }}
    args: stack deploy --compose-file stack.yaml coolapp
```

If you are deploying any private Docker images, you can use the built-in registry authentication:

```yaml
- name: Deploy to swarm
  uses: elevantiq/docker-remote-deploy-action@master
  with:
    remote_host: ssh://user@myswarm.com
    ssh_private_key: ${{ secrets.DOCKER_SSH_PRIVATE_KEY }}
    docker_registry: ghcr.io
    docker_username: ${{ github.actor }}
    docker_password: ${{ secrets.GITHUB_TOKEN }}
    args: stack deploy --with-registry-auth --compose-file stack.yaml coolapp
```

## Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `args` | ✅ | - | Arguments to pass to the `docker` command |
| `remote_host` | ✅ | - | Docker host to connect to (e.g., `ssh://user@host`) |
| `ssh_private_key` | ❌ | - | SSH private key for authentication |
| `ssh_public_key` | ❌ | - | SSH public key of the server for verification |
| `docker_version` | ❌ | `28` | Docker CLI version (e.g., `28`, `27`, `latest`) |
| `docker_registry` | ❌ | - | Container registry to log into (e.g., `ghcr.io`) |
| `docker_username` | ❌ | - | Registry username |
| `docker_password` | ❌ | - | Registry password |
| `env` | ❌ | - | Environment variables to pass to docker command |
| `run_number` | ❌ | - | GitHub run number passed to environment |

## License

This project is licensed under the MIT license. See the [LICENSE](LICENSE) file for details.

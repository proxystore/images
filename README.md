# Proxystore Images

This repo contains Dockerfiles used for testing Proxystore's code.
"Nightly" image builds are created on the 1st and 15th of the month or when the corresponding Dockerfile is changed.

| Dockerfile | Location | Details |
| :--------  | :------- | :------ |
| [`Dockerfile-dim`](dockerfiles/Dockerfile-dim) | `ghcr.io/proxystore/proxystore-dim:nightly` | [Details](#dockerfile-dim) |
| [`Dockerfile-relay`](dockerfiles/Dockerfile-relay) | `ghcr.io/proxystore/proxystore-relay:nightly` | [Details](#dockerfile-relay) |

## Adding Dockerfiles

1. Add the Dockerfile to `dockerfiles/`.
2. Add a section in this README with any instructions.
3. Update the table in this README with the links.
4. Add a new matrix entry in [`.github/workflows/check.yml`](.github/workflows/check.yml).
5. Add a new matrix entry in [`.github/workflows/publish.yml`](.github/workflows/publish.yml).

## Dockerfile-dim

### Usage

To effectively work on a system, the `Dockerfile-dim` image needs to be compiled on the machine it will be used on.

For usage with Github Actions CI, a prebuilt image is provided.

### Pull and Run

```bash
$ docker run --rm -it --network host -v <local_path_to_proxystore_dir>:/proxystore ghcr.io/proxystore/proxystore-dim
```

### Build and Run

```bash
$ docker build -t proxystore-dim -f dockerfiles/Dockerfile-dim .
$ docker run --rm -it --network host -v <local_path_to_proxystore_dir>:/proxystore proxystore-dim
```

### Executing test cases

This can be done as usual using tox: `$ tox -e py39`.
All Python versions are available and `tox` is pre-added to the `$PATH`.

## Dockerfile-relay

Relay (signaling) server runner image for testing p2p communication.
This image installs the latest pre-release of ProxyStore from PyPI.

**Warning:** this is not intended for production use and by default runs with no security features.

### Pull and Run

```bash
$ docker run --rm -it -p 8765:8765 --name relay ghcr.io/proxystore/proxystore-relay
```

### Build and Run

```bash
$ docker build -t proxystore-relay -f dockerfiles/Dockerfile-relay .
$ docker run --rm -it -p 8765:8765 --name relay proxystore-relay
```

To run with SSL/TLS:
```bash
$ docker run --rm -it -p 8765:8765 -e PROXYSTORE_SSL_ARGS="--certfile /path/to/certfile --keyfile /path/to/keyfile" --name relay proxystore-relay
```

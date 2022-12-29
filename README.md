# Proxystore Dockerfiles

This repo contains Dockerfiles used for testing Proxystore's code.
Images are built weekly.

| Dockerfile                                     | Details                    |
| :--------------------------------------------- | :------------------------- |
| [`Dockerfile-dim`](dockerfiles/Dockerfile-dim) | [Details](#dockerfile-dim) |

## Dockerfile-dim

### Usage

To effectively work on a system, the `Dockerfile-dim` image needs to be compiled on the
machine it will be used on.

For usage with Github Actions CI, a prebuilt image is provided.

### Build

To build the dockerfile, use the following command:
```bash
$ docker build -t proxystore-dim -f dockerfile/Dockerfile-dim .
```

### Running

To run the image once built, the following command can be used:
```bash
$ docker run --rm -it --network host -v <local_path_to_proxystore_dir>:/proxystore proxystore-dim
```

### Executing test cases

This can be done as usual using tox: `$ tox -e py39`.
All Python versions are available and `tox` is pre-added to the `$PATH`.

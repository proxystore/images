# Proxystore Dockerfiles

This repo contains the dockerfiles used for testing Proxystore's code.
`Dockerfile-dim`, for instance, contains source installations of Mochi and UCX for testing with `pyenv`.

Prebuilt images will be built weekly.

## Usage
To effectively work on a system, the `Dockerfile-dim` image needs to be compiled on the
machine it will be used on.

For usage with Github Actions CI, a prebuilt image is provided.

### Build
To build the dockerfile, use the following command:

`docker build -t <img name> -f Dockerfile-dim .`

### Running
To run the image once built, the following command can be used:

`docker run --rm -it --network host -v <local_path_to_proxystore_dir>:/proxystore dim`

### Executing test cases
This can be done as usual using tox

`tox`



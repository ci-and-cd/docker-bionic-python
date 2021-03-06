# docker-bionic-pyenv-python

Python (pyenv) for multi-stage docker image build.

Dockerfile [ci-and-cd/docker-bionic-pyenv-python on Github](https://github.com/ci-and-cd/docker-bionic-pyenv-python)

[cirepo/pyenv-python on Docker Hub](https://hub.docker.com/r/cirepo/pyenv-python/)

## Use this image as a “stage” in multi-stage builds

```dockerfile

FROM ubuntu:18.04
COPY --from=cirepo/pyenv-python:2.7.16_3.7.2-bionic-archive /data/root /
RUN sudo chown -R $(whoami):$(id -gn) /home/$(whoami) \
  && sudo apt-get -y install gcc libbz2-dev libsqlite3-dev libssl-dev make zlib1g-dev \
  && touch home/$(whoami)/.profile \
  && echo 'export PATH="${HOME}/.pyenv/bin:${PATH}"\
if which pyenv > /dev/null; then eval "$(pyenv init -)"; eval "$(pyenv virtualenv-init -)"; fi' | tee -a home/$(whoami)/.profile

```

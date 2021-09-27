# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.194.0/containers/python-3-miniconda/.devcontainer/base.Dockerfile

FROM mcr.microsoft.com/vscode/devcontainers/miniconda:0-3

# [Choice] Node.js version: none, lts/*, 16, 14, 12, 10
ARG NODE_VERSION="none"
RUN if [ "${NODE_VERSION}" != "none" ]; then su vscode -c "umask 0002 && . /usr/local/share/nvm/nvm.sh && nvm install ${NODE_VERSION} 2>&1"; fi

# Copy environment.yml (if found) to a temp location so we update the environment. Also
# copy "noop.txt" so the COPY instruction does not fail if no environment.yml exists.
COPY mamba_env.yml* .devcontainer/noop.txt /tmp/


# Installs and configures micromamba.
RUN wget -qO- https://micromamba.snakepit.net/api/micromamba/linux-64/latest | tar -xvj bin/micromamba
ENV MAMBA_ROOT_PREFIX=$HOME/micromamba


RUN micromamba create -y -f tmp/mamba_env.yml

SHELL ["/bin/bash", "-c"]
RUN ./bin/micromamba shell init -s bash -p ~/micromamba
RUN source ~/.bashrc
RUN conda config --add envs_dirs /micromamba/envs/

ENTRYPOINT ["/bin/bash", "-c"]
# RUN micromamba activate mamba_env

# [Optional] Uncomment to install a different version of Python than the default
# RUN conda install -y python=3.6 \
#     && pip install --no-cache-dir pipx \
#     && pipx reinstall-all

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>


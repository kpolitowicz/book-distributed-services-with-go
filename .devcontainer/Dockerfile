# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.154.0/containers/go/.devcontainer/base.Dockerfile

# [Choice] Go version: 1, 1.15, 1.14
ARG VARIANT="1"
FROM mcr.microsoft.com/vscode/devcontainers/go:0-${VARIANT}

# [Option] Install Node.js
# ARG INSTALL_NODE="true"
# ARG NODE_VERSION="lts/*"
# RUN if [ "${INSTALL_NODE}" = "true" ]; then su vscode -c "source /usr/local/share/nvm/nvm.sh && nvm install ${NODE_VERSION} 2>&1"; fi

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

# [Optional] Uncomment the next line to use go get to install anything else you need
# RUN go get -x <your-dependency-or-tool>

# [Optional] Uncomment this line to install global node packages.
# RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g <your-package-here>" 2>&1

# Make vi the default editor
RUN echo 'export EDITOR=vi' >> /home/vscode/.bashrc

# Install protobuf tooling
RUN wget https://github.com/protocolbuffers/protobuf/releases/download/v3.14.0/protoc-3.14.0-linux-x86_64.zip
RUN unzip protoc-3.14.0-linux-x86_64.zip -d /usr/local/protobuf
RUN echo 'export PATH="$PATH:/usr/local/protobuf/bin"' >> /home/vscode/.bashrc

# Install protoc generators for golang
RUN go get github.com/gogo/protobuf/protoc-gen-gogo
# Install gRPC generators
RUN go get google.golang.org/grpc

# Make protoc binary installed above findable to vscode user
RUN chown -R vscode /usr/local/protobuf
# Allow `make compile` to write to /go/pkg/mod
RUN mkdir /go/pkg/mod
RUN chown vscode /go/pkg/mod
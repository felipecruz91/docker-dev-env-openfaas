#syntax=docker/dockerfile:1.3-labs

FROM alpine AS curl
RUN apk add --no-cache \
    curl

FROM curl AS docker-cli
ARG DOCKER_CLI_VERSION=20.10.9
RUN <<EOT ash
    curl -fL https://download.docker.com/linux/static/stable/$(uname -m)/docker-${DOCKER_CLI_VERSION}.tgz | tar zxf - --strip-components 1 docker/docker
    chmod +x /docker
EOT

FROM curl AS arkade
RUN <<EOT ash
    curl -sLS https://get.arkade.dev | sh
    arkade --help
EOT

FROM arkade AS faas-cli
ARG FAAS_CLI_VERSION=0.13.15
RUN <<EOT ash
    arkade get faas-cli@${FAAS_CLI_VERSION}
    chmod +x /root/.arkade/bin/faas-cli
    /root/.arkade/bin/faas-cli version
EOT

FROM arkade AS kubectl
ARG KUBECTL_VERSION=v1.22.0
RUN <<EOT ash
    arkade get kubectl@${KUBECTL_VERSION}
    chmod +x /root/.arkade/bin/kubectl
EOT

FROM arkade AS kind
ARG KIND_VERSION=v0.11.1
RUN <<EOT ash
    arkade get kind@${KIND_VERSION}
    /root/.arkade/bin/kind version
    chmod +x /root/.arkade/bin/kind
EOT

FROM debian:bullseye-slim AS final
RUN <<EOT bash
    apt-get update
    apt-get install -y git ca-certificates
    update-ca-certificates
EOT
COPY --from=docker-cli /docker /usr/local/bin/docker
COPY --from=arkade /usr/local/bin/arkade /usr/local/bin/arkade
COPY --from=faas-cli /root/.arkade/bin/faas-cli /usr/local/bin/faas-cli
COPY --from=kubectl /root/.arkade/bin/kubectl /usr/local/bin/kubectl
COPY --from=kind /root/.arkade/bin/kind /usr/local/bin/kind

RUN useradd -s /bin/bash -m vscode
RUN groupadd docker && usermod -aG docker vscode

USER vscode

ENTRYPOINT ["sleep", "infinity"]

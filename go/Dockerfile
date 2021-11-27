#syntax=docker/dockerfile:1.3-labs

FROM golang:1.17-alpine

RUN <<EOT ash
    apk add --no-cache git make bash shadow
EOT

COPY --from=felipecruz/dev-environments-openfaas:0.1.0-alpha /usr/local/bin/docker /usr/local/bin/docker
COPY --from=felipecruz/dev-environments-openfaas:0.1.0-alpha /usr/local/bin/arkade /usr/local/bin/arkade
COPY --from=felipecruz/dev-environments-openfaas:0.1.0-alpha /usr/local/bin/faas-cli /usr/local/bin/faas-cli
COPY --from=felipecruz/dev-environments-openfaas:0.1.0-alpha /usr/local/bin/kubectl /usr/local/bin/kubectl
COPY --from=felipecruz/dev-environments-openfaas:0.1.0-alpha /usr/local/bin/kind /usr/local/bin/kind

RUN useradd -s /bin/bash -m vscode
RUN groupadd docker && usermod -aG docker vscode

USER vscode

ENTRYPOINT ["sleep", "infinity"]

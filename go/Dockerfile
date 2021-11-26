#syntax=docker/dockerfile:1.3-labs

FROM felipecruz/dev-environments-openfaas:0.1.0-alpha AS openfaas-default


FROM docker/dev-environments-go:stable-1 AS final
COPY --from=openfaas-default /usr/local/bin/arkade /usr/local/bin/arkade
COPY --from=openfaas-default /usr/local/bin/faas-cli /usr/local/bin/faas-cli
COPY --from=openfaas-default /usr/local/bin/kubectl /usr/local/bin/kubectl
COPY --from=openfaas-default /usr/local/bin/kind /usr/local/bin/kind

USER vscode

ENTRYPOINT ["sleep", "infinity"]

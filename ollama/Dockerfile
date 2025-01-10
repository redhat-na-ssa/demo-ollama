# IMAGE=docker.io/nvidia/cuda:12.2.2-runtime-ubi9
ARG IMAGE=docker.io/nvidia/cuda:12.3.2-devel-ubi9
FROM ${IMAGE}

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

RUN dnf -y update \
    && dnf install -y --nodocs pciutils \
    && dnf clean all && rm -rf /var/cache/*

USER root

WORKDIR /ollama

RUN chmod 770 /ollama && \
    chgrp root /ollama && \
    curl https://ollama.ai/install.sh | sh

EXPOSE 8080
USER 1001

ENV OLLAMA_HOST 0.0.0.0:11434
#ENV OLLAMA_ORIGINS  http://localhost:*,http://0.0.0.0:*
ENV OLLAMA_MODELS /ollama/models

ENTRYPOINT ["/usr/local/bin/ollama"]
CMD ["serve"]

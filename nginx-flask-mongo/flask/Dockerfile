# syntax=docker/dockerfile:1.4
FROM --platform=$BUILDPLATFORM python:3.10 AS builder

WORKDIR /src

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y git

COPY requirements.txt /src
RUN --mount=type=cache,target=/root/.cache/pip \
    pip3 install -r requirements.txt

RUN groupadd -r docker && \
    useradd -r -s /bin/bash -g docker vscode

COPY . .

CMD ["python3", "server.py"]

FROM builder as dev-envs

# install Docker tools (cli, buildx, compose)
COPY --from=gloursdocker/docker / /

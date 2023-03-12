# Shared image, envs, packages for both devcontainer & prod.
FROM ruby:3.2-bullseye
RUN apt update

# Temporary multi-platform SAM CLI install method.
# https://github.com/aws/aws-sam-cli/issues/3908
RUN update-alternatives --install /usr/bin/python python /usr/bin/python3 1
RUN apt-get install -y pip && pip install aws-sam-cli

# Postgres client.
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive && \
    apt-get -y dist-upgrade && \
    apt-get install -y \
      libpq-dev \
      postgresql-client

# Install anycable-go.
RUN cd /tmp && \
    curl -L https://github.com/anycable/anycable-go/releases/download/v1.2.3/anycable-go-linux-amd64 > anycable-go-linux-amd64 && \
    chmod +x anycable-go-linux-amd64 && \
    mv anycable-go-linux-amd64 /usr/local/bin/anycable-go

# Local devcontainer Codespaces compatibility.
RUN mkdir -p /workspaces/anycable_rails_demo
ENV BUNDLE_IGNORE_CONFIG=1
ENV BUNDLE_PATH=./vendor/bundle
ENV BUNDLE_CACHE_PATH=./vendor/cache

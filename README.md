# aws-dev

A MacOS development environment for applications deployed to AWS.

## Brew

Brew is a package manager for MacOS:

    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

## JQ

Install JQ

    brew install jq

## Docker

Download Docker Desktop for Mac: https://www.docker.com/products/docker-desktop. This install apparently includes docker engine, docker compose, and Kubernetes.

## Python

Customize your zsh shell to add python3 to your path:

    sudo nano ~/.zshrc

Add the following before the “export PATH=…” line:

    path+=('/Users/larry/Library/Python/3.8/bin')

## PIP

Install PIP:

    python3 -m pip install --upgrade pip

## Localstack

Use PIP to install Localstack:

    pip3 install localstack

Confirm Docker is running and then start localstack:

    localstack start -d

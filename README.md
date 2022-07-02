# aws-dev

The following describes how I set up my macOS Monterey (12.4) development environment for applications deployed to AWS. My MacBook Pro has an M1 Pro chip.

## Z Shell

Zsh is now the default shell for macOS. Bash 3.2 (2006) is still available and will be used by shell scripts that begin with #!/bin/bash.

Confirm that Zsh is your default:

    echo $0

## Xcode

A full Xcode install includes command line tools that are installed to /Library/Developer/CommandLineTools/usr/bin. The tools include python3, pip3, and git.

## Generate key pair

Generate an Ed25519 formatted key for yourself.
    
    % ssh-keygen -t ed25519 -C "YOUR-EMAIL-ADDRESS"

Enter a secure passphrase when prompted.

Now save your passphrase to your MacOS keychain.

First configure SSH by creating ~/.ssh/config

    Host *
      AddKeysToAgent yes
      UseKeychain yes
      IdentityFile ~/.ssh/id_ed25519

Now add your private key to your keychain.

    ssh-add --apple-use-keychain ~/.ssh/id_ed25519

## GitHub

Add SSH public key to GitHub profile. See [Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account).

## Pip

Pip is the package installer for Python. 

Upgrade Pip. The upgraded version will be installed in /Users/YOUR-USER-NAME/Library/Python/3.8/lib/site-packages.

    python3 -m pip install --upgrade pip

Confirm that pip is updated.

    % pip3 --version
    pip 22.1.2 from /Users/larry/Library/Python/3.8/lib/python/site-packages/pip (python 3.8)

## Brew

Brew is a package manager for MacOS, but I only use it for things that don't have other supported installation methods.

    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

Do not install ssh or ssh-add using brew, because this could override Apple's versions of these tools.

## JQ

Install JQ.

    brew install jq

## Docker

Install Docker Desktop for Mac: https://www.docker.com/products/docker-desktop. This install includes Docker Engine, Compose, and Kubernetes.

## Localstack

Use pip to install Localstack:

    pip3 install localstack

Customize your Zsh shell to add localstack and awslocal to your path:

    sudo nano ~/.zshrc

Add the following before the “export PATH=…” line:

    path+=('/Users/YOUR-USER-NAME/Library/Python/3.8/bin')

Confirm Docker is running and then start localstack:

    localstack start -d

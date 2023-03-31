# MacOS Setup

The following describes how I set up my macOS Monterey (12.4) development environment for applications deployed to AWS. My MacBook Pro has an M1 Pro chip.

## Default Command Line Tools

MacOS Monterey incluces curl, ssh, ssh-add, and ssh-keygen. The tools are installed in /usr/bin.

## Z Shell

Zsh is now the default shell for macOS. Bash 3.2 (2006) is still available and will be used by shell scripts that begin with #!/bin/bash.

Confirm that Zsh is your default:

    echo $0

## Xcode

A full Xcode install includes command line tools that are installed to /Library/Developer/CommandLineTools/usr/bin. The tools include python3, pip3, and git. Xcode and the tools can be installed as follows:
    
    xcode-select --install
    
Somehow python3, pip3, and git are also installed in /usr/bin.

## Generate key pair

Generate an Ed25519 formatted key for yourself.
    
    ssh-keygen -t ed25519 -C "YOUR-EMAIL-ADDRESS"

Enter a secure passphrase when prompted.

Now save your passphrase to your MacOS keychain.

First configure SSH by creating ~/.ssh/config

    Host *
      AddKeysToAgent yes
      UseKeychain yes
      IdentityFile ~/.ssh/id_ed25519
      
Now add your private key passphrase to your keychain.

    ssh-add --apple-use-keychain ~/.ssh/id_ed25519
      
Or if using 1Password, add/move the id_ed25519 SSH key to your private vault and create ~/.ssh/config as follows:

    Host *
	   IdentityAgent "~/Library/Group Containers/2BUA8C4S2C.com.1password/t/agent.sock"

## GitHub

Add your public key (~/.ssh/id_ed25519) to GitHub profile. See [Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account).

## Brew

Brew is a package manager for MacOS, but I only use it for things that don't have other supported installation methods.

    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

Do not install ssh or ssh-add using brew, because this could override Apple's versions of these tools.

## Python

Reference: https://opensource.com/article/19/5/python-3-default-mac

Install Simple Python Version Management (pyenv)

    brew install pyenv

Install latest version of python

    % pyenv install 3.10 
    python-build: use openssl@1.1 from homebrew
    python-build: use readline from homebrew
    Downloading Python-3.10.10.tar.xz...
    -> https://www.python.org/ftp/python/3.10.10/Python-3.10.10.tar.xz
    Installing Python-3.10.10...
    python-build: use readline from homebrew
    python-build: use zlib from xcode sdk
    Installed Python-3.10.10 to /Users/YOUR-USER-NAME/.pyenv/versions/3.10.10

Customize your Zsh shell to add python to your path:

    sudo nano ~/.zshrc
    
    if command -v pyenv 1>/dev/null 2>&1; then
      eval "$(pyenv init -)"
    fi

## Pip

Pip is the package installer for Python. Each version of python can have it's own pip.

Upgrade pip. 

    python3 -m pip install --upgrade pip

Confirm that pip is updated.

### Python 3.8

    % pip3 --version
    pip 22.1.2 from /Users/larry/Library/Python/3.8/lib/python/site-packages/pip (python 3.8)
    
### Python 3.9 (Xcode)

    % pip3 --version
    pip 21.2.4 from /Applications/Xcode.app/Contents/Developer/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/site-packages/pip (python 3.9)
    
### Python 3.10 (Brew)
 
    % pip3 --version
    pip 23.0.1 from /opt/homebrew/lib/python3.10/site-packages/pip (python 3.10)
    
### Uninstall all packages

    pip3 freeze | xargs pip3 uninstall -y

## Additional Command Line Tools

Install JQ. JQ is used to extract data from JSON objects.

    brew install jq

Install JMESPath Terminal (jpterm).

    pip3 install jmespath-terminal

Install wget

    brew install wget

## Docker

Install Docker Desktop for Mac: https://www.docker.com/products/docker-desktop. This install includes Docker Engine, Compose, and Kubernetes.

## Localstack

Localstack requires Python3, Pip3, and Docker.

Use pip to install Localstack:

    pip3 install localstack

Confirm Docker is running and then start localstack:

    localstack start -d

## Install Terraform

Download zip from https://www.terraform.io/downloads. Extract

    sudo mv ~/Downloads/terraform /usr/local/bin/

## Visual Studio Code

Download and Install Visual Studio Code. See https://code.visualstudio.com/download. 

Install extensions:
- HashiCorp Terraform 
- Docker

## AWS Command Line Interface

See [Installing or updating the latest version of the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

    % aws --version
    aws-cli/2.7.7 Python/3.9.11 Darwin/21.5.0 exe/x86_64 prompt/off


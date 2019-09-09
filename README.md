:stylesheet:

= Prerequisites

== OSX system setup.
1. Install homebrew

    
    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    

2. Install link:https://www.vagrantup.com/downloads.html[vagrant] (optional)

    
    brew cask install vagrant
    

3. Install the hashi suite. 

    
    brew install terraform vault packer
    

4. Install git.

    
    brew install git
    

5. Install AWSCLI (optionally in `virtualenv`)

    
    pip3 install awscli --upgrade --user
    
6. Install link:https://github.com/vmware/govmomi/releases[govmomi]

    
    cd ~/Downloads && wget https://github.com/vmware/govmomi/releases/download/v0.21.0/govc_darwin_amd64.gz
    tar zxf govc_darwin_amd64.gz && gzip -d govc_darwin_amd64.gz && chmod +x govc_darwin_amd64
    sudo mv govc_darwin_amd64 /usr/local/bin/govc
    
7. Install `teleconsole` - in case we need to share terminals
    
    curl https://www.teleconsole.com/get.sh | sh

Optional utilities I like.

`zsh`, `bat`, `fd`, `docker`

    
    sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
    brew install bat fd
    


== Windows system setup.

=== Set up a linux box

==== WSL in Windows 10

1. Enable the WSL, reboot

    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux

2. Open microsoft store and pick a linux distro

==== Vagrant
1. Enable virtualization in BIOS.
2. Install link:https://www.vagrantup.com/downloads.html[vagrant]. 

NOTE: You must disable Hyper-V for vagrant to work with virtualbox.

3. Create the below `Vagrantfile`

    Vagrant.configure("2") do |config|
        config.vm.box = "bento/ubuntu-18.04"
        config.vm.network "forwarded_port", guest: 22, host: 2222
        config.vm.provision "shell", inline: 'echo "COLUMNS=250" >> /home/vagrant/.bashrc'
    end

4. Enter your machine.
    
    vagrant up
    vagrant ssh

NOTE: Note your shared folder.

    ...
    ==> default: Mounting shared folders...
    default: /vagrant => /Users/steventobias/repos/stobias-dev-assets/docs/tech-talks/terraform-workshop-101/assets/windows

5. Do all the same shit.

=== Packages

```
    sudo apt-get update
    sudo apt-get install -y git \
                            python3 \
                            python3-pip \
                            golang \
                            unzip \
                            curl \ 
                            gunzip \
                            wget 

    ## terraform
    wget https://releases.hashicorp.com/terraform/0.12.7/terraform_0.12.7_linux_amd64.zip
    unzip terraform_0.12.7_linux_amd64.zip &&  sudo mv terraform /usr/local/bin/

    ## govc
    cd ~/Downloads && wget https://github.com/vmware/govmomi/releases/download/v0.21.0/govc_linux_amd64.gz
    tar zxf govc_linux_amd64.gz && gunzip -d govc_linux_amd64.gz && chmod +x govc_linux_amd64
    sudo mv govc_linux_amd64 /usr/local/bin/govc

    ## teleconsole
    curl https://www.teleconsole.com/get.sh | sh

    ## AWSCLI
    pip3 install awscli --upgrade --user
    
```

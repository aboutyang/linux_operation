# Post Install Ubuntu 18.10 and deriviates

## Update System

```shell
sudo apt-get update -y && sudo apt-get upgrade -y
sudo apt-get install -y wget curl git gitk vim-nox build-essential linux-headers-$(uname -r) dkms gdebi zsh gnome-tweak-tool gparted nautilus-dropbox keepass2
```

## Install Powerline fonts

```
mkdir ~/gitrepos && cd ~/gitrepos
git clone https://github.com/powerline/fonts.git
cd fonts && ./install.sh

```
## Configure Git

```
git config --global user.name $USER
git config --global user.email $USER@$HOSTNAME.nl
```

## Oh-my-zsh

`wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh`

Make it your default shell. You will need to log off after this.

```
chsh -s `which zsh`

```

Oh My Zsh Themes

```
cd ~/.oh-my-zsh/themes
wget https://raw.githubusercontent.com/dikiaap/dotfiles/master/.oh-my-zsh/themes/oxide.zsh-theme
wget https://raw.githubusercontent.com/jacqinthebox/arm-templates-and-configs/master/fino-clean.zsh-theme
wget https://raw.githubusercontent.com/agnoster/agnoster-zsh-theme/master/agnoster.zsh-theme
wget https://raw.githubusercontent.com/caiogondim/bullet-train-oh-my-zsh-theme/master/bullet-train.zsh-theme
```


## Docker

```
sudo apt install docker.io
sudo systemctl start docker
sudo systemctl enable docker

```

Fix sudo (requires logoff):

```
sudo usermod -aG docker $USER

```

[https://github.com/docker/compose/releases](https://github.com/docker/compose/releases)

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose
```

Kubectl & Minikube

```
sudo apt-get update && sudo apt-get install -y apt-transport-https
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update
sudo apt-get install -y kubectl

wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
chmod +x minikube-linux-amd64
sudo mv minikube-linux-amd64 /usr/local/bin/minikube

```

## Node.js and npm fix

```
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs
mkdir ~/npm-global -p
sudo chown -R $USER:$USER ~/npm-global
npm config set prefix '~/npm-global'
echo "export PATH=~/npm-global/bin:$PATH" >> ~/.zshrc

```

## Vim

```
mkdir -p ~/.vim/autoload ~/.vim/bundle && curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim
cd ~/.vim/bundle
git clone https://github.com/scrooloose/nerdtree.git
git clone https://github.com/Valloric/MatchTagAlways.git
git clone https://github.com/ctrlpvim/ctrlp.vim.git
git clone https://github.com/vim-airline/vim-airline.git 
git clone https://github.com/vim-airline/vim-airline-themes.git 
git clone https://github.com/lukaszb/vim-web-indent.git
git clone https://github.com/hashivim/vim-vagrant.git
git clone https://github.com/altercation/vim-colors-solarized.git
git clone https://github.com/kristijanhusak/vim-hybrid-material

cd vim-hybrid-material/colors && mkdir ~/.vim/colors
cp * ~/.vim/colors
```

Copy vmrc
```
wget -O ~/.vimrc https://raw.githubusercontent.com/jacqinthebox/arm-templates-and-configs/master/vimrc
```


## Virtualbox

```
cd ~/Downloads
sudo sh -c 'echo "deb http://download.virtualbox.org/virtualbox/debian bionic contrib" >> /etc/apt/sources.list.d/virtualbox.list'
wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -
sudo apt-get update -y && sudo apt-get install virtualbox-6.0 -y
```


## Vagrant
```
cd ~/Downloads
wget -nc https://releases.hashicorp.com/vagrant/2.2.2/vagrant_2.2.2_x86_64.deb
if [ ! -f /usr/bin/vagrant ] ; then
   sudo dpkg -i vagrant_2.2.2_x86_64.deb
fi
```

## Install .net core

[https://www.microsoft.com/net/download/linux-package-manager/ubuntu18-04/sdk-current](https://www.microsoft.com/net/download/linux-package-manager/ubuntu18-04/sdk-current)

```
wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb && sudo apt-get install apt-transport-https && sudo apt-get update -y && sudo apt-get install dotnet-sdk-2.2 -y
```

# PowerShell
[https://docs.microsoft.com/en-us/powershell/scripting/setup/installing-powershell-core-on-linux?view=powershell-6](https://docs.microsoft.com/en-us/powershell/scripting/setup/installing-powershell-core-on-linux?view=powershell-6)

```
# Import the public repository GPG keys
cd ~/Downloads
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

#Register the Microsoft Ubuntu repository
sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list

# Install
sudo apt-get update -y && sudo apt-get install -y powershell-preview

#Start PowerShell
pwsh-preview

```


## Atom

```
cd ~/Downloads
wget -q https://github.com/atom/atom/releases/download/v1.34.0-beta1/atom-amd64.deb
sudo dpkg -i atom-amd64.deb
```

## Visual Studio Code

```
cd ~/Downloads
wget -o vscode.deb https://go.microsoft.com/fwlink/?LinkID=760868
sudo dpkg -i vscode.deb
```

Settings: 
```
{
    "workbench.iconTheme": "material-icon-theme",
    "editor.fontSize": 12,
    "window.zoomLevel": 0,
    "terminal.integrated.fontFamily": "Meslo LG M DZ for Powerline",
    "window.restoreWindows": "none",
    "terminal.integrated.fontSize": 12,
    "editor.minimap.enabled": false,
    "editor.multiCursorModifier": "ctrlCmd",
    "workbench.colorTheme": "Monokai Dimmed",
    "powershell.scriptAnalysis.enable": true,
    "editor.formatOnType": true,
    "editor.formatOnSave": true
}
```

### Operations Studio

[https://docs.microsoft.com/en-us/sql/sql-operations-studio/download](https://docs.microsoft.com/en-us/sql/sql-operations-studio/download)

```
cd ~/Downloads
wget -o sqlstudio.deb https://go.microsoft.com/fwlink/?linkid=2030750
sudo dpkg -i install sqlstudio.deb
```

## When having internet connectivity problems

`vim /etc/NetworkManager/NetworkManager.conf`

Comment out the line dns=dnsmasq, so it looks like this:
`dns=dnsmasq`

Then
```
sudo restart network-manager
sudo service network-manager restart
```

## Nice theme

```
sudo add-apt-repository ppa:daniruiz/flat-remix
sudo apt-get update
sudo apt-get install flat-remix-gtk
```

### Icons

```
cd /tmp && rm -rf flat-remix &&
git clone https://github.com/daniruiz/flat-remix &&
mkdir -p ~/.icons && cp -r flat-remix/Flat-Remix* ~/.icons/ &&
gsettings set org.gnome.desktop.interface icon-theme "Flat-Remix"
```

## Oracle Java 8 for xMind

```
sudo add-apt-repository ppa:webupd8team/java
sudo apt update && sudo apt install -y oracle-java8-set-default
```

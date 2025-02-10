Setup
=====

Requirements
------------

Install the requirements with `winget`.

### Git

Install git.

```shell
winget install --exact --id Git.Git
```

### Chocolatey

Install Chocolatey (choco) - this is optional.

```shell
# Start powershell as admin
>  Start-Process powershell -Verb runAs
>  Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))


# Install Nerd Fonts
>  choco --version
>  choco feature enable -n allowGlobalConfirmation
>  choco install nerd-fonts-hack

```

### Python 3

Install Python 3.13.

```shell
winget install --exact --id Python.Python.3.13 --custom "PrependPath=1 Include_doc=0"
```

Install pipx.

```shell
pip3 install pipx
# %AppData% - C:\Users\{username}\AppData\Roaming
cd $Env:AppData
cd Python\Python313\Scripts
.\pipx.exe ensurepath
```

### Ansible

Install Ansible with pipx.

```shell
pipx install ansible-core
```

### WSL

Install WSL 2.

```powershell
# Start powershell as admin
>  Start-Process powershell -Verb runAs

# Enable WSL feature
>  dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

# Enable Virtual Machine Platform feature
>  dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

# Set WSL default version to v2
>  wsl --set-default-version 2
```

### Install Ubuntu WSL

```powershell
# List all WSL images available
>  wsl --list --online

# List all installed images
>  wsl --list --verbose

# Install Ubuntu 24.04 LTS
>  wsl --install Ubuntu-24.04 --web-download

# Set Ubuntu 24.04 to default
>  wsl --set-default Ubuntu-24.04
```

### Upgrade Ubuntu

```bash
touch ~/.hushlogin

sudo apt update
sudo apt full-upgrade
```

### Set up Ubuntu

Install lsDeluxe

```bash
sudo apt install lsd
```

Create some symbolic links for convenience

```bash
ln -s /mnt/c ~/C
ln -s /mnt/d ~/D
ln -s '/mnt/c/Users/Dev' ~/Dev
```

### Python and pip

```bash
python3 --version
>>> 3.12.1

sudo apt install python3-pip
sudo apt install libffi-dev libssl-dev openssh-client
which pip
pip --version

sudo apt install pipx
```

### Restart WSL

```powershell
> wsl --shutdown
> wsl
```

### Install Ansible

```bash
pipx install --include-deps ansible
pipx ensurepath
logout  # CTRL+D

> wsl

ansible --version
ansible-community --version
```


### Configure Ansible

```bash
# Create .ansible.cfg
cd ~
echo -e "[defaults]\ninventory = ~/.ansible-hosts" > .ansible.cfg

# Create .ansible-hosts (previously was named hosts.yml)
cd ~
echo -e "localhost ansible_connection=local" > .ansible-hosts

```

source ~/.venv/bin/activate


ANSIball = ansible
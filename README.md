# Kickstart for .NET dev on a Mac
New dev machine? Start here

## Setting up your environment
- Rename your laptop:
    ```shell
    sudo scutil --set HostName <DesiredName>
    sudo scutil --set LocalHostName <DesiredName>
    sudo scutil --set ComputerName <DesiredName>
    dscacheutil -flushcache
    ```
- Install Homebrew
    ```shell
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    touch ~/.zprofile
    echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
    eval "$(/opt/homebrew/bin/brew shellenv)"
    brew update
    brew upgrade
    echo 'export PATH=/usr/local/bin:$PATH' >> ~/.zshrc
    echo 'export PATH=/opt/homebrew/bin:$PATH' >> ~/.zshrc
    echo 'export PATH=/opt/homebrew/sbin:$PATH' >> ~/.zshrc
    ```
- Setup your Git config
    ```shell
    git config --global user.name "FirstName LastName"
    git config --global user.email "first.last@example.com"
    git config --global core.editor "code --wait"
    git config --global pull.rebase true
    git config --global init.defaultBranch main
    ```
- Install [Oh My Zsh](https://ohmyz.sh/)
  ```shell
  sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
  ```
- Enable the ability to install fonts from Homebrew
  ```shell
  brew install --cask font-hack-nerd-font
  brew install --cask font-meslo-lg-nerd-font
  brew install --case font-jetbrainsmono-nerd-font
  brew install --case font-mononoki-nerd-font
  brew install --case font-roboto-mono
  brew install --case font-ubuntu-mono-nerd-font
  ```
  Alternately, you can install all of the fonts (not advised):
  ```shell
  brew search '/font-.*-nerd-font/' | awk '{ print $1 }' | xargs -I{} brew install --cask {} || true
  ```
- Install Powerlevel10k
  ```shell
  git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
  ```
  Set `ZSH_THEME="powerlevel10k/powerlevel10k"` in ~/.zshrc.
  Run `exec zsh` to trigger the install process. Here are the typical install options used:
  - Rainbow
  - Unicode
  - 24-hour format
  - vertical
  - flat
  - flat
  - Two Lines
  - Disconnected
  - No Frame
  - Sparse
  - Few Icons
  - Fluent
  - No Transient Prompt
  - Verbose
  - Apply Changes
- Configure Powerlevel10K
  ```shell
  p10k configure
  ```
- Install .NET 8:
    ```shell
    brew install --cask dotnet-sdk
    dotnet --version
    ```
- Install mkcert
    ```shell
    brew install mkcert
    brew install nss # for Firefox
    mkcert -install #installs a root CA
    ```
- Install DNS Masq which will make it so you _never_ have to touch your local `/etc/hosts/` file again.
    ```shell
    brew install dnsmasq
    mkdir -pv $(brew --prefix)/etc/ # create the config directory
    echo 'address=/.test/127.0.0.1' >> $(brew --prefix)/etc/dnsmasq.conf # setup *.test aliases
    echo 'port=53' >> $(brew --prefix)/etc/dnsmasq.conf # Change port for High Sierra
    # Autostart - now and after reboot
    sudo brew services start dnsmasq
    # Create resolver directory
    sudo mkdir -v /etc/resolver
    # Add your nameserver to resolvers
    sudo bash -c 'echo "nameserver 127.0.0.1" > /etc/resolver/test'
    ```
  You can run scutil --dns to show all of your current resolvers, and you should see that all requests for a domain ending in .test will go to the DNS server at 127.0.0.1
- Install Chrome
    - Sign into your Google work account
- Install Obsidian (Markdown reader):
  ```shell
  brew install obsidian
  ```
- Install [Docker Desktop](https://docs.docker.com/desktop/install/mac-install/) (don’t use brew - that is the CLI only)
- Install Rider
    ```shell
    brew install --cask rider
    ```
    _Note_: VSCode does not play nicely with .NET projects because why would a Microsoft technology work properly with VSCode??
- Login to your [Github.com](http://Github.com) account and [setup an SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent). You can use your personal account as long as it was invited to the GitHub repo.

---
layout: post
title: "oh-my-zsh Setup"
date: 2022-01-26 09:30:00 +0800
categories: note
tags: [zsh, oh-my-zsh, terminal]
---

## Result  
![result_pic](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/oh_my_zsh_res.png?raw=true)  
(using [Tabby](https://tabby.sh/) terminal)

## Setup steps  
1. update OS
    ``` console
    $ sudo apt-get update
    $ sudo apt-get upgrade
    ```
2. install zsh
    ``` console
    $ sudo apt-get install -y zsh

    // check zsh is installed.
    $ cat /etc/shells

    // change default shell
    $ chsh -s $(which zsh)
    ```

3. install [oh-my-zsh](https://github.com/ohmyzsh/ohmyzsh)
    ``` console
    $ sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
    ```
4. install [powerlevel10k](https://github.com/romkatv/powerlevel10k)
    ``` console
    $ git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

    // modify ~/.zshrc to change theme
    // ZSH_THEME="powerlevel10k/powerlevel10k"
    $ vi ~/.zshrc
    ```

5. install proper font for terminal
- [MesloLGS NF Regular.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Regular.ttf)
- [MesloLGS NF Bold.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold.ttf)
- [MesloLGS NF Italic.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Italic.ttf)
- [MesloLGS NF Bold Italic.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold%20Italic.ttf)

6. Active and config theme
    ``` console
    source ~/.zshrc
    ```

7. install zsh useful plugins
- [zsh-completions](https://github.com/zsh-users/zsh-completions)
- [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
- [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)

8. Active plugins
    ``` console
    source ~/.zshrc
    ```
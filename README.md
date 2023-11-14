# Guia de Configuração do Ambiente

Este guia fornece instruções passo a passo para configurar um ambiente de desenvolvimento com Tmux, Zsh, Neovim, Node.js, TypeScript, Rust e Nvchad.

## Instalar Dependências Básicas
```
sudo apt-get update
sudo apt-get install automake libevent-dev libncurses-dev build-essential pkg-config bison ninja-build gettext libtool libtool-bin autoconf automake cmake lldb g++ pkg-config unzip zsh pass bat fzf zoxide mc
```
## Configurar o Tmux
```
git clone https://github.com/tmux/tmux.git
cd tmux
git checkout 3.3a
sh autogen.sh
./configure && make

# Instalar o Plugin Manager do Tmux
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm

# Remover arquivos temporários do tmux
cd ..
rm -rf tmux

# Configurar o arquivo .tmux.conf
git clone https://github.com/oMatheusmol/tmux
mv tmux/tmux.conf ~/.tmux.conf
rm -rf tmux
```

## Configurar o Zsh
```
chsh -s $(which zsh)

# Instalar Oh My Zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

## Instalar Plugins para Zsh
```
git clone https://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions

git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/.powerlevel10k

git clone https://github.com/oMatheusmol/zsh
mv zsh/.zshrc ~/.zshrc
rm -rf zsh
source ~/.zshrc
```

## Configurar o Nvim (Neovim)
```
# Instalar Neovim
git clone https://github.com/neovim/neovim.git
cd neovim
git checkout tags/v0.9.4 -b mybranch
make
sudo make install
cd ..
rm -rf neovim
```

## Configurar o NVM (Node Version Manager)
```
# Instalar NVM
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
source ~/.zshrc

# Instalar Node.js e TypeScript
nvm install node
nvm alias default node
npm install -g typescript
npm install -g ts-node
```

### No node é preciso installar @types/node e criar o arquivo eslintrc

```
npm install --save-dev @types/node
npm init @eslint/config
```

## Configurar o Rust
```
# Instalar Rust
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
export PATH="$HOME/.cargo/bin:$PATH"
source $HOME/.cargo/env
```
### Conferir se o lldb-vscode esta installado com este nome
```
which lldb-vscode
```
Caso não apareca nada certifique-se de renomear para lldb-vscode
```
/usr/bin
sudo mv lldb-vscode-14 lldb-vscode
```
Substituir 14 pelo numero da versão instalada

## Git config
```
git config --global user.name "name"
git config --global user.email "e@e.com"
```

## Configurar o GPG Pass
Gerar chave GPG:
```
gpg --gen-key
```
Inicializar o GPG Pass com {UID} substituído pelo ID do usuário:
```
pass init {UID}
```
Inicializar um repositório Git para o GPG Pass e insere uma senha no GPG Pass
```
pass git init
pass insert api/chatgpt
```
Para Decriptar a chave
```
pass show api/chatgpt >> /dev/null
```

## Configurar o Nvchad (Configuração do Neovim)
```
mv ~/.config/nvim ~/.config/nvim.backup # Apenas se necessário, se você já tinha uma configuração anterior
rm -rf ~/.local/share/nvim
git clone https://github.com/NvChad/NvChad ~/.config/nvim --depth 1 && nvim
```

## Source Configuração
```
source ~/.zshrc
tmux
```

## Atualizar Tmux
```
tmux source ~/.tmux.conf
```

## Atualizar Plugins do Tmux
No Tmux, use o seguinte comando:
```
<Prefix> + I
```
I maiúsculo, Prefix default é (Cntrl + b)

## Mover Configuração do Nvchad para a Pasta Custom
```
cd ~/.config/nvim/lua
rm -rf custom
# Clonar o repositório nvchad
git clone https://github.com/oMatheusmol/nvchad.git custom
cd custom
cd ~/
```
### (Opcional) Remover a pasta .git
```
rm -rf ~/.config/nvim/lua/custom/.git
```

## Install python venv package
```
sudo apt install python3.10-venv
```

## Dentro do Neovim: Instalar Plugins Adicionais
Abra o Neovim:
```
vim
```
###Execute os seguintes comandos para instalar plugins adicionais:
```
:MasonInstall
```
### Instalar python tree
```
:TSInstall python
```
###Configurar o Copilot
```
:Copilot setup
```




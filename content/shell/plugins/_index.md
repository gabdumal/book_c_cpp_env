+++
  title = "Plugin"
  type = "page"
  weight = 4
+++

Plugins são uma forma de estender as funcionalidades do shell.
Para os sistemas que configuramos com o **Zsh**, utilizaremos o **Oh My Zsh**
Já para o **PowerShell**, instalaremos os plugins diretamente.

## Zoxide

O [**Zoxide**](https://github.com/ajeetdsouza/zoxide) é um plugin que facilita a navegação entre diretórios.

Por exemplo, imagine que você tenha um diretório chamado `~/Documents/Projects/MyProject`, que voê frequentemente acessa.

Ter que digitar esse caminho toda vez que quiser acessar esse diretório pode ser um pouco cansativo.
O Zoxide permite que você navegue para esse diretório apenas digitando `cd MyProject`.

Isso é possível porque o Zoxide mantém um histórico dos diretórios que você acessa com mais frequência.
E então, quando você digita `cd MyProject`, ele automaticamente navega para o diretório `~/Documents/Projects/MyProject`.

O Zoxide tem como dependência o [**FZF**](https://github.com/junegunn/fzf), que é um fuzzy finder.
Ele é uma ferramenta que permite que você pesquise por arquivos e diretórios de forma rápida e eficiente.
Vamos tratar da sua instalação adiante.

### PowerShell

Para instalar o FZF no PowerShell, execute o seguinte comando:

```powershell
winget install fzf
```

E então, instale o Zoxide com o seguinte comando:

```powershell
winget install ajeetdsouza.zoxide
```

<figure>
<img src="./installing_zoxide_powershell.png" />
<figcaption>Instalando o FZF e o Zoxide no PowerShell.</figcaption>
</figure>

Então, precisamos adicionar as seguintes linhas ao **final** do seu arquivo de configuração do PowerShell:

```powershell
## Plugins

### Zoxide
Invoke-Expression (& { (zoxide init --cmd cd powershell | Out-String) })
```

Lembre-se que, para abrir o arquivo de configuração do PowerShell, você deve executar o comando `code $PROFILE` no terminal.
O arquivo aberto dependerá da versão do PowerShell que você está utilizando.

<figure>
<img src="./configuring_zoxide_powershell.png" />
<figcaption>Configurando o Zoxide no PowerShell.</figcaption>
</figure>

Salve o arquivo, feche o editor, e então **feche** e abra novamente o PowerShell para que as alterações tenham efeito.

### Zsh

Para instalar o FZF no Zsh, execute os seguintes comandos:

```bash
mkdir -p ~/Downloads
git clone --depth 1 https://github.com/junegunn/fzf.git ~/Downloads/.fzf
~/Downloads/.fzf/install
```

Quando perguntado sobre ativar os recursos do FZF, pressione a tecla <kbd>y</kbd> e então pressione <kbd>Enter</kbd> para cada.

<figure>
<img src="./installing_fzf_zsh.png" />
<figcaption>Instalando o FZF no Zsh.</figcaption>
</figure>

Para instalar o Zoxide, execute o seguinte comando:

```bash
curl -sSfL https://raw.githubusercontent.com/ajeetdsouza/zoxide/main/install.sh | sh
```

<figure>
<img src="./installing_zoxide_zsh.png" />
<figcaption>Instalando o Zoxide no Zsh.</figcaption>
</figure>

Possivelmente, o FZF editou seu arquivo de configuração do Zsh.
Vamos excluir a linha que ele adicionou.
Então devemos mover o bloco `Plugins` para o final do arquivo, e adicionar as seguintes linhas:

```bash
### FZF
[ -f ~/.fzf.zsh ] && source ~/.fzf.zsh
source <(fzf --zsh)

### Zoxide
eval "$(zoxide init --cmd cd zsh)"
```

O arquivo de configuração do Zsh deve ficar assim:

```bash
# Path to your Oh My Zsh installation.
export ZSH="$HOME/.oh-my-zsh"

# Shell configuration
ZSH_THEME="robbyrussell"

## User configuration
PATH=$PATH:~/.local/bin

## Source Oh my Zsh
source $ZSH/oh-my-zsh.sh

## Theme
eval "$(starship init zsh)"
export STARSHIP_CONFIG="$HOME/.config/starship.toml"

## Plugins
plugins=(git)

### FZF
[ -f ~/.fzf.zsh ] && source ~/.fzf.zsh
source <(fzf --zsh)

### Zoxide
eval "$(zoxide init --cmd cd zsh)"
```

Salve o arquivo, feche o editor, e então **feche** e abra novamente o terminal para que as alterações tenham efeito.

Para testar se a instalação foi bem sucedida, execute os seguintes comandos:

```bash
fzf --version
zoxide --version
```

<figure>
<img src="./checking_zoxide_zsh.png" />
<figcaption>Verificando as versões do FZF e do Zoxide no Zsh.</figcaption>
</figure>

<!--
TODO: Ensinar a instalar o The Fuck, considerando que ele exige instalar o Python.

## The Fuck

Primeiramente, perdoem-me o palavreado.
Mas sabe quando você digita um comando enorme, mas percebe só depois de executar que errou uma coisinha só?
O tempo todo eu esqueço de adicionar o `sudo` na frente dos comandos.

Pensando nisso, foi criado o [**The Fuck**](https://github.com/nvbn/thefuck).
Ele é um plugin que corrige esses pequenos erros nos comandos, sejam uma letra trocada, ou todo um atributo esquecido.

Quando receber um erro, digite `fuck`, e o plugin tentará corrigi-lo para você.

### Dependências

Como dependências, o The Fuck exige que se tenha instalado:

- python (3.5+)
- pip
- python-dev -->

## Zsh Autosuggestions

O [**Zsh Autosuggestions**](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh) é um plugin que sugere comandos enquanto você digita.
Isso é especialmente útil quando você se lembra de parte de um comando, mas não dele todo.

Esse plugin está disponível apenas para o Zsh --- sinto muito, pessoal do PowerShell 😔.
O Zsh Autosuggestions pode ser habilitado por meio do **Oh My Zsh**.

Para isso, devemos clonar o repositório do plugin para a pasta de plugins do Oh My Zsh.
Faça isso executando o seguinte comando:

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

Então, vamos editar o arquivo de configuração do Zsh para habilitar o plugin.
Fazemos isso adicionando mais uma linha ao atributo `plugins`, em que havia apenas o `git`.

```bash
## Plugins
plugins=(
    git
    zsh-autosuggestions
)
```

Lembre-se de salvar o arquivo, fechar o editor, e então **fechar** e abrir novamente o terminal para que as alterações tenham efeito.

## Zsh Syntax Highlighting

O [**Zsh Syntax Highlighting**](https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md#oh-my-zsh) é um plugin que destaca comandos enquanto você digita.

Ele também está disponível apenas para o Zsh, e pode ser habilitado por meio do **Oh My Zsh**.

Para isso, devemos clonar o repositório do plugin para a pasta de plugins do Oh My Zsh.
Faça isso executando o seguinte comando:

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

Então, vamos editar o arquivo de configuração do Zsh para habilitar o plugin.
Da mesma forma, basta adicionar a linha `zsh-syntax-highlighting` ao atributo `plugins`.

```bash
## Plugins
plugins=(
    git
    zsh-autosuggestions
    zsh-syntax-highlighting
)
```

<figure>
<img src="./configuring_zsh_plugins.png" />
<figcaption>Configurando os plugins Zsh Autosuggestions e Zsh Syntax Highlighting.</figcaption>
</figure>

Como sempre, salve o arquivo, feche o editor, e então **feche** e abra novamente o terminal para que as alterações tenham efeito.

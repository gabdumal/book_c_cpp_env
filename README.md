# Configuração de ambiente Windows para desenvolvimento em C e C++ utilizando MSYS2

> [Gabriel Malosto](https://github.com/gabdumal), 2024

Este guia pretende auxiliar a configurar uma máquina Windows para desenvolvimento de software em C e C++.

## Editor de texto

A fim de escrever código, você precisará de um editor de texto apropriado.
É interessante que ele seja voltado para o desenvolvimento de software, com funcionalidades como _syntax highlighting_, _code completion_, _debugging_, etc.

O **Visual Studio Code** é um editor de texto muito popular entre desenvolvedores.
Ele é leve, rápido e possui uma grande quantidade de extensões que facilitam o desenvolvimento de software.
Você pode fazer seu download em [https://code.visualstudio.com/](https://code.visualstudio.com/).
Execute o instalador e siga as instruções.

## Ambientes do MSYS2

O **MSYS2** é um ambiente de desenvolvimento que fornece um shell tipo bash, pacotes de software e ferramentas de compilação.

Ele habilita um ambiente Unix-like no Windows.
O Linux é um exemplo de sistema operacional Unix-like, que é muito utilizado para desenvolvimento de software.
Mas perceba que o MSYS2 não é um emulador de Linux, ele apenas oferece um ambiente de desenvolvimento similar ao Linux, que facilita a instalação de ferramentas.

Faça o download do instalador do MSYS2 em [https://www.msys2.org/](https://www.msys2.org/).\
Execute o instalador e siga as instruções.
Durante a instalação, você pode escolher o diretório de instalação, mas o padrão é `C:\msys64`.

O MSYS fornece vários ambientes de desenvolvimento, como explicado pela [documentação oficial](https://www.msys2.org/docs/environments/).
O que vamos usar é o MSYS2 **Clang64**, que é um ambiente de desenvolvimento baseado no Clang e no LLVM.

**Clang** é um compilador C, C++, Objective-C e Objective-C++ de código aberto, que é parte do projeto LLVM. Outro compilador muito conhecido é o _GCC_.
Já **LLVM** é uma infraestrutura de compilador que é usada para construir compiladores para várias linguagens de programação.

No MSYS2, cada ambiente tem suas próprias ferramentas de compilação e bibliotecas.
Ao instalar um pacote voltado para compilação, devemos selecionar sempre aquele que é prefixado com o nome do ambiente que estamos utilizando.

Isto se dá pois o MSYS2 apenas instalará os programas na pasta correspondente ao ambiente selecionado.
Por exemplo, se você instalar o pacote `clang` no ambiente `MSYS2 CLANG64`, ele será instalado em `C:\msys64\clang64`.

Apesar dessa divisão, os pacotes **não vêm** instalados por padrão.
Vamos aprender a fazer isso mais adiante.

## Mintty

Após a instalação, abra o programa **MSYS2 CLANG64**, disponível no menu Iniciar.

Ele abre o emulador de **terminal** padrão do MSYS2, que é o **Mintty**, que é baseado no terminal _xterm_.
Um emulador de terminal é um programa que permite que você interaja com o computador por meio de comandos de texto.

Essa interação é feita por meio de um **shell**, que é um programa que interpreta comandos e executa programas.
O shell padrão do MSYS2 é o **bash**, que é muito popular no Linux.

Dentro do Mintty, nós podemos executar comandos específicos do MSYS2.
Ele é um ambiente **Unix-like**, então muitos comandos são similares aos do Linux.
Por exemplo, para listar os arquivos de um diretório, usamos o comando `ls`.

## Atualização dos pacotes

O MSYS2 disponibiliza um gerenciador de pacotes chamado **pacman**.
Ele é usado para instalar, atualizar e remover pacotes de software.

Primeiramente, vamos atualizar o banco de dados de **pacotes** do MSYS2.
Execute o comando abaixo no terminal Mintty:

```bash
pacman -Syu
```

O shell perguntará se você deseja proceder com o processo.
Digite `Y` e pressione `Enter`.

Ao concluir, ele o pedirá para reiniciar o MSYS2.
Novamente, digite `Y` e pressione `Enter`.

Abra o MSYS2 CLANG64 novamente.
Agora vamos de fato **baixar** os pacotes atualizados.
Antes, havíamos apenas buscado as informações sobre os pacotes disponíveis.
Digite o comando abaixo:

```bash
pacman -Su
```

Confirme a instalação dos pacotes digitando `Y` e pressionando `Enter`.

## Estrutura de diretórios

O MSYS2 cria uma pasta no seu disco `C:` chamada `msys64`.
Ela simula um ambiente Unix-like, com diretórios como `/bin`, `/home`, `/usr`, etc.

Além disso, é neste diretório que você encontrará os executáveis de cada ambiente disponibilizado pelo MSYS2.
Lembre-se: estamos utilizando o CLANG64, mas há outros ambientes disponíveis, caso você precise.

O diretório `/home` cria uma pasta para cada usuário do subsistema MSYS2.
Inicialmente, você verá apenas uma pasta dentro dela, que é o seu usuário do Windows.
Vamos nos referir a ele como `[username]`.
Então, o caminho completo para a pasta do seu usuário é `C:\msys64\home\[username]`.

Dentro dessa pasta, ficarão todos os arquivos de configuração do shell e de outros programas que você virá a instalar no MSYS2.

Além disso, todos os arquivos que você queira usar dentro do MSYS2, incluindo projetos que você queira desenvolver, devem ser colocados dentro de `/home/[username]`.

Todas vez que você inicia o MSYS2 CLANG64, ele abre o terminal Mintty no diretório `/home/[username]`.
Por enquanto, há apenas os arquivos de configuração do shell.
Você pode listá-los com o comando `ls --all`.

Para ajudar na organização, vamos criar um diretório chamado `dev` dentro de `/home/[username]`.
Dentro dele, você pode colocar todos os seus projetos de desenvolvimento.

```bash
mkdir ~/dev
```

Esse `~` é um atalho de linha de comando, que representa o caminho até seu diretório `/home/[username]`.
Você pode usá-lo para se referir a este diretório em qualquer lugar do subsistema MSYS2.

Se você listar o conteúdo do diretório novamente, verá que o diretório `dev` foi criado.
O comando `ls` lista o conteúdo de um diretório, e o argumento `--all` (executado como `ls --all`) faz com que ele liste todos os arquivos, incluindo os ocultos.

### Link simbólico

Acessar essa pasta pelo Windows Explorer pode ser um pouco trabalhoso, além de arriscar perder os arquivos caso você venha a desinstalar o MSYS2.

Em vez de criar uma nova pasta dentro do MSYS2, você pode, na verdade, criar uma pasta comum no Windows, e definir um "atalho" para ela dentro do MSYS2, o que é chamado de **link simbólico**.

Primeiramente, vamos apagar a pasta `dev` que criamos dentro do MSYS2.
Execute o comando abaixo no terminal Mintty.
Ele indica que se deve apagar um diretório e todo o seu conteúdo.

```bash
rm -rf ~/dev
```

Agora, vamos criar uma pasta `dev` no Windows.
Eu escolhi criá-la no diretório `C:\Users\[username]`.
Veja, este diretório `C:\Users\` tem uma função similar ao `/home` do MSYS2, pois é onde ficam os arquivos de cada usuário do Windows.
Apesar disso, são duas pastas completamente diferentes, não as confunda.

Vamos lá, crie normalmente, utilizando o Windows Explorer, uma pasta chamada `dev` no diretório `C:\Users\[username]`, ou seja, `C:\Users\[username]\dev`.

Crie dentro dela um arquivo de texto qualquer, para testarmos o link simbólico.
Chamei o meu de `ola_mundo.txt`.

![Conteúdo do arquivo ola_mundo.txt.](img/ola_mundo.png)

Agora, vamos criar o link simbólico.
Para isso, abra o Prompt de comando do Windows, ou seja, o `cmd`.
Não funciona no terminal do MSYS2 nem no PowerShell.

O comando para criar links simbólicos no Windows é `mklink`.
Ele apresenta diferentes tipos de links.
Vamos utilizar um chamado **junction**, que é um link simbólico de diretório, em que mudanças feitas em um diretório são refletidas no outro, e vice-versa.

No **Prompt de comando do Windows**, execute o comando abaixo, substituindo `[username]` pelo nome da sua pasta de usuário do Windows.

```bash
mklink /J C:\msys64\home\[username]\dev C:\Users\[username]\dev
```

Agora, se você listar o conteúdo do diretório `~/dev` no Mintty, verá que o arquivo `ola_mundo.txt` está lá.
Isso significa que o link simbólico foi criado com sucesso.

Você pode fixar a pasta `dev` no Windows Explorer, para que ela fique sempre visível.
Todas as alterações feitas dentro dela serão refletidas no MSYS2, e vice-versa.

## Instalação do shell ZSH

Vamos trocar o shell do MSYS2 para o **zsh**, que é um shell mais moderno e poderoso que o bash.

Para isso, execute o comando abaixo no terminal do **MSYS2**, para instalar o pacote `zsh`:

```bash
pacman -S zsh
```

Agora precisamos definir o **zsh** como o shell padrão.
Para isso, precisamos definir uma nova variável de ambiente, chamada `SHELL`.
Uma variável de ambiente é um valor que contém alguma informação sobre o ambiente do sistema, e que frequentemente é utilizada por programas.

- Pesquise no menu Iniciar por **Editar as variáveis de ambiente do sistema**.
- Clique em **Variáveis de ambiente**.
- Na janela que abrir, há duas tabelas: `Variáveis de usuário para [username]` e `Variáveis do sistema`.
  - Na tabela de `Variáveis de usuário`, clique em **Novo...**.
    - No campo **Nome da variável**, digite `SHELL`.
    - No campo **Valor da variável**, digite o caminho do executável do zsh, que é `C:\msys64\usr\bin\zsh.exe`.
    - Clique em **OK**.

Aproveitando que estamos aqui, vamos adicionar o diretório do executável do MSYS2 ao **Path**.
O Path é uma variável de ambiente que contém uma lista de diretórios onde o sistema procura por executáveis.

Para que você possa rodar qualquer comando do MSYS2 de qualquer diretório, é necessário adicionar o diretório do executável ao PATH.

- Na tabela de `Variáveis de usuário`, clique em **Path** e depois em **Editar...**.
- Clique em **Novo** e adicione o caminho `C:\msys64\usr\bin`.
- Clique em **OK**.

Agora, feche o terminal atual e abra um novo, ainda do MSYS2 CLANG64.

Você verá uma mensagem de boas-vindas do zsh.
Ele te guiará por um processo de configuração inicial.
Sinta-se à vontade para configurar como desejar.

![Mensagem de boas vindas do Zsh.](img/zsh-welcome.png)

Para navegar pelas opções, você deve digitar o número ou letra correspondente à opção desejada e pressionar `Enter`.
A fim de configurar, pressione `1` e `Enter`.

A seguinte sequência de teclas pode ser usada para fazer uma configuração padrão: `10213041u2s00`.

## Configuração do Windows Terminal

Nós podemos configurar o **Windows Terminal** para abrir no ambiente MSYS2 CLANG64, como mostrado na [documentação oficial](https://www.msys2.org/docs/terminals/).

Para isso, abra o Windows Terminal e acesse as **configurações**.
Na barra inferior, clique em **Abrir o arquivo JSON**.
Este arquivo define todas as configurações do Windows Terminal.
Nós desejamos adicionar um novo perfil para o MSYS2 Clang64.

Encontre a chave `"profiles"`.
Ela contém duas chaves:

- `"defaults"`: define as configurações padrão para todos os perfis.
- `"list"`: contém a lista de perfis, definida pelos colchetes `[]`.
  Cada perfil dentro deles é um objeto JSON que contém várias configurações, como nome, ícone, fonte, esquema de cores, etc.

Abaixo definimos um novo perfil, chamado `CLANG64 / MSYS2`, que abre o MSYS2 Clang64 no diretório do usuário.
Copie **APENAS** o objeto JSON abaixo e cole dentro do array `"list"`.

```json
{
  "guid": "{07b52e3e-de2c-5db4-bd2d-ba144ed6c273}",
  "name": "CLANG64 / MSYS2",
  "commandline": "C:/msys64/msys2_shell.cmd -defterm -here -no-start -clang64 -shell zsh",
  "icon": "C:\\msys64\\clang64.ico",
  "startingDirectory": "C:/msys64/home/%USERNAME%"
}
```

Salve o arquivo e feche o Windows Terminal.

Agora, abra o Windows Terminal novamente e você verá um novo perfil chamado `CLANG64 / MSYS2`.
Clique nele e você abrirá o MSYS2 Clang64 no diretório do usuário.

Você pode definir este perfil como padrão,.
Acesse as **Configurações** do Windows Terminal, clique em **Inicialização** e, no campo **Perfis padrão**, selecione o perfil `CLANG64 / MSYS2`.

Sinta-se à vontade para personalizar o perfil como desejar.

## Instalação do Git

O **Git** é um sistema de controle de versão distribuído.
Ele é muito utilizado para controle de versão de código fonte e colaboração em projetos de software.

O Git é focado em sistemas Unix-like.
Para usá-lo no Windows, é necessário instalar uma versão específica chamada, veja só, **Git for Windows**.
Você pode baixar o instalador pelo site [https://gitforwindows.org/](https://gitforwindows.org/).

Execute o instalador e siga as instruções.
Durante a instalação, você pode escolher o diretório de instalação, mas o padrão é `C:\Program Files\Git`.
Quando perguntado sobre o editor de texto padrão, você pode escolher o **Visual Studio Code**, caso o tenha instalado.

Na sessão **Adjusting the name of the initial branch in new repositories**, você pode escolher o nome da branch padrão.
Recomendo selecionar a opção **Override the default branch name for new repositories** e digitar `main`, uma vez que este é o padrão adotado pelo _GitHub_.

Nas próximas sessões, pode manter as opções padrão, até a **Configuring extra options**, em que recomendo marcar também a caixa **Enable symbolic links**.

O Git for Windows configura automaticamente a Path para seu executável.
De todo modo, caso você tenha problemas, você pode adicionar o diretório do executável do Git ao Path, como fizemos com o MSYS2.

Clique em **Editar...** a variável **Path**.
Dessa vez, adicione duas novas entradas a ela: `C:\Program Files\Git\cmd`, e `C:\Program Files\Git\bin\git.exe`.

Para testar se a instalação foi bem-sucedida, abra o PowerShell e execute o comando:

```bash
git --version
```

Se tudo estiver correto, você verá a versão do Git instalada, como `git version 2.46.0.windows.1`, por exemplo.

### MSYS2 e Git

A Path do Git for Windows não é reconhecida por padrão pelo terminal do MSYS2.
Para resolver isso, nós teremos que editar o arquivo de configuração do zsh.
Ele é um arquivo chamado `.zshrc` e fica no diretório do usuário dentro do subsistema MSYS2. Seu caminho é `C:\msys64\home\[username]`.

Essa pasta guardará vários arquivos de configuração de programas que você utilizará no MSYS2.
Caso você encontre algum problema, é possível que a solução esteja em um desses arquivos.

Abra o arquivo `C:\msys64\home\[username]\.zshrc` com um editor de texto qualquer.
Adicione a linha abaixo ao **final** do arquivo:

```bash
export PATH=$PATH:"/c/Program Files/Git/cmd":"/c/Program Files/Git/bin"
```

Aqui tem um detalhe: o MSYS2, assim como sistemas Unix-like, usa barras normais (`/`) para separar os diretórios.
No Windows, usamos barras invertidas (`\`), como em `C:\Program Files\Git\cmd`.

Além disso, em vez de nomear os discos como `C:`, `D:`, etc., começamos o caminho pelo diretório raiz `/` seguido pela letra do disco em minúsculo.

Salve o arquivo e feche o editor.
**Feche** o terminal atual e abra um novo.
Agora faça o teste do Git novamente.
Se tudo estiver correto, você verá a versão do Git instalada.

O que nós fizemos foi dizer para o shell zsh que ele deve procurar os executáveis do Git nos diretórios `C:\Program Files\Git\cmd` e `C:\Program Files\Git\bin`.
Você pode precisar fazer isso para outros programas que você instalar no MSYS2 no futuro.

## Instalação do Oh My Zsh

Eu disse que o zsh é um shell mais moderno e poderoso que o bash.
Mas ainda não expliquei por quê.
A resposta é que ele é altamente _customizável_ e _extensível_, graças a uma grande quantidade de _plugins_ e _temas_ disponíveis.

O **Oh My Zsh** é um framework para gerenciar a configuração do zsh.
Suas instruções de instalação estão disponíveis no seu [repositório no GitHub](https://github.com/ohmyzsh/ohmyzsh).

Neste link, você encontrará o comando de instalação.
Execute-o no terminal do MSYS2.

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

O Oh My Zsh instalará vários plugins e temas por padrão.
Após a instalação, você verá uma mensagem de boas-vindas do Oh My Zsh.

Infelizmente, ele substituirá o arquivo `.zshrc` dentro da pasta `/home/[username]`, que nós editamos anteriormente.
Mas não se preocupe, o conteúdo do arquivo original será salvo em um arquivo chamado `.zshrc.pre-oh-my-zsh`.

Edite o arquivo `.zshrc` com um editor de texto qualquer.
Copie a seguinte linha e a coloque no **INÍCIO** do arquivo:

```bash
export PATH=$PATH:"/c/Program Files/Git/cmd":"/c/Program Files/Git/bin"
```

O Oh My Zsh depende do Git para funcionar corretamente, então é importante que você o defina no Path logo na **primeira** linha do arquivo.
Caso contrário, você poderá ter problemas ao abrir o terminal.

Como sempre, para atualizar as definições, feche o terminal atual e abra um novo.

## Compilando um programa em C

Ufa, finalmente terminamos as configurações iniciais!
Agora vamos compilar um programa em C para testar se tudo está funcionando corretamente.

Crie um diretório chamado `hello_world` dentro de `~/dev`.
Dentro dele, crie um arquivo chamado `hello_world.c`.

![Comandos executados no Windows Terminal no perfil MSYS2 CLANG64 para criar um arquivo chamado hello_world.c.](img/create_hello_world_project.png)

Abra o arquivo com um editor de texto qualquer e adicione o código abaixo:

```c
#include <stdio.h>

int main() {
    printf("Hello, world!\nThis is my first code in MSYS2.\n");
    return 0;
}
```

Salve o arquivo e volte ao terminal do MSYS2.

### Instalando o compilador

Para compilar o programa, vamos usar o **Clang**.
Lembre-se que incluímos o perfil `CLANG64 / MSYS2` no **Windows Terminal**.
A compilação não funcionará em nenhum outro perfil, nem em outros terminais.

Para instalar pacotes no MSYS2, usamos o `pacman`.
Aqueles voltados para o ambiente CLANG64 são prefixados com `mingw-w64-clang-x86_64-`.
A [documentação oficial](https://www.msys2.org/docs/package-management/) do MSYS2 explica em detalhes como funciona o gerenciamento de pacotes.
Toda a lista de pacotes disponíveis pode ser vista no [repositório do MSYS2](https://packages.msys2.org/).

Vamos instalar o compilador Clang e a ferramenta de compilação Ninja.
Para instalá-los, execute o comando abaixo no terminal do MSYS2:

```bash
pacman -S mingw-w64-clang-x86_64-clang mingw-w64-clang-x86_64-ninja
```

Confirme a instalação digitando `Y` (ou `S`, se estiver em português) e pressionando `Enter`.

O comando de compilação do Clang tem a seguinte estrutura:

```bash
clang [opções] arquivo.c -o arquivo
```

- `[opções]`: são as opções de compilação, como `-c` para compilar sem linkar, `-g` para incluir informações de debug, etc.

- `arquivo.c`: é o arquivo que será compilado.

- `-o arquivo`: é o nome do arquivo de saída.

Assim, com o terminal aberto na pasta `~/dev/hello_world`, execute:

```bash
clang hello_world.c -o hello_world
```

Se tudo estiver correto, você não verá nenhuma mensagem de erro.
Para executar o programa, digite `./hello_world` e pressione `Enter`.

![Comandos executados no terminal do MSYS2 para compilar e executar o programa hello_world.c.](img/compiling_and_running_hello_world_project.png)

## Adicionando o Visual Studio Code à Path

Para criar projetos maiores, é interessante utilizar um ambiente de desenvolvimento integrado (IDE).
Para este guia, vamos utilizar o **Visual Studio Code**.

Há um comando para abrir o Visual Studio Code diretamente no terminal, que é o `code`.
Entretanto, se você tentar executá-lo, verá que ele não é reconhecido pelo MSYS2.
Isso acontece porque o VsCode não está no Path do MSYS2.

Para resolver isso, você pode adicionar o diretório do executável do Visual Studio Code ao Path, como fizemos com o Git.
Mas dessa vez, vamos editar o arquivo diretamente no terminal.

O MSYS2 tem um editor de texto chamado **nano**.
Ele é um editor de texto simples, que pode ser usado diretamente no terminal.

Precisamos abrir o arquivo `.zshrc` para adicionar o diretório do executável do Visual Studio Code ao Path.

Execute o comando abaixo no terminal do MSYS2:

```bash
nano ~/.zshrc
```

Dentro do nano, adicione a linha abaixo logo após o caminho do Git, substituindo `[username]` pelo seu nome de usuário do Windows:

```bash
export PATH=$PATH:"/c/Users/[username]/AppData/Local/Programs/Microsoft VS Code/bin"
```

O arquivo deve ficar como este:

![Editor de texto Nano com o conteúdo do arquivo .zshrc, em que adicionamos o executável do VsCode na Path.](img/adding_vscode_path.png)

Para salvar as alterações, pressione `Ctrl` + `O` e `Enter`.
Para sair do nano, pressione `Ctrl` + `X`.

Em vez de fechar o terminal e abrir um novo, você pode recarregar o arquivo `.zshrc` com o comando `source ~/.zshrc`.

Agora, você pode abrir o Visual Studio Code diretamente do terminal com o comando `code`.

![Comandos executados no terminal do MSYS2 para editar o arquivo de configuração .zshrc, e então abrir o Visual Code Studio.](img/opening_vscode.png)

## Compilando um projeto em C

Disponibilizamos, na pasta `/code` deste repositório, um projetos em C e C++ que você pode utilizar para testar a compilação de código com vários arquivos separados.

Retorne ao diretório `~/dev` e crie um diretório chamado `separate_function`.
Acesse-o e abra o Visual Studio Code com o comando `code .`.

No VsCode, crie um arquivo chamado `main.c` e adicione o código abaixo:

```c
#include <stdio.h>

int sum(int a, int b);

int main() {
    int a = 5, b = 7;
    int result = sum(a, b);
    printf("The sum of %d and %d is %d.\n", a, b, result);
    return 0;
}
```

Crie um arquivo chamado `functions.c` e adicione o código abaixo:

```c
int sum(int a, int b) {
    return a + b;
}
```

A função principal `main` chama a função `sum`, que está definida em outro arquivo.
Então, para fazer a compilação, precisamos passar os dois arquivos para o compilador.
Internamente, o compilador fará a compilação de cada arquivo separadamente e, em seguida, fará a ligação entre eles.

Para compilar o projeto, execute o comando abaixo no terminal do MSYS2.
Perceba que você pode definir o nome do arquivo de saída com a opção `-o` antes dos arquivos de entrada.

```bash
clang -o separate_function main.c functions.c
```

Então, execute o programa com `./separate_function`.

![alt text](img/compiling_and_running_separate_function_project.png)

## Adicionando o MSYS2 à Path

Até então, o Clang está disponível apenas para o terminal do MSYS2.

Entretanto, se o quisermos utilizar em aplicativos do Windows, como o Visual Studio Code, é necessário adicionar o diretório do executável do Clang à Path do Windows.

Para fazer isso, devemos ajustar novamente as variáveis de ambiente do sistema, similar ao que fizemos com o Git.

- Pesquise no menu Iniciar por **Editar as variáveis de ambiente do sistema**.
- Clique em **Variáveis de ambiente**.
- Selecione a variável **Path** na tabela de `Variáveis de usuário para [username]` e clique em **Editar...**.
- Clique em **Novo** e adicione o caminho `C:\msys64\clang64\bin`.
- Clique em **Novo** mais uma vez e adicione o caminho `C:\msys64\usr\bin`.
- Clique em **OK**.

Agora, todos os pacotes que você instalar no ambiente CLANG64 do MSYS2 estarão disponíveis para uso em qualquer aplicativo do Windows.

## Criando projeto em C no Visual Studio Code

O Visual Studio Code é um editor de texto muito poderoso, com várias extensões que facilitam o desenvolvimento de software.

Vamos criar um projeto em C no Visual Studio Code e adicionar extensões que facilitam a compilação e execução do código.

Abra o Ícone de Configurações do Visual Studio Code e clique em **Profiles** (ou Perfis, se estiver em português).

Clique em **New Profile** e o nomeie de MSYS2 Clang64.
Clique em **Create**.
![alt text](img/creating_profile_in_vscode.png)

**Selecione** o perfil, clicando no ícone de "checkmark" do lado do neu nome na lista.
É importante que o perfil correto esteja selecionado para que as configurações sejam aplicadas.

![alt text](img/selecting_profile_in_vscode.png)

### Extensões

Pesquise no menu de **extensões** do Visual Studio Code e instale as seguintes:

- [Git Graph](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph): visualiza o histórico de commits do Git.
- [C/C++](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools): fornece suporte para desenvolvimento em C e C++.

Atenção: ainda **não instale** a extensão `C/C++ Extension Pack`!
Ela inclui outras extensões que serão explicadas mais adiante.

Abra a **paleta de comandos** do Visual Studio Code com `Ctrl` + `Shift` + `P` e pesquise por **Preferences: Open User Settings (JSON)**, ou o equivalente em português.

Copie o conteúdo da pasta [`/config/initial_settings.json`](config/initial_settings.json) deste repositório e cole no arquivo `settings.json` do Visual Studio Code.
Perceba que, abrindo o arquivo `settings.json` quando se usa o perfil MSYS2 Clang64, você verá as configurações específicas para este perfil, e não as configurações gerais do Visual Studio Code.
É este mesmo o objetivo que temos.

A configuração definida no arquivo `settings.json` faz o seguinte:

- O compilador Clang é definido como o compilador padrão.
- Bibliotecas do Clang são incluídas no Path do terminal do Visual Studio Code.
- O terminal integrado do Visual Studio Code é definido como o terminal do MSYS2.

Salve o arquivo e feche o Visual Studio Code.

### Compilando o projeto

Crie um novo diretório chamado `linked_nodes` dentro de `~/dev`.
Acesse-o e abra o Visual Studio Code com o comando `code .`.

Neste repositório, disponibilizamos um projeto em C que simula uma lista encadeada de nós.
Você pode encontrá-lo na pasta [`/code/linked_nodes`](code/linked_nodes) deste repositório.
Copie todos os arquivos para o diretório `linked_nodes` que você criou.

Você verá que o Visual Studio Code já reconhece o projeto e identifica as bibliotecas e funções utilizadas.

Vamos compilar o projeto pelo terminal integrado do Visual Studio Code.
Abra o terminal integrado com `Ctrl` + `` ` `` e execute o comando abaixo:

```bash
clang -o linked_nodes -include node.h main.c node.c
```

Esse comando compila os arquivos `main.c` e `node.c`, incluindo o arquivo de cabeçalho `node.h`, e gera o arquivo executável `linked_nodes`.
Para executar o programa, digite `./linked_nodes` e pressione `Enter`.

![Compilação e execução de um projeto em C pelo terminal integrado do VsCode.](img/compiling_and_running_linked_nodes.png)

## Depurando o projeto

Okay, podemos compilar o projeto pelo terminal do Visual Studio Code.
Mas e se quisermos o fazer por uma interface gráfica?
E se quisermos depurar o código, ou seja, executá-lo passo a passo e inspecionar variáveis?

Primeiramente, vamos instalar o **GDB**, que é um depurador de código para C e C++.
Execute o comando abaixo no terminal do MSYS2 e confirme:

```bash
pacman -S mingw-w64-clang-x86_64-gdb
```

### Compilando pela interface gráfica

Aceite a instalação, e reabra o Visual Studio Code no diretório `linked_nodes`.

Nele, crie uma pasta chamada `.vscode`.
Dentro dela, crie um arquivo chamado `tasks.json` e adicione o conteúdo do arquivo [`/code/linked_nodes/.vscode/tasks.json`](code/linked_nodes/.vscode/tasks.json) deste repositório.

O que ele faz é definir uma tarefa chamada `Clang: build` que compila o projeto com o Clang, incluindo todos os arquivos de cabeçalho e código definidos na raiz do projeto.
O executável gerado terá o nome da pasta aberta no Visual Studio Code.

Você pode executar a tarefa `Clang: build` pressionando `Ctrl` + `Shift` + `B`, ou acessando pela **paleta de Comandos** a opção `Tasks: Run Build Task`.

### Rodando o programa pela interface gráfica

Agora precisamos definir um arquivo de configuração para a depuração do projeto.
Crie um arquivo chamado `launch.json` dentro da pasta `.vscode` e adicione o conteúdo do arquivo [`/code/linked_nodes/.vscode/launch.json`](code/linked_nodes/.vscode/launch.json) deste repositório.

Para rodar o programa, abra o arquivo `main.c` e clique na setinha ao lado do botão de **play** localizado no canto superior direito da janela.
Seleciona a opção "Debug C/C++ file".

![Imagem da porção superior direita da janela do VsCode com a extensão C/C++ habilitada, que mostra ícones de ação sobre o código.](img/start_debugging_in_vscode.png)

O Visual Studio Code compilará pedirá para você selecionar a tarefa de depuração.
Selecione **GDB: build and launch**.

![pop-up do VsCode pedindo para selecionar uma tarefa de depuração. A selecionada é GDB: build and launch.](img/select_debug_task_in_vscode.png)

Essa ação executará a tarefa que definimos no arquivo `tasks.json` e gerará o executável `linked_nodes` na pasta do projeto.
Em seguida, abrirá o depurador em um terminal separado.

Caso você coloque um ponto de interrupção no código, o programa será executado até que aquela linha seja atingida.
Quando o depurador pausa, você pode inspecionar variáveis, ver o valor de ponteiros, e utilizar outras ferramentas que o sistema de depuração oferece.

![Visualização de depuração sendo feita no Visual Studio Code.](img/debugging_in_vscode.png)

#### Configurações globais

Felizmente, o Visual Studio Code permite que você salve as configurações de compilação e depuração em arquivos globais, para serem utilizadas em outros projetos.

Para salvar o `launch.json`, você deve criar uma nova entrada no arquivo `settings.json` do Visual Studio Code, chamada `launch`.
Dentro dela, voê pode definir todas as configurações de depuração que você deseja que sejam globais.
Disponibilizamos uma versão atualizada do arquivo `settings.json` em [`/config/debug_settings.json`](config/debug_settings.json), que inclui a configuração global de depuração.

Para as tarefas de compilação, você deve abrir a **paleta de comandos** do Visual Studio Code e pesquisar por **Tasks: Open User Tasks (JSON)**.
Então, selecione **Other** e cole o conteúdo do arquivo [`/config/initial_debug_tasks.json`](config/initial_debug_tasks.json) deste repositório.

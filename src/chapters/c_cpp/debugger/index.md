# Depurador

O depurador é uma ferramenta que permite que você execute um programa passo a passo, inspecionando variáveis e observando o fluxo de execução.
Isso é útil para encontrar bugs e entender o comportamento do programa.

Você pode já ter utilizado o depurador [**GDB**](https://www.sourceware.org/gdb/) (GNU Debugger).
Ele é do mesmo projeto do GCC (GNU Compiler Collection).

Apesar de ser comumente utilizado para depurar códigos em C e C++, o GDB, além de outros depuradores, podem suportar outras linguagens.
Isso depende da forma como o compilador gera o código objeto e provê informações de depuração.

Então percebemos que, para o depurador funcionar, ele deve ser compatível com o compilador que gerou o binário.

Uma vez que estamos utilizando o compilador **Clang**, escolheremos o depurador [**LLDB**](https://lldb.llvm.org/) (LLVM Debugger), que também é parte do projeto LLVM.

O LLDB depende de ter instalado o Python.
Em sistemas Linux (incluindo WSL), ao fazer a instalação do LLDB, todas as dependências são resolvidas e instaladas.
Já para o Windows, cada dependência deve ser manualmente instalada previamente.

## Linux

<!-- TODO -->

## Windows

Para instalar o **LLDB** no Windows, é necessário ter instalado o **Python 3.10**.
Leia o capítulo sobre a linguagem [**Python**](/src/chapters/python/index.md) para saber como instalá-la.

### LLVM

Instalar o LLVM no Windows é um pouco mais complicado do que no Linux.
A forma mais fácil de fazê-lo é baixar o instalador do projeto **LLVM** do [repositório oficial](https://github.com/llvm/llvm-project).

A fim de evitar problemas de compatibilidade de versões, recomendo instalar a versão mais recente na data de escrita deste livro.
Assim, eu lhes garanto que o processo de instalação funcionará com o Python 3.10.

Acesse a página de [**downloads do LLVM**](https://github.com/llvm/llvm-project/releases/tag/llvmorg-19.1.2) na versão 19.1.2 e baixe o arquivo `LLVM-19.1.2-win64.exe`.

<figure>
<img src="./llvm_download_options.png" />
<figcaption>Opções de download do LLVM.</figcaption>
</figure>

Então, execute o instalador e siga as instruções.
Na página **Install Options**, selecione a opção **Add LLVM to the system PATH for all users**.
Então prossiga com a instalação.

<figure>
<img src="./installing_llvm.png" />
<figcaption>Instalador do LLVM na página "Install Options".</figcaption>
</figure>

Para verificar se a instalação foi bem-sucedida, abra uma nova instância do PowerShell e execute o comando `lldb --version`.

<figure>
<img src="./testing_installation.png" />
<figcaption>Verificando se a instalação do LLVM foi bem-sucedida.</figcaption>
</figure>

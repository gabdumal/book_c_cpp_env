+++
  title = "Interpretando um arquivo"
  type = "page"
  weight = 2
+++

O Python é um linguagem interpretada, que executa um arquivo linha por linha.
Dessa forma, não é necessário compilar o código antes de executá-lo.
Basta chamar o interpretador Python e passar o arquivo como argumento.

Eu gosto de organizar meus projetos em uma pasta chamada `dev` na raiz da minha pasta de usuário.
A criação dessa pasta foi tratada no capítulo [Windows Subsystem for Linux](/src/chapters/wsl/_index.md).

## Olá, Mundo

Para os sistemas **Ubuntu** e **Fedora**, basta executar o seguinte comando para criar a pasta `dev`:

```bash
mkdir ~/dev
```

Já para o **Windows**, você pode executar o seguinte comando no PowerShell:

```powershell
mkdir $HOME/dev
```

Então, vamos criar dentro dela uma pasta chamada `python` e um arquivo chamado `hello.py`:

Para os sistemas **Ubuntu**, **Fedora** e **WSL**, execute o seguinte comando:

```bash
mkdir ~/dev/python
```

Já para o **Windows**, execute o seguinte comando no PowerShell:

```powershell
mkdir $HOME/dev/python
```

Por fim, criemos o arquivo `hello.py` dentro da pasta `python`:

```powershell
cd $HOME/dev/python
echo "print('Hello, World!')" > hello.py
```

Para executar o arquivo, basta chamar o interpretador Python e passar o arquivo como argumento:

```powershell
python hello.py
```

<figure>
<img src="./hello.png" />
<figcaption>Execução do script "hello".</figcaption>
</figure>

## Visual Studio Code

Vamos criar um projeto para editar no Visual Studio Code.

Crie uma pasta dentro do diretório `python` recém-criado chamada `hello_person`:

```powershell
mkdir $HOME/dev/python/hello_person
```

Então, abra o Visual Studio Code nessa pasta:

```powershell
code $HOME/dev/python/hello_person
```

Por dentro do VSCode, crie um arquivo chamado `main.py` e adicione o seguinte código:

```python
name = input('Qual é o seu nome? ')
print(f'Olá, {name}!')
```

Abra o terminal do Visual Studio Code e execute o script:

```powershell
python main.py
```

<figure>
<img src="./hello_person.png" />
<figcaption>Execução do script "main" do projeto "hello_person" por dentro do Visual Studio Code.</figcaption>
</figure>

Nós podemos melhor a experiência de desenvolvimento no Visual Studio Code instalando algumas extensões.

### Perfis

Para não misturar definições de linguagens diferentes, vamos utilizar o recurso de **Perfis** do Visual Studio Code.

<figure>
<img src="./opening_profiles.png" />
<figcaption>Abrindo a tela de configuração de perfis do Visual Studio Code.</figcaption>
</figure>

Clique no botão **New Profile**.
Dê o nome de **Python** para o perfil.
Selecione o ícone de _cobra_.
Então, clique em **Create**.

<figure>
<img src="./creating_profile.png" />
<figcaption>Criando perfil para a linguagem Python no Visual Studio Code.</figcaption>
</figure>

Na imagem acima, ignore o espaço em branco na lista de perfis.
Nele, estavam definidos alguns perfis que eu já criei.
A fim de não confundir, apaguei-os na edição.
Para você, a lista terá apenas o perfil **Default**.

Garanta que você definiu que as extensões do perfil **Default** sejam aplicadas para todos os perfis, como mostrado no capítulo [Visual Studio Code](/src/chapters/vscode/_index.md#extensões).

Agora, abra novamente a lista de perfis e selecione o ícone de _check_ na opção **Python**.
Isso aplicará o perfil criado na pasta atualmente aberta no Visual Studio Code.

<figure>
<img src="./selecting_profile.png" />
<figcaption>Selecionando o perfil "Python" no Visual Studio Code.</figcaption>
</figure>

#### Extensões e Configurações padrão

Se você abrir o arquivo de configuração do Visual Studio Code pela paleta de comandos, verá que o arquivo estará vazio.

Isso ocorre porque o Visual Studio Code cria um arquivo de configuração para cada perfil.
Dessa forma, as extensões instaladas e as configurações definidas para um perfil não interferem nos outros.

<figure>
<img src="./empty_settings.png" />
<figcaption>Arquivo de configurações do perfil "Python" no Visual Studio Code.</figcaption>
</figure>

Mas e se eu quiser que certas configurações sejam aplicadas a todos os perfis?
É para isso que definimos, nas configurações do perfil **Default**, o atributo `"workbench.settings.applyToAllProfiles"`.

Ele espera a lista de definições que serão aplicadas a todos os perfis.
Sempre que você definir uma nova configuração no perfil **Default**, lembre-se de adicionar o nome dela nessa lista.

Mas e se eu quiser que certas extensões sejam aplicadas a todos os perfis?
É para isso que definimos, para cada uma das extensões do perfil **Default**, a opção **Apply to all profiles**.

#### Extensões específicas para Python

Agora que entendemos como funcionam os perfis, vamos instalar algumas extensões específicas para a linguagem Python.

Recomendo instalar as seguintes extensões:

- [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python)
- [Python Debugger](https://marketplace.visualstudio.com/items?itemName=ms-python.debugpy)
- [Pylance](https://marketplace.visualstudio.com/items?itemName=ms-python.vscode-pylance)
- [Pyhton Environment Manager](https://marketplace.visualstudio.com/items?itemName=donjayamanne.python-environment-manager)
- [Ruff](https://marketplace.visualstudio.com/items?itemName=charliermarsh.ruff)
- [Even Better TOML](https://marketplace.visualstudio.com/items?itemName=tamasfe.even-better-toml)

#### Configurações específicas para Python

Agora, vamos definir algumas configurações específicas para a linguagem Python.

Copie o conteúdo do arquivo [`settings.json`](settings.json) e cole no arquivo de configuração do perfil **Python**.
Lembre-se de **salvar** o arquivo após a edição.

---

Agora, o Visual Studio Code apresenta uma série de ferramentas para facilitar o desenvolvimento de aplicações em Python.

<figure>
<img src="./workspace.png" />
<figcaption>Visual Studio Code com funcionalidades para o Python.</figcaption>
</figure>

### Executando e depurando

Para executar ou depurar um arquivo pela interface do Visual Studio Code, basta selecionar no botão **Run** na barra lateral, e então clicar no botão **Run and Debug**.

O VSCode pedirá para selecionar o depurador a ser utilizado.
Da lista de opções, escolha **Python Debugger**.

<figure>
<img src="./launch.png" />
<figcaption>Executando o código pela interface do visual Studio Code.</figcaption>
</figure>

Então, o Visual Studio Code abrirá uma lista de opções para como executar o programa.
Nesse caso, escolha **Python File**.

<figure>
<img src="./select_launcher.png" />
<figcaption>Escolhendo como executar o código</figcaption>
</figure>

Por fim, o Visual Studio Code abrirá uma janela de depuração, onde você poderá acompanhar a execução do programa linha por linha.
Para interagir com o programa, utilize o terminal integrado do Visual Studio Code.

<figure>
<img src="./debug.png" />
<figcaption>Depurando o programa pela interface do visual Studio Code.</figcaption>
</figure>

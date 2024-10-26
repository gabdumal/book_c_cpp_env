+++
  title = "Instalação"
  type = "page"
  weight = 1
+++

O Python é instalado por padrão no Ubuntu (e WSL) e no Fedora, bastando verificar se as ferramentas auxiliares estão instaladas.
Já no Windows, é necessário instalar o Python manualmente.

## Linux

<!-- TODO -->

## Windows

Para instalar o Python no Windows, podemos utilizar a ferramenta [**Winget**](https://winget.run/pkg/Python/Python.3.10).

Por motivos de compatibilidade com o **LLVM**, é recomendado instalar a versão 3.10.
Abra o **Powershell** como **administrador** e execute o comando:

```powershell
winget install -e --id Python.Python.3.10
```

<figure>
<img src="./installing.png" />
<figcaption>Instalação do Python para Windows.</figcaption>
</figure>

Para verificar se a instalação foi bem-sucedida, **feche** e abra o **Powershell** novamente, então digite os comandos:

```bash
python --version
pip --version
```

<figure>
<img src="./testing_installation.png" />
<figcaption>Verificando se a instalação do Python foi bem-sucedida.</figcaption>
</figure>

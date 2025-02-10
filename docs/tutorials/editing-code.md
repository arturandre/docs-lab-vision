# Acessando e editando código remotamente

Editar códigos que serão executados em uma máquina remota, como na rede vision, pode ser complicado, ainda mais se forem necessários testes, experimentações ou prototipagem. Executar localmente e enviar o código via git não é produtivo.

## VS Code
O VS Code e outras IDEs modernas permitem acesso de pastas via SSH, agilizando bastante o desenvolvimento. Este tutorial mostra como conectar o VS Code ao servidor da rede e-science, permitindo a edição de arquivos diretamente no servidor e a execução do código sem necessidade de transferências manuais.

### 1. Instalando Remote - SSH e client compátivel

Para realizar a conexão ao servidor, utilizaremos a extensão Remote - SSH da Microsoft. Você pode baixá-la através do seguinte link:

[Remote - SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh)

Feito isso, é necessário instalar um cliente SSH compatível com OpenSSH, para isso, execute:

```bash
sudo apt-get install openssh-client 
```

Agora, já é possível partir para a configuração do vscode. 

### 2. Configurando o VS Code

Verifique que é possível conectar à rede vision pelo terminal usando:

```bash
ssh <user_science>@vision.ime.usp.br
```

Se isso funcionou, no VSCode, pressione ```F1``` ou ```Ctrl+Shift+P```, digite ```Remote-SSH: Connect to Host...```
e aperte enter. Então, digite o mesmo comando acima, ou seja:

```bash
ssh <user_science>@vision.ime.usp.br
```

Agora, o VSCode irá configurar automaticamente todo o necessário. Você estará conectado à rede Vision assim que inserir sua senha na barra superior. No canto inferior esquerdo da tela, você verá algo como ```SSH: vision.ime.usp.br```.

!!! Aviso 
    Isso irá conectá-lo à máquina base do servidor. Para encerrar a sessão, clique no ícone azul no canto inferior esquerdo e selecione 'Close Remote Connection', ou, para mudar de máquina, use o comando ```ssh <nome_da_maquina>```.

### 3. Acessando e editando remotamente

Para abrir um diretório, arquivo ou workspace, você faz exatamente como faria na máquina local:
	
Open Folder > ...
    
ou

File > Open File... > ```arquivo ou diretório```

Após inserir sua senha e se conectar, o VS Code salva o host na barra lateral esquerda, na seção representada por um monitor e um símbolo no canto inferior direito, parecido com '><'. Assim, você pode facilmente se reconectar a qualquer momento. Caso deseje adicionar outros hosts, clique no símbolo de '+' no canto superior da aba e adicione o endereço desejado.

Quando se trabalha com ambientes Python alternativos (como Anaconda, por exemplo), o VS Code oferece uma maneira simples de alternar entre esses ambientes. Para selecionar o ambiente desejado, siga os seguintes passos:

1. Abra o **Command Palette** no VS Code, pressionando ```Ctrl+Shift+P``` ou ```F1```.

2. Digite e selecione a opção "**Python: Create Environment...**" para criar um novo ambiente, ou escolha "**Python: Select Interpreter**" para selecionar um ambiente existente.

A partir desse ponto, o ambiente de desenvolvimento está pronto, podendo compilar e editar códigos diretamente na sua conta e máquina de uso em qualquer terminal aberto.


### ssh tunneling
- altere o arquivo .ssh/config na sua máquina local
- adicione a shell como Host e a máquina que você irá fazer o experimento.
- o tunneling também permite que você acesse a máquina interna diretamente

## Jupyter notebook / Jupyterlab
TODO



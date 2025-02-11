# Acessando e editando código remotamente

Editar códigos que serão executados em uma máquina remota, como na rede e-Science, pode ser complicado, ainda mais se forem necessários testes, experimentações ou prototipagem. Tendo em vista que executar localmente e enviar o código via git não é produtivo, geralmente, ou usamos o VS Code para editar e executar programas diretamente na rede ou editamos e executamos jupyter notebooks na mesma. Por isso, nesta página, segue tanto o tutorial para a edição de programas alocados na rede e-Science a partir do VS Code quanto o tutorial para a configuração e uso de jupyter notebooks na rede.

## VS Code

O VS Code e outras IDEs modernas permitem acesso a pastas via SSH, o que agiliza consideravelmente o desenvolvimento. Este tutorial mostra como conectar o VS Code ao servidor da rede e-Science, permitindo a edição e execução de arquivos diretamente no servidor sem necessidade de transferência de arquivos entre sua máquina local e a rede e-Science.

Vale ressaltar que os comandos deste tutorial para a edição e execução de arquivos a partir do VS Code na rede e-Science devem ser executados em um terminal linux em sua máquina local.

### 1. Instalando Remote - SSH e um cliente SSH compátivel com OpenSSH

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

Se isso funcionou, no VS Code, pressione `F1` ou `Ctrl+Shift+P`, que deve abrir o "Command Palette", digite `Remote-SSH: Connect to Host...` e aperte enter. Então, digite o mesmo comando acima, ou seja:

```bash
ssh <user_science>@vision.ime.usp.br
```

Agora, o VS Code irá configurar automaticamente tudo necessário. Agora, basta inserir sua senha da rede e-Science na barra superior e você estará conectado. No canto inferior esquerdo da tela, você verá algo como ```SSH: vision.ime.usp.br``` assim como segue na imagem:

![Connected machine status](../images_editing-code/ssh:vision.ime.usp.br_vs_code.png)

!!! Aviso 
    Isso irá conectá-lo à máquina base do servidor. Para encerrar a sessão, clique no ícone azul no canto inferior esquerdo e selecione 'Close Remote Connection', ou, para mudar de máquina, use o comando ```ssh <nome_da_maquina>``` no 'Command Palette', que pode ser aberto com `Ctrl + Shift + P` ou `F1`.

### 3. Salvando as conexões a outra(s) máquina(s) 


#### Aba "Remote Explorer"

Tendo em vista que a extensão Remote - SSH foi instalada, a aba 'Remote Explorer' foi adicionada em seu VS Code, como na imagem que segue:

![Connected machines](../images_editing-code/remote_explorer.png)

A partir dela, é possível salvar as conexões estabelecidas a qualquer máquina da rede e-Science.

#### Salvando uma nova conexão

Para salvar uma nova conexão, primeiro, é necessário adicionar a máquina desejada como host no arquivo `config` da pasta `.ssh` assim como é indicado na sessão "Configurando o fácil acesso a máquinas da rede e-Science" na página [Tutorial SSH](./configuring-workplace.md). Posteriormente, basta clicar no ícone "+" como segue na imagem:

![New conection](../images_editing-code/new_ssh_conection_vs_code.png)

digitar `ssh <nome_maquina>` e apertar enter, assim como a sequência de imagens a seguir exemplifica para a conexão à máquina deepten da rede:

![Connecting new machine1](../images_editing-code/new_machine1.png)
![Connecting new machine2](../images_editing-code/new_machine2.png)

Assim, a conexão será salva, de modo que, para se reconectar à máquina pelo VS Code basta seguir o caminho: 

Aba "Remote Explorer" > passar o mouse em cima de `<nome_maquina>` > selecionar "Connect in New Window", assim como em:

![Connecting new machine3](../images_editing-code/new_machine3.png)

### 4. Acessando e editando remotamente

Para abrir um diretório, arquivo ou workspace, você faz exatamente como faria na máquina local:
	
Open Folder > ...
    
ou

File > Open File... > ```arquivo ou diretório```

Quando se trabalha com ambientes Python alternativos (como Anaconda, por exemplo), o VS Code oferece uma maneira simples de alternar entre esses ambientes. Após abrir ou criar um workspace no VS Code, a fim de selecionar o ambiente desejado, siga os seguintes passos:

1. Abra o **Command Palette** no VS Code, pressionando ```Ctrl+Shift+P``` ou ```F1```.

2. Digite e selecione a opção "**Python: Create Environment...**" para criar um novo ambiente, ou escolha "**Python: Select Interpreter**" para selecionar um ambiente existente.

A partir desse ponto, o ambiente de desenvolvimento está pronto, podendo compilar e editar códigos diretamente na sua conta e máquina sendo usada na rede e-Science em qualquer terminal aberto.


### ssh tunneling
- altere o arquivo .ssh/config na sua máquina local
- adicione a shell como Host e a máquina que você irá fazer o experimento.
- o tunneling também permite que você acesse a máquina interna diretamente

## Jupyter notebook / Jupyterlab
TODO



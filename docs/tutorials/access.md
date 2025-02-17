# Acesso à Rede Vision via SSH

A principal forma de acesso às máquina da rede eScience é via ssh. Este texto irá abordar como realizar essa conexão e duas formas de simplificar esse processo, eliminando a necessidade de digitação de senha e realizando conexão direta usando ssh tunneling.

## Acesso à Rede e-Science

A fim de acessar a máquina de entrada da rede e-Science, basta executar o comando a seguir no terminal de sua máquina local:

```bash
ssh <seu_user_science>@vision.ime.usp.br
```

!!! tip "Primeiro Acesso?"
	Se esse for o seu primeiro acesso à rede, conecte em alguma outra máquina diferente da shell, ex: ```ssh tolstoi``` e mude a sua senha usando o ```passwd <nova_senha>```.


!!! info
	Caso esteja realizando o acesso via windows, recomendamos usar o [WSL](https://learn.microsoft.com/pt-br/windows/wsl/).

!!! question
	Caso não tenha o cliente SSH em sua máquina local, instale o [openssh](https://www.openssh.com/manual.html):
	```bash
	sudo apt install openssh-client
	```

## Autorizando o seu acesso através da chave pública

Para acessar a rede e-Science e qualquer uma de suas máquinas sem informar a senha será necessário registrar a sua chave pública nos servidores.

### 1. Criando uma chave SSH

Caso tenha um chave e não deseje sobrescrevê-la pode pular esta etapa.

```bash
ssh-keygen -t rsa
```

Durante a geração da chave, será necessário confirmar o local de salvamento (```~/.ssh/id_rsa```) e definir uma senha — ambos são opcionais e, caso não queira, basta pressionar Enter. Esse processo criará duas chaves: uma privada (```~/.ssh/id_rsa```), usada para autenticar suas conexões, e uma pública (```~/.ssh/id_rsa.pub```), que deve ser copiada para o servidor da Rede e-Science para obter acesso.

### 2. Copiando a chave SSH pública para a Rede e-Science
Há 2 comandos possíveis para se copiar a chave para os servidores, sendo o primeiro:

```bash
ssh-copy-id <user_science>@vision.ime.usp.br
``` 

Após executado o comando acima, será solicitado a senha da sua conta e após isso o acesso estará pronto, mas caso este primeiro comando não funcione, você terá que registrar a sua chave pública manualmente no arquivo authorized_keys com o comando:

```bash
cat ~/.ssh/id_rsa.pub | ssh <user_science>@vision.ime.usp.br "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

Este comando não solicitará sua senha e, após isso, seu acesso à Rede e-Science está pronto! Para se conectar utilize o comando:

```bash
ssh <user_science>@vision.ime.usp.br 
```

E assim, você estará conectado à máquina de entrada.

## Configurando SSH tunneling

Outra configuração que simplifica o acesso é o SSH tunneling. Com essa configuração ativa, você poderá acessar as máquinas diretamente pelo hostname delas, sem precisar explicitar o seu usuário e sem escrever o acesso ssh da Shell para a máquina desejada.

Na prática,
```bash
   ssh <seu_user>@vision.ime.usp.br
   >> prompt senha
   ssh <maquina_qualquer>
   >> prompt senha
```
Vira 
```bash
   ssh <maquina_qualquer>
```

Para realizar essa configuração, você precisa adicionar em sua máquina local em ```~/.ssh/config```
1. O host da máquina de entrada com hostname e seu usuario
2. O host das máquinas que deseja acessar adicionado o ProxyJump com a máquina de entrada.

```
Host labvision
    HostName vision.ime.usp.br
    User <seu_usuario_vision>

Host deepthree
    HostName deepthree
    User <seu_usuario_vision>
    ProxyJump labvision
```

### Gere o seu arquivo de configuração de ssh para ssh tunnelling na vision

Insira abaixo o seu nome de usuário para gerar o arquivo .ssh/config com o seu nome e login para as máquinas deep, cientistas e russas.

Clique no botão copiar ao lado direito do código.

<br>
<input id="userInput" type="text" placeholder="insira seu user vision">
<button class="btn" onclick="computeOutput()">Gerar .ssh/config</button>

<style>
  .btn {
    background-color:rgb(45, 47, 110); 
    color: white;
    border: none;
    padding: 10px 20px;
    font-size: 16px;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s, transform 0.2s;
  }

  .btn:hover {
    background-color:rgb(64, 81, 181);
  }

  .btn:active {
    transform: scale(0.95);
  }
</style>


<pre id="output">
```python
```
</pre>
<br>
<script>
  function computeOutput() {
    // Get the user input.
    const machines = ["deepzero", "deepone", "deeptwo", "deepthree", "deepfour", "deepfive", "deepsix", "deepseven", "deepeight", "deepnine", "deepten", "deepeleven", "deeptwelve", "tolstoi", "dostoievski", "puchkin", "curie", "hopper", "lovelace", "hamilton"];
        var username = document.getElementById("userInput").value;

        let result = "";
        result += `Host labvision\n`;
        result += `    HostName shell.vision.ime.usp.br\n`;
        result += `    User ${username}\n\n`;

        for (const machine of machines) {
            result += `Host ${machine}\n`;
            result += `    HostName ${machine}\n`;
            result += `    User ${username}\n`;
            result += `    ProxyJump labvision\n\n`;
        }

        console.log(result);

    // Display the result.
    document.getElementById("output").querySelector("code").textContent = result;
  }
</script>

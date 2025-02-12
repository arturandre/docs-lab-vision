# Conectando-se à Rede e-Science via SSH

## Acesso à Rede e-Science

A fim de acessar a máquina de entrada da rede e-Science, basta executar o comando a seguir no terminal de sua máquina local:

```bash
ssh <seu_user_science>@vision.ime.usp.br
```
Note, porém, que você deve sempre inserir a senha para conseguir entrar na máquina de acesso, o que se torna cansativo ao longo do tempo. Sendo assim, nessa página, para se conectar ao servidor da Rede e-Science sem precisar informar a senha.

## Acesso à Rede e-Science sem informar a senha

Para acessar a rede e-Science e qualquer uma de suas máquinas sem informar a senha será necessário não só utilizar o protocolo SSH, mas também alocar sua chave SSH pública para ela.

### 1. Instalando o SSH

Caso não tenha o SSH, instale-o com o comando:

```bash
sudo apt install openssh-client
```
Se não tiver certeza se já está instalado, você pode verificar com:

```bash
ssh -V
```
Se aparecer algo como 'command not found', significa que o SSH ainda não está instalado.

### 2. Criando uma chave SSH

Antes de criar uma nova chave, verifique se ja há alguma chave SSH para não sobrescrever suas configurações com o comando:

```bash
ls -al ~/.ssh/id_*.pub
```
Se não houver chave, você verá o seguinte resultado:

```bash
ls: cannot access /home/user/.ssh/id_*.pub: No such file or directory
```

Caso tenha um chave e não deseje sobrescrevê-la pode pular esta etapa.

Para gerar a chave pública SSH, utilize o comando:

```bash
ssh-keygen -t rsa
``` 

Durante a geração da chave, será necessário confirmar o local de salvamento (```~/.ssh/id_rsa```) e definir uma senha — ambos são opcionais e, caso não queira, basta pressionar Enter. Esse processo criará duas chaves: uma privada (```~/.ssh/id_rsa```), usada para autenticar suas conexões, e uma pública (```~/.ssh/id_rsa.pub```), que deve ser copiada para o servidor da Rede e-Science para obter acesso.

### 3. Copiando a chave SSH pública para a Rede e-Science

Há 2 comandos possíveis para se copiar a chave para os servidores, sendo o primeiro:

```bash
ssh-copy-id <user_science>@vision.ime.usp.br
``` 

Após executado o comando acima, será solicitado a senha da sua conta ( aquela enviada por email ) e após isso o acesso estará pronto, mas caso este primeiro comando não funcione utilize:

```bash
cat ~/.ssh/id_rsa.pub | ssh <user_science>@vision.ime.usp.br "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

Este comando não solicitará sua senha e, após isso, seu acesso à Rede e-Science está pronto! Para se conectar utilize o comando:

```bash
ssh <user_science>@vision.ime.usp.br 
```

E assim, você estará conectado à máquina de entrada ( lembre-se que nunca se deve fazer experimentos nela! ).
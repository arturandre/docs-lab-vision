# Instalando e configurando o seu ambiente de trabalho

Para usar e configurar ambientes python, recomendamos baixar e instalar o miniconda.

https://docs.anaconda.com/miniconda/install/#quick-command-line-install


# Configurando seu ambiente de trabalho

Configurar seu ambiente de trabalho corretamente é essencial para aproveitar os recursos do laboratório. Este documento fornece um guia passo a passo para configurações úteis mais comuns.

## Conectando-se à Rede Vision (Acesso ao Servidor via SSH)

Para se conectar ao servidor da Rede Vision, será necessário utilizar o protocolo SSH para o acesso.

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
Isso gerará duas chaves: uma privada (arquivo ```~/.ssh/id_rsa```), usada para autenticar suas conexões, e uma pública (```~/.ssh/id_rsa.pub```), usada para se conectar aos servidores.

Agora, basta copiar a chave para o servidor da Rede Vision para obter acesso.

### 3. Copiando a chave SSH pública para a Rede Vision

Há 2 comandos possíveis para se copiar a chave para os servidores, sendo o primeiro:

```bash
ssh-copy-id <seu_usuario>@vision.ime.usp.br
``` 

Sera solicitado a senha da sua conta ( aquela enviada por email ) e após isso o acesso estará pronto, mas caso o primeiro comando não funcione utilize:

```bash
cat ~/.ssh/id_rsa.pub | ssh <seu_usuario>@vision.ime.usp.br "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

Este comando não solicitará sua senha e, após isso, seu acesso a Rede Vision está pronto! Para se conectar utilize o comando:

```bash
ssh <seu_usuario@vision.ime.usp.br> 
```

E com isso, você estará conectado a máquina de entrada ( aquela que nunca se deve fazer experimentos! ).

### 2. Permissões e acessos
- nível de acesso provido, etc

### 3. Configurando o Arquivo `.bashrc`
- Alias úteis para comandos comuns

### 4. Instalando Python via Miniconda
- O que é Miniconda e por que utilizá-lo
- Baixando e instalando o Miniconda
- Criando ambientes Python para projetos específicos





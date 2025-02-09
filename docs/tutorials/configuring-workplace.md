# Instalando e configurando o seu ambiente de trabalho

Configurar seu ambiente de trabalho corretamente é essencial para aproveitar os recursos do laboratório. Este documento fornece um guia passo a passo para configurações úteis mais comuns.

Para usar e configurar ambientes python, recomendamos baixar e instalar o anaconda, cujo uso e instalação estão explicados nessa página. Ademais, supomos o uso do sistema operacional linux, de modo que, nesse tutorial, todos os comandos foram testados em um terminal linux. Nesta página, encontram-se também os tutorias para o acesso com ssh na rede e-Science e para o acesso sem senha dos computadores desta rede.

## 1. Anaconda 

### O que é anaconda

Anaconda é uma plataforma para se desenvolver projetos em python e R. Assim, dispõe de mais de 7500 pacotes adicionais, que podem ser instalados pelo repositório do Anaconda, fora os 300 pacotes que já vem instalados ao baixá-lo. De forma simples, o Anaconda permite a criação de ambientes de programação diversos e independentes entre si, o que facilita o desenvolvimento de programas que dependem de múltiplos pacotes adicionais. Para conferir mais sobre, recomendamos sua página na wikipedia:

https://en.wikipedia.org/wiki/Anaconda_(Python_distribution)

Para a rede e-Science, temos um interesse especial no Anaconda tendo em vista que o usuário comum, ou seja, um usuário que não seja administrador, não tem acesso ao comando sudo, essencial para instalar pacotes. Sendo assim, ao usar Anaconda, contornamos o problema de não se ter permissão para executar o comando sudo.

### Instalando o anaconda no meu usuário da rede e-Science
Como primeiro passo, baixe, no seu computador, a versão mais recente do anaconda disponível neste repositório:

https://repo.anaconda.com/archive/

O arquivo baixado deve ter um nome parecido com "Anaconda3-2024.10-1-Linux-x86_64.sh".

Instalado esse arquivo, devemos mandá-lo à máquina base da rede e-Science. Para isso,
rode o comando:
```bash
scp <endereço do .sh baixado> <user_science>@vision.ime.usp.br
```
Onde `<user_science>` deve ser substituído pelo nome de seu usuário na rede e-Science e `<endereço .sh>`, pelo endereço do arquivo .sh em sua máquina. Vale ressaltar que será necessário inserir sua senha após rodar o comando, caso não tenha configurado ainda o acesso remoto sem senha, cujo tutorial está disponível na página "Acessando e editando código remotamente", localizada dentro da seção "Tutoriais" desta documentação.

Exemplo: `scp ~/Downloads/Anaconda3-2024.10-1-Linux-x86_64.sh usuario@vision.ime.usp.br`

Após a execução deste comando, o arquivo estará disponível na sua home em qualquer máquina da rede e-Science. Portanto, acesse a máquina base desta rede com o comando:
```bash
ssh <user_science>@vision.ime.usp.br
``` 

Estando na máquina base, devemos, agora, de fato instalar o anaconda. Assim, devemos executar o bash script anteriormente baixado a partir do seguinte comando:

```bash
bash Anaconda3-2024.10-1-Linux-x86_64.sh
```
onde `Anaconda3-2024.10-1-Linux-x86_64.sh` deve ser substituído pelo arquivo baixado.

Executado esse comando, será mostrado os termos de licença do Anaconda. Basta aceitá-los digitando 'yes' quando requisitado e configurar o local de instalação que o anaconda será instalado no seu usuário da rede e-Science.

### Configurando o anaconda no meu usuário da rede e-Science

A fim de configurar o anaconda, será necessário ativá-lo pela primeira vez, o que é feito a partir da execução do seguinte comando:

```bash
eval "$(<local_instalacao_anaconda>/conda shell.YOUR_SHELL_NAME hook)"
```

ou algum comando parecido, que será exibido como orientação do próprio anaconda após sua instalação. Assim, você deve substituir `YOUR_SHELL_NAME` pela palavra `bash` e `local_instalacao_anaconda`, pelo caminho para o local onde foi instalado o anaconda, por padrão, `/home/<user_science>/anaconda3/bin`, de modo que o comando seria algo como:

```bash
eval "$(/home/user1/anaconda3/bin/conda shell.bash hook)"
```


Agora, o conda está ativado no ambiente base e já é possível usá-lo livremente na rede e-Science. Para aprender a usar o anaconda, verifique a seção seguinte do tutorial, 'Uso do anaconda'.

### Uso do anaconda

#### Ativação do anaconda
Toda vez que quiser usar o anaconda, a primeira coisa a se fazer é ativar o anaconda, o que pode ser feito executando o comando:
```bash
source ~/.bashrc
```
Rodado esse comando, o prefixo '(base)' deve aparecer antes do seu usuário na linha de comando como em '`(base)user_science@deepone:~$ `', indicando que você está no ambiente primário do anaconda.

#### Atualizar o anaconda
A fim de se certificar que seu anaconda está atualziado, basta executar:
```bash 
conda update conda
```

#### Criação de um ambiente anaconda
Podemos tanto criar um ambiente anaconda sem nenhum pacote adicional quanto a partir de um arquivo de configuração. A primeira opção pode ser feita com:

```bash
conda create --name myenv python=3.7 -y
```
no caso do exemplo, informamos que a versão desejada do python é a 3.7 (se não informarmos nada, se usará uma versão predefinida do python).

Outra forma de criar um ambiente python é usando um arquivo de configuração `.yml`, que já informe tanto os pacotes a serem usados quanto o nome do ambiente. Para isso, basta adicionar a flag '-f' e informar o arquivo `.yml`:

```bash
conda create --name myenv --file=<arquivo.yml> -y
```
#### Remoção de um ambiente anaconda
Basta executar:
```bash
conda remove --name <old_env> --all
```
onde `<old_env>` deve ser substituído pelo nome do ambiente a ser removido.

#### Lista de ambientes anaconda criados
O comando a seguir mostra todos os ambientes criados:
```bash
conda env list
```

#### Ativação de um ambiente anaconda
A fim de ativar um ambiente, basta executar:
```bash
conda activate <env_name>
```
onde `<old_env>` deve ser substituído pelo nome do ambiente a ser ativado. Após rodar esse comando, um prefixo com o nome do ambiente deve aparecer antes do seu usuário na linha de comando como em '`(myenv)user_science@deepone:~$ `', indicando que você está no ambiente desejado.

#### Desativação de um ambiente anaconda
Para sair de um ambiente, ou seja, desativá-lo, deve-se rodar o seguinte comando após ter entrado em algum ambiente anaconda:
```bash
conda deactivate
```

#### Instalação de um pacote com anaconda
A fim de instalar um pacote no ambiente anaconda, basta rodar:
```bash
conda install <package_name>
```
onde `<package_name>` deve ser substituído pelo nome do pacote a ser instalado. Veja um exemplo:

```bash
(myenv)user_science@deepone:~$ conda install numpy
```

#### Verificar a lista de pacotes disponíveis no ambiente anaconda
Para verificar os pacotes instalados e disponíveis no ambiente atual, basta executar:
```bash
conda list
```

## 2. Conectando-se à Rede Vision (Acesso ao Servidor via SSH)

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

Durante a geração da chave, será necessário confirmar o local de salvamento (```~/.ssh/id_rsa```) e definir uma senha — ambos são opcionais e, caso não queira, basta pressionar Enter. Esse processo criará duas chaves: uma privada (```~/.ssh/id_rsa```), usada para autenticar suas conexões, e uma pública (```~/.ssh/id_rsa.pub```), que deve ser copiada para o servidor da Rede Vision para obter acesso.

### 3. Copiando a chave SSH pública para a Rede Vision

Há 2 comandos possíveis para se copiar a chave para os servidores, sendo o primeiro:

```bash
ssh-copy-id <user_science>@vision.ime.usp.br
``` 

Após executado o comando acima, será solicitado a senha da sua conta ( aquela enviada por email ) e após isso o acesso estará pronto, mas caso este primeiro comando não funcione utilize:

```bash
cat ~/.ssh/id_rsa.pub | ssh <user_science>@vision.ime.usp.br "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

Este comando não solicitará sua senha e, após isso, seu acesso à Rede Vision está pronto! Para se conectar utilize o comando:

```bash
ssh <user_science>@vision.ime.usp.br 
```

E com isso, você estará conectado à máquina de entrada ( lembra que nunca se deve fazer experimentos nela! ).

## 3. Permissões e acessos
Na rede e-Science, um usuário que não seja administrador não tem acesso aos comandos apt-get e sudo, essenciais para a realização de diversas tarefas. Sendo assim, é necessário não só usar ambientes de desenvolvimento como os do anaconda caso deseje usar pacotes adicionais em seus projetos, mas também é necessário contatar a administração da rede caso seja negado o acesso a algum recurso que você precise usar. Isso pode ser feito por meio do envio de um email para: `adminvision@ime.usp.br`. 

## 4. Configurando o Arquivo `.bashrc`
- Alias úteis para comandos comuns





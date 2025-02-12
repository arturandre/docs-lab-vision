# Instalando e configurando o seu ambiente de trabalho

Configurar seu ambiente de trabalho corretamente é essencial para aproveitar os recursos do laboratório. Este documento fornece um guia passo a passo para configurações úteis mais comuns.

Para usar e configurar ambientes python, recomendamos baixar e instalar o Miniconda, uma vez que, na Rede e-Science, usuários que não tenham as permissões de administrador não podem executar comandos com sudo nem com apt-get, essenciais na instalação de pacotes. Tanto o uso quanto a instalação do Miniconda estão explicados nessa página. Ademais, supomos o uso do sistema operacional linux, de modo que, nesse tutorial, todos os comandos foram testados em um terminal linux. Nesta página, há também uma explicação sobre as permissões e acessos que o usuário comum tem na Rede e-Science.

## 1. Miniconda 

### O que é o Anaconda e porque usar o Miniconda?

Anaconda é uma plataforma para se desenvolver projetos em python e R. Sua versão completa, ou seja, o anaconda3, dispõe de mais de 7500 pacotes adicionais, que podem ser instalados pelo repositório do Anaconda, fora os 300 pacotes que já vem instalados ao baixá-lo. De forma simples, o Anaconda permite a criação de ambientes de programação diversos e independentes entre si, o que facilita o desenvolvimento de programas que dependem de múltiplos pacotes adicionais. Para conferir mais sobre, confira a [Documentação do Anaconda](https://docs.anaconda.com/).

Em relação à Rede e-Science, temos um interesse especial no Miniconda, uma versão do Anaconda que não tem nenhum pacote pré-instalado, de forma que ocupa muito menos espaço que o anaconda3 e apresenta as mesmas funcionalidades.

### Instalando o miniconda no meu usuário da Rede e-Science
Como primeiro passo, baixe, no seu computador, a versão mais recente do miniconda a partir da execução do seguinte comando:

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

Ao executar este comando, o arquivo `.sh` será baixado no mesmo diretório em que se rodou o código acima. Agora, devemos mandá-lo à máquina de acesso shell da Rede e-Science. Para isso,
rode o comando:
```bash
scp <endereço do .sh baixado> <user_science>@vision.ime.usp.br:~
```
Onde `<user_science>` deve ser substituído pelo nome de seu usuário na Rede e-Science e `<endereço .sh>`, pelo endereço do arquivo .sh em sua máquina. Vale ressaltar que será necessário inserir sua senha após rodar o comando, caso não tenha configurado ainda o acesso remoto sem senha, cujo tutorial está disponível na página "Acessando e editando código remotamente", localizada dentro da seção "Tutoriais" desta documentação.

Exemplo: `scp ~/Downloads/Miniconda3-latest-Linux-x86_64.sh usuario@vision.ime.usp.br:~`

Após a execução deste comando, o arquivo estará disponível na sua home em qualquer máquina da Rede e-Science. Portanto, acesse a máquina de acesso desta rede com o comando:
```bash
ssh <user_science>@vision.ime.usp.br
``` 

Estando nessa máquina, como não é recomendado instalar nada a partir da máquina de entrada shell, devemos acessar outra, como, por exemplo, a deepzero, com o comando `ssh deepzero`. Quando a linha de comando do terminal se parecer com `user_science@deepzero:~$`, entramos na máquina `deepzero`. Agora, vamos, de fato instalar o miniconda. Assim, devemos executar o bash script anteriormente baixado a partir do seguinte comando:

```bash
bash Miniconda3-latest-Linux-x86_64.sh
```

Executado esse comando, será mostrado os termos de licença do Anaconda. Basta aceitá-los digitando 'yes' quando requisitado e configurar o local de instalação que o miniconda será instalado no seu usuário da Rede e-Science.

### Configurando o miniconda no meu usuário da Rede e-Science

A fim de configurar o anaconda, será necessário ativá-lo pela primeira vez, o que é feito a partir da execução do seguinte comando:

```bash
eval "$(<local_instalacao_miniconda>/conda shell.YOUR_SHELL_NAME hook)"
```

ou algum comando parecido, que será exibido como orientação do próprio anaconda após sua instalação. Assim, você deve substituir `YOUR_SHELL_NAME` pela palavra `bash` e `local_instalacao_anaconda`, pelo caminho para o local onde foi instalado o anaconda, por padrão, `/home/<user_science>/miniconda3/bin`, de modo que o comando seria algo como:

```bash
eval "$(/home/user1/miniconda3/bin/conda shell.bash hook)"
```
Quando entrar no ambiente base do anaconda, ou seja, quando o seu terminal parecer algo como `(base)user_science@deepzero:~$ `, rode o comando:

```bash
conda init
```

Finalmente, basta reiniciar o terminal com `Ctrl+ D` para fechá-lo e `Ctrl+Alt+T` para abri-lo que o conda estará ativado no ambiente base e configurado, de modo que será possível usá-lo livremente na Rede e-Science. Para aprender a usar o anaconda, verifique a seção seguinte do tutorial, 'Uso do anaconda'.

### Uso do anaconda

#### Ativação do anaconda
Toda vez que quiser usar o anaconda, a primeira coisa a se fazer é ativar o anaconda, o que pode ser feito executando o comando:
```bash
source ~/.bashrc
```
Rodado esse comando, o prefixo '(base)' deve aparecer antes do seu usuário na linha de comando como em '`(base)user_science@deepzero:~$ `', indicando que você está no ambiente primário do anaconda.

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
onde `<old_env>` deve ser substituído pelo nome do ambiente a ser ativado. Após rodar esse comando, um prefixo com o nome do ambiente deve aparecer antes do seu usuário na linha de comando como em '`(myenv)user_science@deepzero:~$ `', indicando que você está no ambiente desejado.

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
conda install numpy
```

#### Verificar a lista de pacotes disponíveis no ambiente anaconda
Para verificar os pacotes instalados e disponíveis no ambiente atual, basta executar:
```bash
conda list
```

## 2. Permissões e acessos
Na Rede e-Science, um usuário que não seja administrador não tem acesso aos comandos apt-get e sudo, essenciais para a realização de diversas tarefas. Sendo assim, é necessário não só usar ambientes de desenvolvimento como os do anaconda caso deseje usar pacotes adicionais em seus projetos, mas também é necessário contatar a administração da rede caso seja negado o acesso a algum recurso que você precise usar. Isso pode ser feito por meio do envio de um email para: `adminvision@ime.usp.br`. 

<!-- ## 4. Configurando o Arquivo `.bashrc`
- Alias úteis para comandos comuns -->





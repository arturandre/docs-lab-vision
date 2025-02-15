# Execução de Processos em Background

Executar tarefas longas, que podem demorar horas ou dias, exige um tratamento especial no comando, pois não é razoável manter o terminal aberto e conectado na sua máquina local durante esse período.

Existem muitas formas de lidar com esse problema, e aqui iremos explorar três delas - os comandos `&`, `nohup` e `screen`.

## O comando `&`

O operador `&` permite que você execute um comando em segundo plano diretamente no terminal. Isso é útil para iniciar processos sem bloquear o terminal. Ao usá-lo, o processo continuará a imprimir na saída padrão.

!!! example "Exemplo"
	```bash
	python script.py &
	```
* O terminal retornará o número identificador do processo PID (Process ID).
* Você pode continuar usando o terminal enquanto o script está em execução.
* Para acessar os processos em execução em segundo plano você pode usar o comando `jobs`.

!!! danger "Cuidado"
	Fechar o terminal irá matar o processo. Use o `&` em conjunto com o `nohup` para evitar isso.

## O comando `nohup`

Caso você queira salvar a saída padrão dessa execução, é possível usar o comando `nohup` (no hang-up), que a redireciona para um arquivo designado (`nohup.out` por padrão). Além disso, ele permite que o processo continue rodando mesmo que você encerre a sessão SSH ou feche o terminal.

!!! example "Exemplo"
	```bash
	nohup python script.py &
	```
* O comando salva a saída padrão em um arquivo chamado `nohup.out` por padrão.


!!! tip "Para redirecionar a saída para um arquivo específico"
	```bash
	nohup python script.py > output.log 2>&1 &
	```

## O comando `screen`

O `screen` é uma ferramenta poderosa para criar sessões persistentes. Você pode desconectar-se da sessão e reconectá-la posteriormente.

### Criando uma nova sessão
!!! info "Novo terminal" 
	```bash
	screen -S minha_sessao
	```
* Uma vez na sessão, você pode usar o terminal normalmente.

### Desconectando-se da sessão
Pressione `Ctrl+A,D` (Ctrl+A depois D) para desconectar da sessão sem encerrá-la.

### Reconectando-se à uma sessão
!!! info "Veja as sessões disponíveis"
	```bash
	screen -list
	```
!!! success "Reconectar à sua sessão"
	```bash
	screen -r minha_sessao
	```

### Fechando uma sessão
Para sair e fechar uma sessão, basta fechar o terminal dela.
!!! failure "Sair da sessão"
	```bash
	exit
	```

### Informações adicionais
Para informações mais específicas, acesse a [man page do screen](https://www.gnu.org/software/screen/manual/screen.html) ou use o [explain shell](https://explainshell.com/explain?cmd=screen+-r+nova_sessao) para investigar o que cada parâmetro realiza.

## Considerações finais
Qualquer que seja a forma escolhida para executar os processos, é importante ficar atento às tarefas que está executando. Lembre-se de que essa é uma rede compartilhada.

Para ver como avaliar os recursos que você está usando acesse: [Quais recursos estão disponíveis e quanto estou usando?](resources.md).

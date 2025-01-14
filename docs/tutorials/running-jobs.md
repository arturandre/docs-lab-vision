# Executando tarefas em segundo plano

Em um ambiente compartilhado ou ao executar tarefas longas, como o treinamento de modelos de aprendizado profundo, é essencial garantir que os processos continuem mesmo após desconexões. Comandos para execução em segundo plano permitem liberar o terminal e manter a continuidade das operações sem interrupções. Este tutorial apresenta ferramentas como `&`, `nohup` e `screen` para gerenciar essas situações de forma eficiente.

## Operador &

O operador `&` permite que você execute um comando em segundo plano diretamente no terminal. Isso é útil para iniciar processos sem bloquear o terminal.

### Exemplo:
```bash
python script.py &
```
- O terminal retornará um número (PID - Process ID) que identifica o processo.
- Você pode continuar usando o terminal enquanto o script está em execução.
- Para acessar os processos em execução você pode usar o comando `jobs`.

## Comando nohup

O comando `nohup` (no hang-up) permite que um processo continue rodando mesmo que você encerre a sessão SSH ou feche o terminal.

### Exemplo:
```bash
nohup python script.py
```

- O comando salva a saída padrão em um arquivo chamado `nohup.out` por padrão.
- Para redirecionar a saída para um arquivo específico:
```bash
nohup python script.py > output.log 2>&1 &
```

## Comando screen

O `screen` é uma ferramenta poderosa para criar sessões persistentes. Você pode desconectar-se da sessão e reconectá-la posteriormente. É interessante para tarefas mais interativas.

### Criando uma nova sessão:
```bash
screen -S minha_sessao
```
- Após isso, você pode iniciar o comando desejado.

### Desconectando-se da sessão:
Pressione `Ctrl+A`, depois `D` para desconectar a sessão sem encerrá-la.

### Reconectando-se a uma sessão:
Veja as sessões disponíveis:
```bash
screen -ls
```
Reconecte-se a uma sessão específica:
```bash
screen -r minha_sessao
```

Atente-se às tarefas que está executando. Lembre-se que essa é uma rede compartilhada.

Para ver como avaliar os recursos que você está usando acesse o tutorial: [Quais recursos estão disponíveis e quanto estou usando?](tutorials/resources.md).

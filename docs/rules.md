# Regras de uso


### 1 - Máquina de entrada
NUNCA, mas NUNCA mesmo, use a máquina de entrada para fazer experimentos.

### 2 - Múltipos processos
NUNCA, mas NUNCA mesmo, entupa as máquinas com seus processos, como se você fosse o único usuário da rede. [Aprenda a usar o comando nice do linux](tutorials/resources.md).

### 3 - Muitas operações de escrita e leitura.
Caso você precise executar processos que realizem muitas operações de entrada/saída (gravação e leitura de arquivos em disco), você deve usar o disco local de cada máquina e, depois, copiar os resultados para o seu diretório. Isso reduz o consumo de banda da rede e acelera a execução de seus processos. Para isso, escreva para adminvision@ime.usp.br solicitando a criação de uma pasta para você (geralmente em /misc/users).

### 4 - Experimentos
NÃO faça ciência baseada em bruta-força! Pense no seu problema, discuta com a sua orientadora, ou com o seu orientador.

### 5 - Lista de emails
Temos a lista de emails esciencelab@lists.ime.usp.br, que serve para anúncios e discussões técnicas sobre eScience. Se precisar de ajuda, use-a. Todos os usuários da Rede eScience já deveriam estar automaticamente inscritos. Caso não esteja recebendo os emails da lista, solicite sua inscrição pelo email esciencelab-request@lists.ime.usp.br.

### 6 - Política de cotas de armazenamento
A Rede eScience possui uma política de cotas. Cada usuário tem uma cota de 100 GB. Se você passar disso, não conseguirá mais escrever no seu home. Para ficar dentro do limite, você deve fazer uma limpeza de sua área e copiar dados não usados frequentemente em memória externa (pen-drives ou HDs externos).

### 7 - Diretório scratch 
Alguns usuários precisam de mais de 100 GB e existe uma solução para esses casos, que é o diretório ```/scratch/<username>```. Nesse diretório você pode guardar resultados intermediários, datasets etc. Esse é também um bom lugar para compartilhar arquivos.

Para saber quanto espaço você ocupa no servidor, digite:
```bash
cd ~
du -sh
```

[saiba mais sobre du -sh](https://explainshell.com/explain?cmd=du+-sh+)


### 8 - Acesso físico ao laboratório
Os laboratórios da Rede eScience ficam nos blocos A e CCSL do IME-USP. Para cadastrar sua 
carteirinha da USP e passar a ter acesso físico aos laboratórios, por favor, escreva para adminvision@ime.usp.br.

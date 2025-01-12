# Acessando e editando código remotamente

Editar códigos que serão executados em uma máquina remota, como na rede vision, pode ser complicado, ainda mais se forem necessários testes, experimentações ou prototipagem. Executar localmente e enviar o código via git não é produtivo.


## vscode
O vscode e outras IDEs modernas permitem acesso de pastas via ssh, agilizando bastante o desenvolvimento.
- instale extensão apropriada
- configure host e conecte na máquina desejada
- lembre-se: nunca realize experimentos e processamentos na máquina de entrada.

### ssh tunneling
- altere o arquivo .ssh/config na sua máquina local
- adicione a shell como Host e a máquina que você irá fazer o experimento.
- o tunneling também permite que você acesse a máquina interna diretamente

## jupyter notebook / jupyterlab
TODO



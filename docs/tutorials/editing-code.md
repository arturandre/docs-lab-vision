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

## Configurando Jupyter Notebook via SSH no VS Code

### 1. Conectar via SSH
No **VS Code**, clique no botão de SSH no canto inferior esquerdo e conecte-se ao servidor remoto da vision

### 2. Instale o Jupyter Lab
```bash
pip install jupyterlab
```

### 3. Gerar o arquivo de configuração do Jupyter
No terminal da máquina remota execute:
```bash
jupyter notebook --generate-config
```
Isso criará o arquivo `~/.jupyter/jupyter_notebook_config.py`.

### 3. Editar a configuração do Jupyter
Edite o arquivo de configuração:
```bash
nano ~/.jupyter/jupyter_notebook_config.py
```
Adicione essa linha abaixo de `c = get_config()`:
```python
c.NotebookApp.token = '<USERNAME>'  # Ou outro token de sua escolha
```

### 4. Reiniciar a conexão SSH
Reinicie a conexão SSH e conecte-se novamente em alguma máquina com **GPU**

### 5. Iniciar o Jupyter Lab
Na máquina, execute:
```bash
jupyter lab --no-browser --ip=0.0.0.0 --port=8888
```
O terminal mostrará um link semelhante a:
```
http://deepeleven:8888/lab?token=...
```

Copie esse link e substitua `...` pelo token definido:
```
http://deepeleven:8888/lab?token=<TOKEN>
```

### 6. Configurar o Kernel no Jupyter Notebook
- Abra o notebook no VS Code
- No canto superior direito, clique no botão `Select Kernel`
- Selecione `Select Another Kernel` → `Existing Jupyter Server`
- Cole o link modificado com o Token e conecte

### 7. Verificar se a GPU está ativa
No Jupyter Notebook, execute:
```python
!nvidia-smi
```
Se tudo estiver correto, você verá informações sobre a GPU disponível

## Obs.:
- Se mais de um usuário ativo utilizar a mesma porta (ex: `8888`), pode ocorrer um conflito ao rodar o Jupyter. Caso enfrente problemas, tente alterar a porta
- Por padrão, o Jupyter só aceita conexões locais (`localhost` ou `127.0.0.1`). Definir `0.0.0.0` permite que qualquer máquina na rede acesse o servidor Jupyter (desde que tenha permissão). Isso é necessário porque você está acessando o Jupyter de outra máquina via SSH



# Gere o seu arquivo de configuração de ssh para ssh tunnelling na vision

## explicações prévias (em ordem)
As explicações dessa parte precisam estar muito corretas pq é questão de segurança do usuário. Temos que fazer double/triple check de tudo.

- acesso via ssh
- gerar ssh keygen
- mudança de senha da primeira vez
- authorized keys
- ssh tunnelling

## (.ssh/config)
Insira abaixo o seu username para gerar o arquivo .ssh/config com o seu nome.
Clique no botão copiar ao lado direito do código.
<br>
<input id="userInput" type="text" placeholder="seu username da vision">
<button onclick="computeOutput()"> Gerar código</button>

<style>
.md-typeset pre > code {
    max-height: 15rem;
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

### abordagem usada
Escrevi um html, com javascript, querySelector, etc...

Tem que melhorar estética do botão/caixa de entrada.
Tem que melhorar estética do código em si, talvez importart custom .css e .js ao invés de usar desse jeito.
Talvez à priori possa só deixar assim também... Antes feito que perfeito...

### vantagens
- já está funcional
- usuário não tem que rodar código nenhum
- usuário não edita edita nada manualmente
- usuário não precisa saber muito do que está acontecendo no código


### desvantagens
- ruim de fazer manutenção
- fora do padrão markdown / mkdocs





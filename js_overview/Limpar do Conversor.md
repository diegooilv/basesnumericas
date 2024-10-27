```javascript
let elementoEmFoco; 

function salvarElementoEmFoco(event) {
    elementoEmFoco = event.target; 
}

function apagarConteudo() {
    document.getElementById("base-2").value = "";
    document.getElementById("base-10").value = "";
    document.getElementById("base-8").value = "";
    document.getElementById("base-16").value = "";

    if (elementoEmFoco) {
        elementoEmFoco.focus();
    }
}

document.querySelectorAll("textarea").forEach(textarea => {
    textarea.addEventListener('focus', salvarElementoEmFoco);
});
```

## Explicação do Código

### Declaração de Variável para Armazenar o Elemento em Foco

`let elementoEmFoco;`

Aqui, criamos uma variável chamada `elementoEmFoco` que será usada para armazenar o último elemento de entrada (`textarea`) que recebeu o foco. Inicialmente, ela está vazia (indefinida).

### Função `salvarElementoEmFoco`

A função `salvarElementoEmFoco` é acionada sempre que um evento de foco (`focus`) ocorre em um dos elementos de entrada (`textarea`). O parâmetro `event` contém informações sobre o evento disparado e o elemento que o disparou (armazenado em `event.target`). A linha `elementoEmFoco = event.target;` atualiza a variável `elementoEmFoco` para que sempre armazene o último elemento que recebeu o foco.

### Função `apagarConteudo`

A função `apagarConteudo` é responsável por limpar o conteúdo de campos específicos (`base-2`, `base-10`, `base-8`, `base-16`). Após a limpeza, a função verifica se `elementoEmFoco` está definido (ou seja, se um campo estava em foco antes de chamar a função). Se sim, o foco é retornado para esse elemento.

### Adicionando o Evento de Foco aos Campos `textarea`

`document.querySelectorAll("textarea").forEach(textarea => { textarea.addEventListener('focus', salvarElementoEmFoco); });`

Este trecho de código seleciona todos os elementos `textarea` da página e adiciona um listener de evento `focus` para cada um. Sempre que um desses campos recebe foco, o evento dispara a função `salvarElementoEmFoco`, que armazena o campo atualmente focado em `elementoEmFoco`.
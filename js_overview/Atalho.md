```javascript
document.addEventListener('keydown', function (event) {
    if (event.ctrlKey && event.key === 'l') {
        event.preventDefault();
        document.getElementById('botaoLimpar').click();
    }
    if (event.ctrlKey && event.key === 'o') {
        event.preventDefault();
        document.getElementById('format-button').click();
    }
});
```

### Funcionamento do Código

1. **Escuta o Evento `keydown`**:
   O código utiliza `document.addEventListener` para escutar o evento `keydown`, que é acionado sempre que uma tecla é pressionada.

2. **Captura do Evento**:
   Quando o evento `keydown` ocorre, uma função anônima é chamada. Essa função recebe um objeto `event`, que contém informações sobre o evento ocorrido, como qual tecla foi pressionada e se a tecla `Ctrl` estava pressionada.

3. **Verificação de Teclas Específicas**:
   - O primeiro bloco `if` verifica se a tecla `Ctrl` (`event.ctrlKey`) e a tecla `l` (`event.key === 'l'`) foram pressionadas simultaneamente. Se a condição for verdadeira:
     - `event.preventDefault();` é chamado para impedir o comportamento padrão do navegador (por exemplo, a ação de limpar a barra de endereços).
     - O código simula um clique no elemento com o ID `botaoLimpar` usando `document.getElementById('botaoLimpar').click();`.
   
   - O segundo bloco `if` funciona de maneira semelhante, mas verifica se a tecla `o` foi pressionada em conjunto com `Ctrl`. Neste caso, ele simula um clique no botão com o ID `format-button`.


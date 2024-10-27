```javascript
$(document).ready(function () {
    var maxLength = 12;

    $('#base-2, #base-8, #base-10, #base-16').on('input', function () {
        var val = $(this).val();
        if (val.length > maxLength) {
            $(this).val(val.slice(0, maxLength));
        }
    });
});
```

**`$(document).ready(function () { ... });`**: Esta linha garante que o código dentro dela só será executado depois que o documento HTML estiver totalmente carregado. Isso é importante para garantir que todos os elementos do DOM estejam disponíveis para manipulação.

**`var maxLength = 12;`**: Define uma variável chamada `maxLength` com o valor 12, que será o comprimento máximo de caracteres permitido para os campos de entrada.

**`$('#base-2, #base-8, #base-10, #base-16').on('input', function () { ... });`**: Esta linha usa jQuery para selecionar os elementos de input com os IDs `base-2`, `base-8`, `base-10` e `base-16`. O evento `'input'` é vinculado a esses elementos, de forma que sempre que o usuário digitar ou colar algo neles, a função fornecida será executada.

**`var val = $(this).val();`**: Dentro da função de callback, `$(this)` se refere ao elemento de input que disparou o evento. `val()` obtém o valor atual desse input e o armazena na variável `val`.

**`if (val.length > maxLength) { $(this).val(val.slice(0, maxLength)); }`**: Esta linha verifica se o comprimento do valor do input excede o `maxLength`. Se sim, ele corta o valor para os primeiros 12 caracteres usando `slice(0, maxLength)` e atualiza o valor do input.

---

```javascript
(() => {
    "use strict";
    !function (e) {
```

**`(() => { "use strict"; ... })();`**: Esta é uma função de escopo imediato (IIFE) que executa o código imediatamente. O modo `"use strict"` é ativado para garantir que o JavaScript seja executado em um modo mais seguro, evitando alguns comportamentos problemáticos.

**`!function (e) { ... }(jQuery);`**: Outra IIFE que aceita `jQuery` como argumento, renomeando-a como `e`. Isso permite usar `e` em vez de `jQuery` dentro do escopo da função, tornando o código mais conciso.

---

```javascript
function a(e, a, t) {
    if (!e) return "";
    var s = parseInt(e, a);
    return isNaN(s) ? "" : s.toString(t).toUpperCase();
}
```

**`function a(e, a, t) { ... }`**: Esta função converte um número de uma base para outra. Ela recebe três argumentos:
   - `e`: O valor a ser convertido.
   - `a`: A base de origem.
   - `t`: A base de destino.

**`if (!e) return "";`**: Se `e` não estiver presente (ou seja, é uma string vazia), a função retorna uma string vazia.

**`var s = parseInt(e, a);`**: Converte o valor `e` da base `a` para um número inteiro.

**`return isNaN(s) ? "" : s.toString(t).toUpperCase();`**: Se a conversão resultar em `NaN`, a função retorna uma string vazia. Caso contrário, o número convertido é retornado na base `t` e transformado em letras maiúsculas.

---

```javascript
function handleInput(selector, baseFrom) {
    e(selector).on("input", function () {
        var s = e(this).val();
        var regex = getRegex(baseFrom);
```

**`function handleInput(selector, baseFrom) { ... }`**: Esta função trata a entrada do usuário para os inputs de base. Ela recebe dois argumentos:
   - `selector`: O seletor do elemento de input.
   - `baseFrom`: A base do número que está sendo digitado.

**`e(selector).on("input", function () { ... });`**: Vincula o evento de input ao elemento selecionado.

**`var s = e(this).val();`**: Obtém o valor atual do input.

**`var regex = getRegex(baseFrom);`**: Chama a função `getRegex` para obter a expressão regular correspondente à base de entrada, que será usada para validar a entrada do usuário.

---

```javascript
if (!regex.valid.test(s)) {
    s = s.replace(regex.invalid, "");
}
```

**`if (!regex.valid.test(s)) { ... }`**: Verifica se o valor atual do input (`s`) corresponde à expressão regular válida para a base. Se não corresponder, o valor será ajustado.

**`s = s.replace(regex.invalid, "");`**: Remove caracteres inválidos do valor `s` usando a expressão regular `invalid`.

---

```javascript
if (s.length > 12) {
    s = s.slice(0, 12);
}
```

**`if (s.length > 12) { ... }`**: Verifica se o comprimento do valor `s` excede 12 caracteres e, se sim, corta o valor para os primeiros 12 caracteres.

---

```javascript
if (s.charAt(0) === '0' && s.length > 1) {
    s = s.slice(0, -1);
}

if (s.charAt(s.length - 1) === '0' && s.length === 1) {
    s = ''; // Se o único caractere for zero, limpe o input
}
```

**`if (s.charAt(0) === '0' && s.length > 1) { ... }`**: Se o primeiro caractere é '0' e o comprimento é maior que 1, remove o último caractere. Isso garante que a entrada não comece com um zero, exceto se o valor for realmente zero.

**`if (s.charAt(s.length - 1) === '0' && s.length === 1) { ... }`**: Se o último caractere é '0' e o comprimento é igual a 1, limpa o input, deixando-o vazio. Isso lida com o caso onde apenas um zero foi digitado.

---

```javascript
e(this).val(s);
```

**`e(this).val(s);`**: Atualiza o valor do input com o valor modificado `s`.

---

```javascript
if (s) {
    e("#base-2").val(a(s, baseFrom, 2));
    e("#base-8").val(a(s, baseFrom, 8));
    e("#base-10").val(a(s, baseFrom, 10));
    e("#base-16").val(a(s, baseFrom, 16));
} else {
    e("#base-2, #base-8, #base-10, #base-16").val("");
}
```

**`if (s) { ... } else { ... }`**: Se `s` não estiver vazio, realiza as conversões para as outras bases (2, 8, 10, 16) usando a função `a`. Caso contrário, limpa os valores dos inputs correspondentes.

---

```javascript
function getRegex(base) {
    switch (base) {
        case 2:
            return { valid: /^[01]*$/, invalid: /[^01]/g };
        case 8:
            return { valid: /^[0-7]*$/, invalid: /[^0-7]/g };
        case 10:
            return { valid: /^[0-9]*$/, invalid: /[^0-9]/g };
        case 16:
            return { valid: /^[0-9A-Fa-f]*$/, invalid: /[^0-9A-Fa-f]/g };
    }
}
```

**`function getRegex(base) { ... }`**: Esta função retorna um objeto que contém duas expressões regulares: `valid` e `invalid`, dependendo da base fornecida. As expressões regulares são usadas para validar e filtrar a entrada do usuário.

---

```javascript
handleInput("#base-2", 2);
handleInput("#base-8", 8);
handleInput("#base-10", 10);
handleInput("#base-16", 16);
```

**`handleInput(...)`**: Chama a função `handleInput` para cada uma das bases (2, 8, 10, 16) para configurar o tratamento de entrada para cada input.

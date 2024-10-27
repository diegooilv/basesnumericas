# Função `formatNumber`

A função `formatNumber` é utilizada para formatar números de acordo com diferentes bases numéricas: binária (base 2), octal (base 8), decimal (base 10) e hexadecimal (base 16). A função recebe dois parâmetros: um valor numérico (`value`) e a base para a qual o número deve ser formatado (`base`).

## Detalhes da Função

A função começa removendo todos os caracteres não numéricos do `value` e transformando-o em letras maiúsculas, o que é especialmente útil para a formatação hexadecimal. A linha de código responsável por isso é:

```javascript
value = value.replace(/\W/g, "").toUpperCase();
```

A função então utiliza uma estrutura de controle `switch` para determinar qual formatação aplicar, dependendo do valor de `base`.

### Formatação por Base

- **Base 2 (Binário)**:
  Para a base binária, a função inverte a ordem dos caracteres, agrupa-os em blocos de 4, adiciona um espaço entre os grupos, remove espaços em branco extras e, finalmente, inverte novamente a string. O código relevante é:

  ```javascript
  return value.split("").reverse().join("").replace(/(.{4})/g, "$1 ").trim().split("").reverse().join("");
  ```

- **Base 8 (Octal)**:
  A formatação octal segue a mesma lógica, mas agrupa os caracteres em blocos de 3. O código é semelhante ao da base binária, apenas alterando o número de caracteres por grupo:

  ```javascript
  return value.split("").reverse().join("").replace(/(.{3})/g, "$1 ").trim().split("").reverse().join("");
  ```

- **Base 10 (Decimal)**:
  Para a base decimal, a função utiliza uma expressão regular para adicionar um ponto a cada três dígitos, permitindo uma melhor legibilidade. O código para isso é:

  ```javascript
  return value.replace(/\B(?=(\d{3})+(?!\d))/g, ".");
  ```

- **Base 16 (Hexadecimal)**:
  A formatação hexadecimal é semelhante à formatação binária, agrupando os caracteres em blocos de 4:

  ```javascript
  return value.split("").reverse().join("").replace(/(.{4})/g, "$1 ").trim().split("").reverse().join("");
  ```

### Valor Padrão

Se a base não corresponder a nenhum dos casos tratados, a função simplesmente retorna o `value` sem formatação:

```javascript
default:
    return value;
```

# Interação com o Botão

A função também está integrada a um evento de clique de um botão com o ID `format-button`. Quando este botão é clicado, o código a seguir é executado:

```javascript
$("#format-button").on("click", function () {
    let binary = $("#base-2").val();
    let octal = $("#base-8").val();
    let decimal = $("#base-10").val();
    let hexadecimal = $("#base-16").val();

    $("#base-2").val(formatNumber(binary, 2));
    $("#base-8").val(formatNumber(octal, 8));
    $("#base-10").val(formatNumber(decimal, 10));
    $("#base-16").val(formatNumber(hexadecimal, 16));
});
```

## Explicação do Evento

- Os valores de cada campo de entrada (representando diferentes bases numéricas) são capturados.
- A função `formatNumber` é chamada para cada valor, utilizando a base correspondente.
- O resultado formatado é então definido de volta em cada campo de entrada.
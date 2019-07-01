---
id: boas_praticas
title: Boas Práticas
---

## JavaScript Formatting

#### Comprimento máximo das linhas

É sugerido que as linhas tenham no máximo 80 caracteres de comprimento.

#### Indentação

Sugere-se que sejam utilizados 4 espaços para indentar e tabs não são encorajadas a se utilizar.


Strings
Utilize aspas simples ao invés de duplas, por consistência.
É útil quando há a necessidade de incluir HTML dentro das strings.

var msg = '<span class="text">Hello World!</div>';

---

Estilização
Quando JavaScript for necessário para alterar o visual de algum elemento, aconselha-se a utilizar classes com as propriedades, ao invés de inserir as propriedades inline no elemento.

$(‘element’).toggleClass(‘_active’);

$(‘element’).css(‘display’, ‘block’);

---

Chaves
Sempre utilizar dentro de blocos com multi-linhas.
img ppt

---

Ponto e vírgula
Sempre utilizar ao final das declarações.
O JavaScript requer que declarações sejam terminadas em ponto e vírgula, exceto quando ele infere a sua existência.
O JavaScript nunca termina uma declaração se o próximo caractere for um ‘bracket’.



img ppt

---

Concatenação de grandes strings
É sugerido que as linhas tenham no máximo 80 caracteres de comprimento.

img ppt

---

Fim do arquivo
A última linha deve ser vazia.
Isso diminui a quantidade de linhas alteradas em um diff e torna o código mais seguro no processo de concatenação.
Convenções gerais para nomes
Evitar underline e números. (exceção)
Devem ter um nome que remetam à sua funcionalidade.
Nome de métodos e variáveis de um objeto, caso sejam private ou protected, devem iniciar com underline.


## JavaScript Naming

Funções, métodos e variáveis
Nome dos métodos das classes devem iniciar com um verbo em Inglês e no infinitivo. 
Ex: initialize, close, open, save, get, set.
Métodos que retornem status flag ou Boolean, devem iniciar com has ou is.
Nome dos métodos para acessar variáveis estáticas sempre iniciam com get ou set.
Nunca utilizar nomes curtos para variáveis( var i, var n...), exceto em loops curtos.
Organizar o código para que seja lido de forma funcional, e não procedural.

---

## JavaScript Coding

Strict mode
"use strict";
É uma expressão literal ignorada por versões anteriores ao ECMAScript 5.
Aumenta a ‘segurança’ do código, transformando erros aceitáveis de sintaxe, em erros reais.

---

Declarar variáveis
Sempre que possível, declarar variáveis com var para que não afete variáveis de escopo global.
Procurar declarar var apenas uma vez por escopo.
var foo = 'bar',
    num = 1,
    arr = [1, 2, 3];
    
---

Declarar funções dentro de blocos

img ppt


---

Declarar arrays e objetos (single line)
var arr = [1, 2, 3];  // Sem espaços depois [ ou antes ].

var obj = {a: 1, b: 2, c: 3};  // Sem espaços depois { ou antes }.

---

Declarar objetos (multi lines)
Propriedades e métodos alinhados.
Object.prototype = {
    a: 0,
    b: 1,
    lengthyName: 2
};


---

Arrays associativos
Sempre utilizar objetos ao invés de arrays associativos.
Errado							Correto

img ppt

---

## LESS

Indentação
Sugere-se que sejam indentados sempre com 4 espaços.
Aspas
Sempre utilizar aspas simples dentro das strings de valores.


---

Brackets
Sempre utilizar um espaço antes de abrir brackets e uma quebra de linha antes de fechar.
// Correto
.nav {
    color: @nav__color;
}
// Incorreto
.nav{color: @nav__color;}

---

Selectors
Devem ser usados apenas classes e elementos HTML, types e estado dos atributos dos elementos FORM, pseudo-classes e pseudo-elementos CSS.
Evitar o uso de seletores de ID!
Sempre utilizar uma quebra de linha após cada seletor, sem espaços antes ou depois deles.
.nav,
.bar {
    color: @color__base;
}


Seletores depreciados

#header { ... }
[data-action="delete"] { ... }
form input[name="password"] { ... }
section[role="main"] { ... }
[role="menu] [role="menuitem"] { ... }
[role="menu] [role="menuitem"].active { ... }


---

Indentação de Combinators ( >, +, ~)
Sempre utilizar espaços antes e depois dos combinators.
.nav + .bar {
    color: @color__base;
}

---

Indentação das Properties
Sempre utilizar espaço após o dois pontos da propriedade. Não antes e, muito menos, sem espaços.
.nav {
    color: @color__base;
    width : @width__base;
    height:@height__base;
}

---

Quebra de linha
Sempre utilizar quebra de linha ao final do arquivo LESS e após cada seletor.
.nav {
    background-color: @nav__background-color;
}
[\n]
.bar {
    background-color: @bar__background-color;
}



---

Nome das classes
Não utilizar notação Camelcase para as classes. Sempre nomes separados por hífen.
.nav-bar { // Correto
    background-color: @nav__background-color;
}

.navBar { // Incorreto
    background-color: @nav__background-color;
}

.nav_bar { // Incorreto
    background-color: @nav__background-color;
}


---

Nome das classes - Helper class
Classes de suporte devem iniciar com underline. O Magento ainda não corrigiu todo o código com esse padrão, mas está no caminho.
._active {
    background-color: @nav__background-color;
}


---

Nome das classes - Significado
Buscar utilizar nome de classes que tragam significado mas que não sejam específicas no estilo.
.category-title { // Correto
    color: black;
}

.button-green { // Correto
    background-color: green;
}



---


Properties
Ordenar para que as propriedades com value de variáveis venham primeiro.
Usar abreviação das propriedades.
Valores com 0 (zero) não precisam de unidade.
Valores flutuantes devem omitir o 0 (zero). Ex: (margin-top: .5rem;)


---

## HTML

Indentação
Sugere-se que sejam indentados sempre com 4 espaços.
Fim do arquivo
A última linha sempre vazia.


---

Comprimento máximo
Linhas de código não devem ultrapassar 120 caracteres. Caso seja necessário, quebrar em várias linhas.

<input data-bind="attr: {
       id: 'cart-item-'+item_id+'-qty',
       'data-item-qty': qty
       }, value: qty"
       type="number"
       size="4"
       class="item-qty cart-item-qty"
      maxlength="12"/>



---

Semântica
Para nomes de atributos, deve-se usar palavras com algum significado, minúsculas e sem abreviação.
Também não se deve utilizar notação Camelcase e nem underline nos nomes.


---



Fechar tags
Sempre fechar tags que sejam autoclose, como <input> e <img>
<img src="image.png" alt="image" />
<input type="text" name="username" />



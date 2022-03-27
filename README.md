Olá essas são minhas notas de aula, de expressões regulares 👍🏻

Utilizando no JavaScript 🌐

- [Site para validação :3](#site-para-validação-3)
- [Marcação](#marcação)
- [Parametros de pesquisa](#parametros-de-pesquisa)
- [Métodos de busca com expressão regular](#métodos-de-busca-com-expressão-regular)
  - [exec](#exec)
  - [test](#test)
- [String - Filtrando a string com expressões regulares](#string---filtrando-a-string-com-expressões-regulares)
  - [match](#match)
  - [replace](#replace)
- [Quantificadores](#quantificadores)
- [Greedy e non-greedy](#greedy-e-non-greedy)
- [Conjuntos](#conjuntos)
- [Ranges](#ranges)
- [Começa e termina Com](#começa-e-termina-com)
- [Retrovisores com match e replace](#retrovisores-com-match-e-replace)
- [Lookahead e Lookaround](#lookahead-e-lookaround)
  - [Lookahead](#lookahead)
  - [Lookaround](#lookaround)
- [Exemplos de uso 🚀](#exemplos-de-uso-)
- [Validando extensões de arquivos jpg - JPG - jpeg - JPEG](#validando-extensões-de-arquivos-jpg---jpg---jpeg---jpeg)
- [Receitas](#receitas)
- [Expressões Regulares - Mozilla](#expressões-regulares---mozilla)

# Site para validação :3

Já vou deixar um site aqui delicinha para você validar suas expressões regulares

[REGEX 101 ](https://regex101.com/)

Sempre que precisar dar aquela validada, chega mais nesse site que ele é muito bom :)

# Marcação

A marcação da expressão regular é o inicio e o fim da expressão marcadas por /. Então uma expressão regular terá a seguinte forma inicial: /expressão/.

A expressão regular pode ser preenchida com grupos, parametros, condicionais e outros, a fim de personalizar sua busca.

# Parametros de pesquisa

Dentro da expressão regular, podemos colocar parametros que nos ajudem a busca os valores que queremos. Alguns desses parametros estão listados abaixos:

- g - Global ( Encontra todas as ocorrencias )
- i - Insensitive
- () Grupos - Podem ser acessados na sequencia com $ e o index
- Exemplo
  ```js
  const texto = 'abcd';
                // 1  2  3  4
  const regExp = /(a)(b)(c)(d)/

  texto.replace(regExp, '$1') // a - Todo o texto foi substituido pelo valor do primeiro grupo, indicado por $1
  ```
- | Ou 


# Métodos de busca com expressão regular

## exec

Retorna um array com objetos ou null caso a expressão não seja encontrada.

- Valor encontrado
- index - Posição que a expressão foi encontrada no texto
- input - Próprio texto de input
- groups - Grupos que foram utilizados

```js
const texto = 'Albert Einstein'
const regExp = /Albert Einstein|Nikola Tesla/

console.log(regExp.exec(texto));
/*
[
  'Albert Einstein',
  index: 0,
  input: 'Albert Einstein',
  groups: undefined
]
*/
```

## test

Retorna booleano quando a expressão regular for encontrada no texto.

```js
const texto = 'abcdefg';
const regExp = /abc/;

console.log(regExp.test(texto)); //true
```

# String - Filtrando a string com expressões regulares

## match

Retorna os valores encontrados ou null

```js
const texto = 'Desafios estão ai para serem ultrapassados'

const regExp = /(Desafios|serem)/gi;

console.log(texto.match(regExp))
```

## replace

```js
const texto = 'desafios estão ai, para serem ultrapassados'

const regExp = /(desafios|serem)/g;

console.log(texto.replace(regExp, 'com toda certeza, $1')) // com toda certeza, desafios estão ai, para com toda certeza, serem ultrapassados


//Exemplo utilizando função
console.log(texto.replace(regExp, (input) => {
  return '#### ' + input + ' ####';
})) //#### desafios #### estão ai, para #### serem #### ultrapassados
```

# Quantificadores

- \* - 0 ou n caracteres
- \+ - 1 ou n caracteres
- ? - 0 ou 1 caracter
- {minimo, maximo}
- {número}
- . Representa qualquer caracter apenas uma vez, exceto uma quebra de linha
- \ escapar o caracter

# Greedy e non-greedy

```js
const html = '<p>Olá mundo!</p> <p>Olá denovo</p>'

console.log(html.match(/<.+>.+<\/.+>/g)) //greedy - ['<p>Olá mundo!</p> <p>Olá denovo</p>']
console.log(html.match(/<.+?>.+?<\/.+?>/g)) // non-greedy - ['<p>Olá mundo!</p>', '<p>Olá denovo</p>']
```

# Conjuntos

São definidos dentro de colchetes

- []
- [^ABC] - Negação do conjunto ABC

```js
const texto = 'ABCDEF';
console.log(texto.match(/[ABC]/));
```

# Ranges

Podemos definir intervalos do menor para o maior, seguindo a seguinte sintaxe [menorValor-maiorValor]

Exemplo Buscando letras e números

```js
const texto = 'abcdef 123456789 10 11 12 13'
console.log(texto.match(/[a-z0-9]+/g)) // [ 'abcdef', '123456789', '10', '11', '12', '13' ]
```
 
> Aqui podemos definir ranges a partir de atalhos, que são os abaixo:

- \w - Todas as letras
- \W - Negação de todas as letras
- \d - Todos números
- \D - Negação de todos os números
- \s - Espaços
- \S - Negação dos espaços

# Começa e termina Com

- ^ - Começa com
- $ - Termina com
- m - Multiline - Valida por linha

# Retrovisores com match e replace

Retrovisores são referencias as posições dos grupos. Utilizando um retrovisor, você pode reutilizar o valor que o grupo referenciado está utilizando. 

Exemplo:

```js
const texto = 'aacccccccccccccc';
const regExp = /(a)(\1)/g;

console.log(texto.match(regExp)); // [aa]

// O grupo (a) tem seu valor reutilizado pelo retrovisor, segundo a referencia \1, que é sua posição
```

# Lookahead e Lookaround

## Lookahead

Checar se existe algo na frente da frase, se existir ele faz oque a expressão regular pede. Por padrão não traz o valor que se usa na condição

- ?= Condição
- ?! Negação da condição

Por exemplo:

```js
const texto = 'abcefg'

console.log(texto.match(/.+(?=e)/g)) // abc - Encontrou o 'e' e trouxe oque a expressão regular pediu
console.log(texto.match(/.+(?=e).+/g)) // abcefg - Encontrou o 'e' e trouxe oque a expressão regular pediu
console.log(texto.match(/.+(?=H)/g)) // null - Não encontrou o 'e' - Logo a expressão regular não obteve valores
```

## Lookaround

Mesma coisa que o lookahead, porém a checagem é feita do começo da frase em vez do final.

- ?<= Condição do lookaround

```js
const texto = 'abcefg'
console.log(texto.match(/(?<=a).+/g)) // bcefg - Checa se existe o 'a' no começo da frase, caso exista a expressão regular trara os dados.
```

# Exemplos de uso 🚀

# Validando extensões de arquivos jpg - JPG - jpeg - JPEG

```js
const arquivos = [
  'arquivo.jpg',
  'arquivo.JPG',
  'arquivo.jpeg',
  'arquivo.JPEG',
]
//? para considerar com ou sem o 'e'
//g para buscar em todos os lugares - Global
//i para buscar com case insensitive
const expReg = /\.(jpe?g)/gi

arquivos.map(arquivo => console.log(arquivo.match(expReg)))
```

# Receitas 

Essas receitas foram pegas do repositório do curso abaixo:

[Curso de JavaScript e TypeScript do básico ao avançado 2022]([https://link](https://www.udemy.com/course/curso-de-javascript-moderno-do-basico-ao-avancado/learn/lecture/17704596#questions))

[Link do repositório do Luiz Otávio](https://github.com/luizomf/regexp)

```js
// Encontra todas as palavras
const palavrasRegEx = /([\wÀ-ú]+)/g

// Não números
const naoNumerosRegEx = /\D/g

// Valida IP
const ipRegExp = /((25[0-5]|2[0-4][0-9]|1\d{2}|[1-9]\d|\d)(\.)){3}(25[0-5]|2[0-4][0-9]|1\d{2}|[1-9]\d|\d)/g;

// Valida CPF
const cpfRegExp = /(?:\d{3}\.){2}\d{3}-\d{2}/g

// Valida telefones
const validaTelefone = /^(\(\d{2}\)\s*)?(9\s*)?(\d{4})-(\d{4})$/g

// Validar senhas fortes
const validaSenhasFortes = /^(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9])(?=.*[!@#$%\]\)]).{8,}$/g

// Validar e-mails
const validaEmail = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
```

Para obter mais informações, por favor acesse a documentação oficial :3

# [Expressões Regulares - Mozilla](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Guide/Regular_Expressions)
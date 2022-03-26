Olá essas são minhas notas de aula, de expressões regulares 👍🏻

Utilizando em JavaScript.

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

Para obter mais informações, por favor acesse a documentação oficial :3

# [Expressões Regulares - Mozilla](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Guide/Regular_Expressions)
<h1 align="center">
<img src="https://raw.githubusercontent.com/Gabrielpatrola/programming-principles/master/DRY/assets/dry-image.png" alt="DRY" width="500"/>
</h1>

<h3 align="center">
  <a href="#-o-que-é">O que é</a>
  <span> · </span>
  <a href="#%EF%B8%8F-definições">Definições</a>
  <span> · </span>
  <a href="#-como-contribuir">Como contribuir</a>
  <span> · </span>
  <a href="#-bibliografia-e-referências">Bibliografia e referências</a>
</h3>

## ⁉ O que é?

DRY é um acronimo para: **D**on't **R**epeat **Y**ourself, que em português significa: Não se repita. É um conceito na área de programação que recomenda a criação de uma funcionalidade dentro de um sistema apenas uma vez e que ela seja reutilizada quantas vezes seja necessária, sem que seja preciso criar ela novamente em outras partes do sistema, evitando assim a duplicidade de código e lógica. A expressão DRY foi utilizada por [Andy Hunt](https://www.google.com/search?sxsrf=AOaemvIxTOD2GJWPN_i3VohUpQJi1ATzPg:1637634288615&q=Andy+Hunt&stick=H4sIAAAAAAAAAOPgE-LUz9U3MM7KjjdWAjPTLPKMkrRkspOt9JPy87P1y4syS0pS8-LL84uyrRJLSzLyixaxcjrmpVQqeJTmlexgZQQASXqTxkUAAAA&sa=X&ved=2ahUKEwjysq2Qt630AhW9rJUCHRvQCl4QmxMoAXoECC4QAw) e [Dave Thomas](https://www.google.com/search?sxsrf=AOaemvIxTOD2GJWPN_i3VohUpQJi1ATzPg:1637634288615&q=Dave+Thomas&stick=H4sIAAAAAAAAAOPgE-LUz9U3MM7KjjdWAjMty1LKDbRkspOt9JPy87P1y4syS0pS8-LL84uyrRJLSzLyixaxcrsklqUqhGTk5yYW72BlBACct2HlRwAAAA&sa=X&ved=2ahUKEwjysq2Qt630AhW9rJUCHRvQCl4QmxMoAnoECC4QBA) no livro "O Programador Pragmático: De Aprendiz a Mestre",


## ✍️ Definições

Antes de tudo, é necessário entender que não faz sentido a existência de uma mesma porção de código em diversos lugares de uma aplicação, pois isso tem como consequência um aumento desnecessário no tamanho da aplicação e também aumenta o trabalho para a manutenção do sistema, pois uma pequena mudança as vezes terá que ser replicada em mais de um ponto e caso a mudança não seja feita em todos os pontos, isso poderá abrir brecha para bugs inesperados.

Aplicando esse conceito de maneira efetiva, uma mudança de lógica dentro do sistema irá ser replicada de maneira previsível e uniforme, o que irá refletir em um sistema funcional e de fácil manutenção. Lembre-se você escreve código para que outras pessoas possam utilizar ele, portanto leve isso sempre em consideração na hora de desenvolver alguma solução ou tarefa.

### 👾 Exemplos

Exemplo em js:

Imaginando que em um sistema tenha um formulário de login e de cadastro de usuário, nos dois formulários será necessário validar se o e-mail fornecido é válido. Abaixo será apresentado dois exemplos: um onde o DRY não é utilizado e outro onde o DRY é utilizado

#### 🐛 Exemplo onde o DRY não é utilizado

Na porção de código abaixo é criado uma constante chamada `validateEmail` para validar o e-mail antes de fazer a lógica de autenticação do usuário.
```js
// auth/login.js
const validateEmail = (email) => /\S+@\S+\.\S+/.test(email)

function login (email, password) {
    const isEmailValid = validateEmail(email);

    if(isEmailValid){
        try {
            /** Lógica para fazer login */
        }catch(error){
            /** Lógica para erro no login */
        }
    }

}
```

Já na parte abaixo, é criado novamente a mesma constante para fazer uma validação antes de criar um novo usuário.

```js
// auth/register.js
const validateEmail = (email) => /\S+@\S+\.\S+/.test(email)

function register (email, password) {
    const isEmailValid = validateEmail(email);

    if(isEmailValid){
        try {
            /** Lógica para fazer registro */
        }catch(error){
            /** Lógica para erro no registro */
        }
    }

```

Os códigos acima servem apenas para demonstrar como uma lógica pode acabar sendo refeita em partes diferentes dentro de uma aplicação. Gerando um retrabalho em uma modificação ou implementação de lógica nova.

#### 🚀 Exemplo utilizando DRY

Primeiro, será necessário extrair a função de validar e-mail para um arquivo separado, para que ela seja posteriomente importada e reutilizada.

```js
// utils/formValidator.js

/**
 * Return if the email
 * is a valid one
 * @param {String} email The user's email
 */
export const validateEmail = (email) => /\S+@\S+\.\S+/.test(email);
```

```js
// auth/login.js
import { validateEmail } from 'utils/formValidator'

function login (email, password) {
    const isEmailValid = validateEmail(email);

    if(isEmailValid){
        try {
            /** Lógica para fazer login */
        }catch(error){
            /** Lógica para erro no login */
        }
    }

}
```

```js
// auth/register.js

import { validateEmail } from 'utils/formValidator'

function register (email, password) {
    const isEmailValid = validateEmail(email);

    if(isEmailValid){
        try {
            /** Lógica para fazer registro */
        }catch(error){
            /** Lógica para erro no registro */
        }
    }

```

Como pode ser visto acima, o método `validateEmail` foi utilizado em duas funções diferentes em arquivos distintos de um jeito bem simples, agora caso o método seja alterado, a lógica será replicada no login e no cadastro.


## 💪 Como contribuir

Basta criar um fork do projeto, realizar as modificações que achar necessário e depois fazer um Pull Request.
Toda ajuda é bem vinda, caso veja algum erro, não hesite em contribuir com o projeto!

## 📚 Bibliografia e referências

Conteúdos em português:

Artigos:
- [Não Se Repita (DRY Don’t Repeat Yourself)](https://medium.com/@rafaelsouzaim/n%C3%A3o-se-repita-dry-dont-repeat-yourself-40da33289bcf)
- [O princípio do “Não se repita” (DRY)](https://www.profissionaisti.com.br/o-principio-do-nao-se-repita-dry/)
- [O que são os princípios DRY, KISS e YAGNI?](https://pt.stackoverflow.com/questions/23052/o-que-s%C3%A3o-os-princ%C3%ADpios-dry-kiss-e-yagni)
- [OOD: DRY para humanos (com exemplos)](https://adrianolisboa.com/ood-dry-para-humanos-com-exemplos/)
Vídeos:
- [145 - DRY (Don't Repeat Yourself!) e a Regra de Três da Duplicação](https://www.youtube.com/watch?v=uRih-n6jDbw)
- [DRY, KISS, YAGNI | Code/Drops #27](https://www.youtube.com/watch?v=5yJ_cAUrpQcA)

Conteúdos em inglês:

Vídeos:
- [Programming Terms: DRY (Don't Repeat Yourself)](https://www.youtube.com/watch?v=IGH4-ZhfVDk)

Artigos:
- [Don't repeat yourself](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)
- [The DRY Principle: Benefits and Costs with Examples](https://thevaluable.dev/dry-principle-cost-benefit-example/)
- [DRY - Don’t repeat yourself](https://blog.oliverjumpertz.dev/dry-dont-repeat-yourself)
- [Orthogonality and the DRY Principle A Conversation with Andy Hunt and Dave Thomas, Part II](https://www.artima.com/articles/orthogonality-and-the-dry-principle)

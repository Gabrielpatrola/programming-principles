<h1 align="center">
<img src="https://raw.githubusercontent.com/Gabrielpatrola/programming-principles/master/SOLID/assets/solid.jpeg" alt="Solid" width="500"/>
</h1>

<h3 align="center">
  <a href="#-o-que-e">O que é</a>
  <span> · </span>
  <a href="#-definicoes">Definições</a>
  <span> · </span>
  <a href="#-como-contribuir">Como contribuir</a>
  <span> · </span>
  <a href="#-bibliografia-e-referencias">Bibliografia e referências</a>
</h3>

## ⁉ O que é?

SOLID é um acrônimo de 5 princípios da programação orientada a objetos, são eles:

- **S**ingle Responsability Principle (Princípio da responsabilidade única)
- **O**pen/Closed Principle (Princípio aberto/fechado)
- **L**iskov Substitution Principle (Princípio da substituição de Liskov)
- **I**nterface Segregation Principle (Princípio da segregação da interface)
- **D**ependency Inversion Principle (Princípio da inversão da dependência)

## 💯 Definições

### Single Responsability Principle (Princípio da responsabilidade única)
<p align="center">
<img src="https://raw.githubusercontent.com/Gabrielpatrola/programming-principles/master/SOLID/assets/first.jpg" alt="First principle" width="500"/><br>
Sua classe não deve ter mais de uma responsabilidade
</p>

> Uma classe deve ter uma e apenas uma razão para mudança, significando que uma classe deve ter apenas uma responsabilidade.

Esse princípio declara que uma classe deve ser especializada em um único assunto e possuir apenas uma responsabilidade dentro do software, ou seja, a classe deve ter uma única tarefa ou ação para executar.

- Exemplo em PHP
```php
/** Exemplo que não segue o princípio */
class UserRegistrationController
{
    public function register(Request $request, Response $response)
    {
        $user = $this->createUser($request);
         
        $this->database->query("insert into users ...");
 
        $this->email
            ->to($user->email())
            ->subject("Welcome")
            ->send();
 
        return $this->successfulResponse($response)
    }
}
```

```php
/** Exemplo que segue o princípio */
class UserRegistration
{
    public function __construct(RegistrationStorage $storage, RegistrationEmail $email) 
    {
        $this->storage = $storage;
        $this->email = $email;
    }
 
    public function register(User $user)
    {
        $this->storage->save($user);
        $this->email->sendTo($user);
    }
}

```

- Exemplo em JS

```js

```

- Objetivo:
Este princípio visa separar comportamentos para que, se surgirem bugs como resultado de sua mudança, isso não afete outros comportamentos não relacionados.

### Open/Closed Principle (Princípio aberto/fechado)

> Objetos ou entidades devem ser abertas para extensão, mas fechadas para modificação.

- Exemplo em PHP
```php
/** Exemplo que não segue o princípio */
abstract class Duck 
{
    public function swim(){...}
    public function quack(){...}
    public function fly(){...}
}
 
class CityDuck extends Duck {...}
class WildDuck extends Duck {...}
class RubberDuck extends Duck {...}
class WoodenDuck extends Duck {...}
```

```php
/** Exemplo que segue o princípio */
interface Swimming { public function swim(); }
interface Quacking { public function makeNoise(); }
interface Flying { public function fly(); }
 
class WildDuck implements Quacking 
{
    public function makeNoise() 
    {
        $this->quacking->makeNoise();
    }
}
 
class RubberDuck 
{
    function __construct (Swimming $swimming, Quacking $quacking, Flying $flying)
    {
        $this->swimming = $swimming;
        $this->quacking = $quacking;
        $this->flying = $flying;
    }
     
    public function quack () 
    {
        $this->quacking->makeNoise();
    }
}

class Squeaking implements Quacking () 
{
    public function makeNoise(){}
}

New RubberDuck(new Swimming, new Squeaking, new Flying);
```

- Exemplo em JS

```js

```

- Objetivo:
Este princípio visa estender o comportamento de uma classe sem alterar o comportamento existente dessa classe. Isso evita causar bugs onde quer que a classe esteja sendo usada.

### Liskov Substitution Principle (Princípio da substituição de Liskov)

> Uma classe derivada deve ser substituída por sua classe base.

- Exemplo em PHP
```php
/** Exemplo que não segue o princípio*/
<?php

class Rectangle
{
    protected $height;
    protected $width;

    public function setHeight(int $height)
    {
        $this->height = $height;
    }

    public function setWidth(int $width)
    {
        $this->width = $width;
    }
}
class Square extends Rectangle
{
    public function setHeight(int $height)
    {
        $this->height = $height;
        $this->width = $height;
    }

    public function setWidth(int $width)
    {
        $this->height = $width;
        $this->width = $width;
    }
}

/** Exemplo que segue o princípio*/
<?php

abstract class AbstractShape
{
    abstract public function Area() : int;
}

class Rectangle extends AbstractShape
{
    private $height;
    private $width;

    public function setHeight(int $height)
    {
        $this->height = $height;
    }

    public function setWidth(int $width)
    {
        $this->width = $width;
    }

    public function Area() : int
    {
        return $this->height * $this->width;
    }
}

class Square extends AbstractShape
{
    private $sideLength;

    public function setSideLength(int $sideLength)
    {
        $this->sideLength = $sideLength;
    }

    public function Area() : int
    {
        return $this->sideLength * $this->sideLength;
    }
}
```

- Exemplo em JS

```js

```

- Objetivo:
Este princípio visa reforçar a consistência para que a classe pai ou sua classe filha possam ser usadas da mesma maneira sem erros.

### Interface Segregation Principle (Princípio da segregação da interface)

> Os clientes não devem ser forçados a depender de métodos que não usam.

- Exemplo em PHP
```php
/** Exemplo que não segue o princípio */
<?php

interface Bird 
{
    public function eat();
    public function fly();
}

/** Classe de uma andorinha */
class Swallow implements Bird
{
    public function eat() { ... }
    public function fly() { ... }
}

/** Classe de um Avestruz **/
class Ostrich implements Bird
{
    public function eat() { ... }
    public function fly() { /* exception */ }
}

/** Exemplo que segue o princípio */

<?php

interface Bird
{
    public function eat();
}

interface FlyingBird 
{
    public function fly();
}

interface RunningBird 
{
    public function run();
}

class Swallow implements Bird, FlyingBird
{
    public function eat() { ... }
    public function fly() { ... }
}

class Ostrich implements Bird, RunningBird 
{
    public function eat() { ... }
    public function run() { ... }
}
```

- Exemplo em JS

```js

```
- Objetivo:
Este princípio visa dividir um conjunto de ações em conjuntos menores, de forma que uma Classe execute SOMENTE o conjunto de ações de que necessita.

### Dependency Inversion Principle (Princípio da inversão da dependência)

> Uma classe não deve ser misturada com a ferramenta que usa para executar uma ação. Em vez disso, deve ser implementada na interface que permitirá que a ferramenta se conecte à classe

- Exemplo em PHP
```php
/** Exemplo que não segue o princípio */
<?php

use MySQLConnection;

class PasswordReminder
{
    private $dbConnection;
    
    public function __construct(MySQLConnection $dbConnection)
    {       
        $this->dbConnection = $dbConnection;           
    }
    
    // Faz alguma coisa
}

/** */
<?php

interface DBConnectionInterface
{
    public function connect();
}


class MySQLConnection implements DBConnectionInterface
{
    public function connect()
    {
        // ...
    }
}

class OracleConnection implements DBConnectionInterface
{
    public function connect()
    {
        // ...
    }
}

class PasswordReminder
{
    private $dbConnection;

    public function __construct(DBConnectionInterface $dbConnection) {
        $this->dbConnection = $dbConnection;
    }
  
    // Faz alguma coisa
}

```

- Exemplo em JS

```js

```

- Objetivo:
Este princípio visa reduzir a dependência de uma classe de alto nível na classe de baixo nível, introduzindo uma interface.

## 💪 Como contribuir

Basta criar um fork do projeto, realizar as modificações que achar necessário e depois fazer um Pull Request.
Toda ajuda é bem vinda, caso veja algum erro, não hesite em contribuir com o projeto!

## 📚 Bibliografia e referências

Conteúdos em português:

Artigos:
- [SOLID com PHP](https://imasters.com.br/back-end/solid-com-php)
- [Princípios SOLID de design para JavaScript](https://www.infoq.com/br/news/2014/02/solid-principios-javascript/)
- [O que é SOLID: O guia completo para você entender os 5 princípios da POO](https://medium.com/desenvolvendo-com-paixao/o-que-é-solid-o-guia-completo-para-você-entender-os-5-princípios-da-poo-2b937b3fc530)

Vídeos:
- [Princípios SOLID em uma API REST com Node.js e TypeScript](https://www.youtube.com/watch?v=vAV4Vy4jfkc)
- [SOLID (O básico para você programar melhor)](https://www.youtube.com/watch?v=mkx0CdWiPRA)
- [SOLID fica FÁCIL com Essas Ilustrações](https://www.youtube.com/watch?v=6SfrO3D4dHM)

Conteúdos em inglês:

Artigos:
- [The Principles of OOD](http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod)
- [SOLID Principles In PHP](https://www.hashbangcode.com/article/solid-principles-php)
- [The S.O.L.I.D Principles in Pictures](https://medium.com/backticks-tildes/the-s-o-l-i-d-principles-in-pictures-b34ce2f1e898)
- [S.O.L.I.D The first 5 principles of Object Oriented Design with JavaScript](https://medium.com/@cramirez92/s-o-l-i-d-the-first-5-priciples-of-object-oriented-design-with-javascript-790f6ac9b9fa)
- [SRP: The Single Responsibility Principle](https://drive.google.com/file/d/0ByOwmqah_nuGNHEtcU5OekdDMkk/view)

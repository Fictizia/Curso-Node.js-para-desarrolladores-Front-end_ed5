# Clase 7

### Testing Unitario

> Una prueba unitaria es una forma de comprobar el correcto funcionamiento de una unidad de código.
Esto sirve para asegurar que cada unidad funcione correctamente y eficientemente por separado.

Además de verificar que el código hace lo que tiene que hacer, comprobamos:
- Que sea correcto el nombre
- Parámetros
- Tipo de lo que se devuelve
- Entrada/Salida
- ...

La idea es escribir casos de prueba para cada función no trivial o método en el módulo, de forma que cada caso sea independiente del resto.
Luego, con las **Pruebas de Integración**, se podrá asegurar el correcto funcionamiento del sistema o subsistema en cuestión.

### TDD

> Desarrollo guiado por pruebas de software, o Test-driven development (TDD) es una práctica de ingeniería de software que involucra otras dos prácticas: Escribir las pruebas primero (Test First Development) y Refactorización (Refactoring).
En primer lugar, se escribe una prueba y se verifica que las pruebas fallan. A continuación, se implementa el código que hace que la prueba pase satisfactoriamente y seguidamente se refactoriza el código escrito.

![tdd](https://www.paradigmadigital.com/wp-content/uploads/2017/04/TDD-6.png)

- Primero los test
- Depués el código (Refactorización <-> Testing)

**Ciclo de Vida**:
1. Escribe los tests
1. Ejecuta y comprueba que fallan
1. Escribe el código para que pasen los tests.
1. Ejecuta los tests
1. Refactoriza
1. Repite

### Algunos datos recientes

![frameworks](https://cdn.pbrd.co/images/HbAydYs.png)

### Combo Breaker

![combo](https://cdn-images-1.medium.com/max/2000/1*AjcpO5fXga08mo2AJU93uQ.png)

**Mocha + Chai + Node.js** ([unit testing + TDD in Node.js](https://www.codementor.io/davidtang/unit-testing-and-tdd-in-node-js-part-1-8t714s877))

#### Mocha

![mocha](https://hackage.haskell.org/package/reload-0.0.0.1/src/web/bower_components/mocha/assets/mocha-banner.svg)

Mocha es un framework de testing para JavaScript que funciona sobre Node.js y/o en el navegador. Los tests de Mocha se ejecutan en serie, permitiendo obtener un reporte completo y sencillo.

**Primeros pasos**:
- [Browser](https://mochajs.org/#running-mocha-in-the-browser)
- [Node.js](https://mochajs.org/#installation)

**Instalación en Node.js**:

```
$ npm install --save-dev mocha
```

**Ejecutar tests en un directorio**:

```
$ mocha tests/*.js
```

**Utilizando babel**:

```
$ mocha --compilers js:babel-core/register -r babel-polyfill tests/*.js
```

**Definiendo tests**:

- `describe`: Sirve para agrupar tests, podríamos decir que sirve para definir una suite de tests.

  ```javascript
  describe('Array', () => {
    // Test code
  });
  ```

- `it`: Define un test

  ```javascript
  it('receives two params', () => {
    // Test code
  });
  ```

  ```javascript
  it('receives two params', (callback) => {
    // Async test code
    callback();
  });
  ```

- `before`: Se ejecuta una única vez antes de empezar la suite (puede agruparse dentro de un `describe`)

  ```javascript
  before(() => {
    // Prepare the suite
  });
  ```

- `after`: Se ejecuta una única vez después de terminar la suite (puede agruparse dentro de un `describe`)

  ```javascript
  after(() => {
    // Suite teardown
  });
  ```

- `beforeEach`: Se ejecuta antes de empezar cada test (puede agruparse dentro de un `describe`)

  ```javascript
  beforeEach('Array', () => {
    // Prepare the test
  });
  ```

- `afterEach`: Se jecuta después de terminar cada test (puede agruparse dentro de un `describe`)

  ```javascript
  afterEach('Array', () => {
    // Test teardown
  });
  ```

[Explain Mocha's testing framework - describe(), it() and before()/etc hooks](https://gist.github.com/samwize/8877226)

#### Chai

![chai](http://zhigalov.github.io/testable-code-01/images/chai.png)

Chai es una librería de aserciones, similar al [assert de Node.js](https://nodejs.org/api/assert.html).
Simplifica el test proporcionando muchas aserciones con las que probar el código.

[Chai API](http://chaijs.com/api/)

**Utilizando `expect`**:

```javascript
const expect = require('chai').expect;
const myFuntion = require('./my-function');

it('returns a String', () => {
  const result = myFuntion();

  expect(result).to.be.a('string');
});
```

**Utilizando `assert`**:

```javascript
const assert = require('chai').assert;
const myFuntion = require('./my-function');

it('returns a String', () => {
  const result = myFuntion();

  assert.typeOf(result, 'string', 'we have a string');
});
```

### Fakes (mock, spy, stub)

### Sinon.js

![sinon](https://i2.wp.com/blog.fossasia.org/wp-content/uploads/2017/07/sinon.jpg?resize=592%2C266&ssl=1)

**Sinon + Chai**:

```javascript
var chai = require('chai');
var sinon = require('sinon');
var sinonChai = require("sinon-chai");
chai.use(sinonChai);
global.expect = chai.expect;
global.sinon = sinon;
```
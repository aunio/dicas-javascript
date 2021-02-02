# dicas-javascript

1. [Múltiplas Condições](#multiplas-condicoes)
2. [Ternários](#ternarios)

## **Múltiplas Condições**

Se você tem muitas condições para uma mesma variável, pode usar o método a seguir

**Ruim:**

```javascript
// Troque isso
if(x === 'abc' || x === 'def' || x === 'ghi' || x === 'jkl') {
    // qualquer coisa
}
```

**Bom:**

```javascript
// Por isso
if(['abc', 'def', 'ghi', 'jkl'].includes(x)) {
    // qualquer coisa
}
```

**[⬆ Voltar ao início](#dicas-javascript)**

## **Ternários**

Isto pode reduzir muito seus códigos.
Tire esse boiler plate de if...else e usa mais ternários.

**Ruim:**

```javascript
// Troque isso
let test: boolean;
if( x > 10 ) {
    test = true;
} else {
    test = false;
}
```

**Bom:**

```javascript
// Por isso
let test = (x > 10) ? true : false;

// Ou isso
let test = x > 10;

console.log(test);
// log: true
```

**[⬆ Voltar ao início](#dicas-javascript)**
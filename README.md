# dicas-javascript

1. [Múltiplas Condições](#multiplas-condicoes)

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
# dicas-javascript

1. [Múltiplas Condições](#multiplas-condicoes)

## **Múltiplas Condições**

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
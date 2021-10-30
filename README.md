# javascript-tips

1. [Multiple Conditions](#multiple-conditions)
2. [Ternary Operator](#ternary-operator)
3. [Date](#date)
4. [If Validation](#if-validation)
5. [Array Order Alphabetically](#array-order-alphabetically)
6. [Foreach Loop](#foreach)
7. [Filter](#filter)
8. [Pipe](#pipe)
9. [Spread](#pipe)

## **Multiple Conditions**

**Bad:**

```javascript
let x = "abc";

if (x === "abc" || x === "def" || x === "ghi" || x === "jkl") {
  // code
}
```

**Good:**

```javascript
let x = "abc";

if (["abc", "def", "ghi", "jkl"].includes(x)) {
  // code
}
```

**[⬆ Back to the top](#javascript-tips)**

## **Ternary Operator**

**Bad:**

```javascript
let x = 20;

if (x > 10) {
  test = true;
} else {
  test = false;
}

console.log(test); //true
```

**Good:**

```javascript
let x = 20;

// Option 1
let test1 = x > 10 ? true : false;
console.log(test1); //true

// Option 2
let test2 = x > 10;
console.log(test2); //true
```

**[⬆ Back to the top](#javascript-tips)**

## **Date**

**Bad:**

```javascript
const regex = /^([0-9]{4})[-](0[1-9]|1[0-2])[-](0[0-9]|1[0-9]|2[0-9]|3[0-1])/;
const date = new Date(2021, 0, 1);
const [full, year, month, day] = regex.exec(date.toISOString());

newDate = `${day}/${month}/${year}`;
console.log(newDate); // 01/01/2021
```

**Good:**

```javascript
const options = {
  year: "numeric",
  month: "long",
  day: "numeric",
};

const date = new Date(2021, 0, 1);

newDate1 = date.toLocaleDateString("pt-br", options);
console.log(newDate1); // 1 de janeiro de 2021

newDate2 = date.toLocaleDateString("pt-br", { ...options, month: "numeric" });
console.log(newDate2); // 01/01/2021
```

**[⬆ Back to the top](#javascript-tips)**

## **If Validation**

**Bad:**

```javascript
function identifyAnimal(animal) {
  if (animal === "Dog") {
    return "Pluto";
  } else if (animal === "Cat") {
    return "Tom";
  } else if (animal === "Mouse") {
    return "Jerry";
  } else if (animal === "Duck") {
    return "Donald";
  }
}

console.log(identifyAnimal("Dog")); // Pluto
```

**Good:**

```javascript
function identifyAnimal(animal) {
  const animals = {
    Dog: "Pluto",
    Cat: "Tom",
    Mouse: "Jerry",
    Duck: "Donald",
  };

  return animals[animal];
}

console.log(identifyAnimal("Dog")); // Pluto
```

**[⬆ Back to the top](#javascript-tips)**

## **Array Order Alphabetically**

Sorting strings with numbers and accented characters.

```javascript
const movies = [
  "Harry Potter",
  "Senhor dos Anéis",
  "Árvore da Vida",
  "As Branquelas",
  "8 Mile - Rua das Ilusões",
];

console.log(movies.sort(Intl.Collator().compare));

/* [
    "8 Mile - Rua das Ilusões",
    "Árvore da Vida",
    "As Branquelas",
    "Harry Potter",
    "Senhor dos Anéis"
] */
```

**[⬆ Back to the top](#javascript-tips)**

## **Foreach**

Foreach Loop is a control flow statement for traversing items in a collection.

```javascript
const pokemons = [
  { id: 1, name: "Bulbasaur", type: { primary: "Grass", secondary: "Poison" } },
  { id: 2, name: "Ivysaur", type: { primary: "Grass", secondary: "Poison" } },
  { id: 3, name: "Venusaur", type: { primary: "Grass", secondary: "Poison" } },
  { id: 4, name: "Charmander", type: { primary: "Fire", secondary: null } },
  { id: 5, name: "Charmeleon", type: { primary: "Fire", secondary: null } },
  { id: 6, name: "Charizard", type: { primary: "Fire", secondary: "Flying" } },
  { id: 7, name: "Squirtle", type: { primary: "Water", secondary: null } },
  { id: 8, name: "Wartotle", type: { primary: "Water", secondary: null } },
  { id: 9, name: "Blastoise", type: { primary: "Water", secondary: null } },
];
```

**Bad:**

```javascript
//forLoop
for (let i = 0; i < pokemons.length; i++) {
  console.log(pokemons[i]);
}

/*
    { id:1, name:"Bulbasaur", type: { primary:"Grass", secondary:"Poison" } }
    { id:2, name:"Ivysaur", type: { primary:"Grass", secondary:"Poison" } }
    { id:3, name:"Venusaur", type: { primary:"Grass", secondary:"Poison" } }
    { id:4, name:"Charmander", type: { primary:"Fire", secondary:null } }
    { id:5, name:"Charmeleon", type: { primary:"Fire", secondary:null } }
    { id:6, name:"Charizard", type: { primary:"Fire", secondary:"Flying" } }
    { id:7, name:"Squirtle", type: { primary:"Water", secondary:null } }
    { id:8, name:"Wartotle", type: { primary:"Water", secondary:null } }
    { id:9, name:"Blastoise", type: { primary:"Water", secondary:null } }
*/
```

**Good:**

```javascript
//forEach
pokemons.forEach((pokemon) => {
  console.log(pokemon);
});

/*
    { id:1, name:"Bulbasaur", type: { primary:"Grass", secondary:"Poison" } }
    { id:2, name:"Ivysaur", type: { primary:"Grass", secondary:"Poison" } }
    { id:3, name:"Venusaur", type: { primary:"Grass", secondary:"Poison" } }
    { id:4, name:"Charmander", type: { primary:"Fire", secondary:null } }
    { id:5, name:"Charmeleon", type: { primary:"Fire", secondary:null } }
    { id:6, name:"Charizard", type: { primary:"Fire", secondary:"Flying" } }
    { id:7, name:"Squirtle", type: { primary:"Water", secondary:null } }
    { id:8, name:"Wartotle", type: { primary:"Water", secondary:null } }
    { id:9, name:"Blastoise", type: { primary:"Water", secondary:null } }
*/
```

**[⬆ Back to the top](#javascript-tips)**

## **Filter**

The filter() method creater a new array with all the elements that pass the test implemented by the callback() function.

```javascript
const pokemons = [
  { id: 1, name: "Bulbasaur", type: { primary: "Grass", secondary: "Poison" } },
  { id: 2, name: "Ivysaur", type: { primary: "Grass", secondary: "Poison" } },
  { id: 3, name: "Venusaur", type: { primary: "Grass", secondary: "Poison" } },
  { id: 4, name: "Charmander", type: { primary: "Fire", secondary: null } },
  { id: 5, name: "Charmeleon", type: { primary: "Fire", secondary: null } },
  { id: 6, name: "Charizard", type: { primary: "Fire", secondary: "Flying" } },
  { id: 7, name: "Squirtle", type: { primary: "Water", secondary: null } },
  { id: 8, name: "Wartotle", type: { primary: "Water", secondary: null } },
  { id: 9, name: "Blastoise", type: { primary: "Water", secondary: null } },
];
```

**Bad:**

```javascript
//forLoop
let filterPokemons = [];
for (let i = 0; i < pokemons.length; i++) {
  if (pokemons[i].type.primary === "Fire") {
    filterPokemons.push(pokemons[i]);
  }
}

/*
    { id:4, name:"Charmander", type: { primary:"Fire", secondary:null } }
    { id:5, name:"Charmeleon", type: { primary:"Fire", secondary:null } }
    { id:6, name:"Charizard", type: { primary:"Fire", secondary:"Flying" } }
*/
```

**Good:**

```javascript
//filter()
let filterPokemons = pokemons.filter(
  (pokemon) => pokemon.type.primary === "Fire"
);
console.log(filterPokemons);

/*
    { id:4, name:"Charmander", type: { primary:"Fire", secondary:null } }
    { id:5, name:"Charmeleon", type: { primary:"Fire", secondary:null } }
    { id:6, name:"Charizard", type: { primary:"Fire", secondary:"Flying" } }
*/
```

**[⬆ Back to the top](#javascript-tips)**

## **Pipe**

```javascript
const plusTen = (number) => number + 10;
const dividedByFive = (number) => number / 5;
const multipliedByThree = (number) => number * 3;
const minusTwo = (number) => number - 2;

const combineOperations = (initValue, arrOfFuncs) =>
  arrOfFuncs.reduce((acc, func) => func(acc), initValue);

console.log(
  combineOperations(5, [plusTen, dividedByFive, multipliedByThree, minusTwo])
);

// 7
```

**[⬆ Back to the top](#javascript-tips)**

## **Spread**

Arrays Copy

```javascript
let arr = ['a', 'b', 'c']
```

**Bad:**

```javascript
let arr2 = arr
arr2.push('d')
console.log(arr) // ['a', 'b', 'c', 'd']
console.log(arr2) // ['a', 'b', 'c', 'd']
```

**Good:**

```javascript
let arr2 = [...arr]
arr2.push('d')
console.log(arr) // ['a', 'b', 'c']
console.log(arr2) // ['a', 'b', 'c', 'd']
```

**[⬆ Back to the top](#javascript-tips)**

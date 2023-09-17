# javascript-tips

1.  [Array em ordem alfabética](#array-em-ordem-alfabética)
2.  [Array.at()](#array-at)
3.  [Date](#date)
4.  [Deep Clone](#deep-clone)
5.  [Filter](#filter)
6.  [Foreach Loop](#foreach)
7.  [Group and GroupMap](#group-and-groupmap)
8.  [If Validation](#if-validation)
9.  [Immutable Reverse](#immutable-reverse)
10. [Immutable Sort](#immutable-sort)
11. [Immutable Splice](#immutable-splice)
12. [Multiple Conditions](#multiple-conditions)
13. [Number Format](#number-format)
14. [Object Literals](#object-literals)
15. [Pipe](#pipe)
16. [Promise](#promise)
17. [Spread](#spread)
18. [Ternary Operator](#ternary-operator)
19. [Using URL Instead of String](#using-url-instead-of-string)

## **Array em ordem alfabética**

Permite deixar um array em ordem afabética levando em consideração letras com acentuação

```javascript
const movies = [
  "Harry Potter",
  "Senhor dos Anéis",
  "Árvore da Vida",
  "As Branquelas",
  "8 Mile - Rua das Ilusões",
];

console.log(movies.sort(Intl.Collator().compare));

/* 
  [
    "8 Mile - Rua das Ilusões",
    "Árvore da Vida",
    "As Branquelas",
    "Harry Potter",
    "Senhor dos Anéis"
  ]
*/
```

**[⬆ Back to the top](#javascript-tips)**

## **Array at**

Allows us to search for an item by its index

**Array:**

```javascript
let arr = [1, 2, 3, 4, 5, 6, 7, 9];
```

**Bad:**

```javascript
arr[arr.length - 1]; // 9
```

**Good:**

```javascript
arr.at(-1); // 9
```

**[⬆ Back to the top](#javascript-tips)**

## **Date**

**Bad:**

```javascript
const regex = /^([0-9]{4})[-](0[1-9]|1[0-2])[-](0[0-9]|1[0-9]|2[0-9]|3[0-1])/;
const date = new Date(2021, 0, 1);
const [full, year, month, day] = regex.exec(date.toISOString());

let newDate = `${day}/${month}/${year}`;
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

let newDate1 = date.toLocaleDateString("pt-br", options);
console.log(newDate1); // 1 de janeiro de 2021

let newDate2 = date.toLocaleDateString("pt-br", {
  ...options,
  month: "numeric",
});
console.log(newDate2); // 01/01/2021
```

**[⬆ Back to the top](#javascript-tips)**

## **Deep Clone**

**Object:**

```javascript
const strawHatPiratesShip = {
  name: "Going Merry",
  debut: {
    chapter: 41,
    episode: 17,
  },
};

const copiedStrawHatPiratesShip = structuredClone(strawHatPiratesShip);

copiedStrawHatPiratesShip.name = "Thousand Sunny";
copiedStrawHatPiratesShip.debut.chapter = 436;
copiedStrawHatPiratesShip.debut.episode = 321;

console.log(strawHatPiratesShip);

/*
  {
    name: "Going Merry"
    debut: {
      chapter: 41,
      episode: 17,
    },
  }
*/

console.log(copiedStrawHatPiratesShip);

/*
  {
    name: "Thousand Sunny"
    debut: {
      chapter: 436,
      episode: 321,
    },
  }
*/
```

**Array:**

```javascript
const strawHatPirates = [
  {
    name: "Monkey D. Luffy",
    birthday: {
      day: 5,
      month: "May",
    },
  },
  {
    name: "Roronoa Zoro",
    birthday: {
      day: 11,
      month: "November",
    },
  },
];

const copiedStrawHatPirates = structuredClone(strawHatPirates);

copiedStrawHatPirates[0].name = "Nami";
copiedStrawHatPirates[0].birthday.day = 3;
copiedStrawHatPirates[0].birthday.month = "July";
copiedStrawHatPirates[1].name = "Usopp";
copiedStrawHatPirates[1].birthday.day = 1;
copiedStrawHatPirates[1].birthday.month = "April";

console.log(strawHatPirates);

/*
  [{
    name: "Monkey D. Luffy",
    birthday: {
      day: 5,
      month: "May"
    },
  }, {
    name: "Roronoa Zoro",
    birthday: {
      day: 11,
      month: "November"
    },
  }]
*/

console.log(copiedStrawHatPirates);

/*
  [{
    name: "Nami"
    birthday: {
      day: 3,
      month: "July"
    },
  }, {
    name: "Usopp"
    birthday: {
      day: 1,
      month: "April"
    },
  }]
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

## **Group and GroupMap**

```javascript
const numbers = [1, 2, 3, 4, 5, 6];
numbers.group((num) => (num % 2 === 0 ? "Even" : "Odd"));
console.log(numbers);
/*
  {
    Odd: [1, 3, 5],
    Even: [2, 4, 6]
   }
*/
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

## **Immutable Reverse**

```javascript
const sequentialNumbers = [1, 2, 3];
sequentialNumbers.toReversed(); // [3, 2, 1]
console.log(sequentialNumbers); // [1, 2, 3]
```

**[⬆ Back to the top](#javascript-tips)**

## **Immutable Sort**

```javascript
const outOfOrder = new Uint8Array([3, 1, 2]);
outOfOrder.toSorted(); // Uint8Array [1, 2, 3]
console.log(outOfOrder); // Uint8Array [3, 1, 2]
```

**[⬆ Back to the top](#javascript-tips)**

## **Immutable Splice**

```javascript
const numbers = [1, 2, 3];
numbers.toSpliced(2, 2); // [3]
console.log(numbers); // numbers [1, 2, 3]
```

**[⬆ Back to the top](#javascript-tips)**

## **Multiple Conditions**

**Bad:**

```javascript
let shinobi = "Naruto";

if (
  shinobi === "Naruto" ||
  shinobi === "Kakashi" ||
  shinobi === "Minato" ||
  shinobi === "Jiraiya"
) {
  // code
}
```

**Good:**

```javascript
let shinobi = "Naruto";

if (["Naruto", "Kakashi", "Minato", "Jiraiya"].includes(shinobi)) {
  // code
}
```

**[⬆ Back to the top](#javascript-tips)**

## **Number Format**

```javascript
const number = 12345;

const euro = new Intl.NumberFormat("de-DE", {
  style: "currency",
  currency: "EUR",
}).format(number);
console.log(euro); // 12.345,00 €

const dollar = new Intl.NumberFormat("en-US", {
  style: "currency",
  currency: "USD",
  currencyDisplay: "name",
}).format(number);
console.log(dollar); // 12,345.00 US dollars

const liter = new Intl.NumberFormat("en-US", {
  style: "unit",
  unit: "liter",
  unitDisplay: "long",
}).format(number);
console.log(liter); // 12,345 liters

const followers = new Intl.NumberFormat("en-US", {
  notation: "compact",
}).format(number);
console.log(followers); // 12K
```

**[⬆ Back to the top](#javascript-tips)**

## **Object Literals**

**Bad:**

```javascript
const dayOfTheWeek = 1;

switch (dayOfTheWeek) {
  case 1:
    selectedDay = "Monday";
    break;
  case 2:
    selectedDay = "Tuesday";
    break;
  case 3:
    selectedDay = "Wednesday";
    break;
  case 4:
    selectedDay = "Thursday";
    break;
  case 5:
    selectedDay = "Friday";
    break;
  case 6:
    selectedDay = "Saturday";
    break;
  default:
    selectedDay = "Sunday";
}

console.log(selectedDay); //Monday
```

**Good:**

```javascript
const dayOfTheWeek = 2;

const daysOfTheWeek = {
  0: "Sunday",
  1: "Monday",
  2: "Tuesday",
  3: "Wednesday",
  4: "Thursday",
  5: "Friday",
  6: "Saturday",
};

const selectedDay = daysOfTheWeek[dayOfTheWeek];

console.log(selectedDay); // Tuesday
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

## **Promise**

**Bad:**

```javascript
const users = await getUser();
const products = await getProducts();
```

**Good:**

```javascript
const [users, products] = await Promise.all([getUsers(), getProducts()]);
```

**[⬆ Back to the top](#javascript-tips)**

## **Spread**

How to Copy an Array

```javascript
let arr = ["a", "b", "c"];
```

**Bad:**

```javascript
let arr2 = arr;
arr2.push("d");
console.log(arr); // ['a', 'b', 'c', 'd']
console.log(arr2); // ['a', 'b', 'c', 'd']
```

**Good:**

```javascript
let arr2 = [...arr];
arr2.push("d");
console.log(arr); // ['a', 'b', 'c']
console.log(arr2); // ['a', 'b', 'c', 'd']
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

## **Using URL Instead of String**

URL is specifically made to deal with URLs. No need to manually parse strings to extract or even change parts of it. A URL makes it easy to access specific parts of a URL, and to modify those parts.

**Bad:**

```javascript
const url = "https://mysite.com/path/to/resource?query=param";
// How to access URL parts?
```

**Good:**

```javascript
const url = new URL("https://mysite.com/path/to/resource?query=param");

url.host; // mysite.com
url.pathname; // /path/to/resource
url.searchParams.get("query"); // param

// You can even modify the url
url.pathname = "other/path/to/resource";

// And changes are immediately reflected
url; // https://mysite.com/other/path/to/resource?query=param
```

**[⬆ Back to the top](#javascript-tips)**

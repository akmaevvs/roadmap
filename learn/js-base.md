# JS — Base

[[_TOC_]]

## Уровни навыка

### Уровень 1

- Знает основные конструкции языка.
- Может реализовать простой или средней сложности алгоритм на js.
- Понимает механизм замыканий, передачи контекста в функции.
- Понимает как работают классы под капотом.
- Знаком с API работы с объектами\массивами.

### **1️⃣ Основные конструкции языка**

Ключевые моменты, которые тебе нужно знать:  
✔️ Переменные (`var`, `let`, `const`)  
✔️ Типы данных (`string`, `number`, `boolean`, `null`, `undefined`, `object`, `symbol`, `bigint`)  
✔️ Операторы (`==`, `===`, `!=`, `!==`, `&&`, `||`, `!`, `??`, `?:`)  
✔️ Условные конструкции (`if`, `switch`)  
✔️ Циклы (`for`, `while`, `do while`, `forEach`, `map`, `reduce`)  
✔️ Функции (обычные, стрелочные, `function declaration` vs `function expression`)

➡ **Практика:** Напиши функцию, которая принимает массив чисел и возвращает сумму всех положительных элементов.

---

### **2️⃣ Реализация алгоритмов (простые и средние)**

Тебе нужно уметь писать алгоритмы, связанные с:  
✔️ **Работой с числами** (поиск максимума, факториал, число Фибоначчи)  
✔️ **Работой со строками** (разворот строки, проверка палиндрома)  
✔️ **Работой с массивами** (фильтрация, сортировка, объединение данных)

➡ **Практика:** Реализуй функцию, которая принимает строку и проверяет, является ли она анаграммой другой строки.

---

### **3️⃣ Механизм замыканий и передача контекста**

🔹 **Замыкание** – это когда функция "запоминает" окружение, в котором она была создана.  
Пример:

```js
function counter() {
  let count = 0;
  return function () {
    return ++count;
  };
}
const increment = counter();
console.log(increment()); // 1
console.log(increment()); // 2
```

🔹 **Контекст (`this`)**  
Зависит от способа вызова функции. Например:

```js
const obj = {
  name: "Alice",
  greet() {
    console.log(`Hello, ${this.name}`);
  },
};
obj.greet(); // "Hello, Alice"

const greetFunc = obj.greet;
greetFunc(); // this === undefined (или window в браузере)
```

Чтобы сохранить `this`, используют: `.bind()`, `.call()`, `.apply()`.

➡ **Практика:** Напиши функцию, которая принимает имя и возвращает другую функцию, которая приветствует это имя.

---

### **4️⃣ Как работают классы под капотом**

JS-классы – это синтаксический сахар над прототипами.  
Под капотом класс:

1. Создаёт функцию-конструктор
2. Привязывает методы к `prototype`
3. Наследование реализуется через `Object.create()`

Пример класса и его аналог через прототипы:

```js
class Person {
  constructor(name) {
    this.name = name;
  }
  greet() {
    console.log(`Hi, I'm ${this.name}`);
  }
}

// То же самое через прототипы:
function Person(name) {
  this.name = name;
}
Person.prototype.greet = function () {
  console.log(`Hi, I'm ${this.name}`);
};
```

➡ **Практика:** Реализуй класс `Animal` с методом `speak()`, а затем унаследуй от него класс `Dog` с методом `bark()`.

---

### **5️⃣ API работы с объектами и массивами**

🔹 **Работа с объектами**

- `Object.keys(obj)`, `Object.values(obj)`, `Object.entries(obj)`
- `Object.assign(target, source)`
- `Object.freeze(obj)`, `Object.seal(obj)`

🔹 **Работа с массивами**

- `map()`, `filter()`, `reduce()`, `find()`, `some()`, `every()`
- `sort()` (и его проблемы со строками)
- `includes()`, `indexOf()`, `splice()`, `slice()`

➡ **Практика:** Напиши функцию, которая принимает массив объектов (пользователей) и возвращает массив имён пользователей старше 18 лет.

---

### 🚀 **Как тренироваться?**

✅ **LeetCode, CodeWars** – решай задачи уровня **Easy/Medium**  
✅ **Пиши код руками** – без копипаста, только так закрепишь материал  
✅ **Придумывай маленькие проекты** – например, калькулятор, список задач, простую игру

Отличный вопрос! В последние версии JavaScript добавили несколько полезных методов для работы с массивами и объектами. Давай разберём их.

---

## **🔹 Новые методы для массивов**

### **1️⃣ `at(index)`**

Альтернатива `arr[index]`, но поддерживает отрицательные индексы.

```js
const arr = [10, 20, 30, 40];
console.log(arr.at(-1)); // 40 (последний элемент)
```

### **2️⃣ `findLast()` и `findLastIndex()`**

Как `find()`, но начинает поиск с конца массива.

```js
const numbers = [5, 12, 8, 130, 44];
console.log(numbers.findLast((n) => n > 10)); // 44
console.log(numbers.findLastIndex((n) => n > 10)); // 4
```

### **3️⃣ `toSorted()`, `toReversed()`, `toSpliced()`**

Работают как `sort()`, `reverse()`, `splice()`, но не изменяют оригинальный массив (создают копию).

```js
const nums = [3, 1, 4, 1, 5, 9];
console.log(nums.toSorted()); // [1, 1, 3, 4, 5, 9]
console.log(nums.toReversed()); // [9, 5, 1, 4, 1, 3]
console.log(nums.toSpliced(2, 2, 99)); // [3, 1, 99, 5, 9]
console.log(nums); // Оригинальный массив не изменился
```

### **4️⃣ `group()` и `groupToMap()`**

Группировка элементов массива по ключу.

```js
const users = [
  { name: "Alice", age: 25 },
  { name: "Bob", age: 30 },
  { name: "Charlie", age: 25 },
];

const grouped = Object.groupBy(users, (user) => user.age);
console.log(grouped);
/*
{
  25: [{ name: "Alice", age: 25 }, { name: "Charlie", age: 25 }],
  30: [{ name: "Bob", age: 30 }]
}
*/
```

⚠ `group()` работает с обычными объектами, а `groupToMap()` создаёт `Map`.

---

## **🔹 Новые методы для объектов**

### **1️⃣ `Object.hasOwn(obj, key)`**

Аналог `obj.hasOwnProperty(key)`, но безопаснее (не зависит от прототипа).

```js
const person = { name: "Alice" };
console.log(Object.hasOwn(person, "name")); // true
console.log(Object.hasOwn(person, "age")); // false
```

### **2️⃣ `Object.fromEntries()` + `Object.entries()`**

Превращает массив пар `[ключ, значение]` обратно в объект.

```js
const entries = [
  ["name", "Alice"],
  ["age", 25],
];
const obj = Object.fromEntries(entries);
console.log(obj); // { name: "Alice", age: 25 }
```

### **3️⃣ `structuredClone()`**

Делает глубокое (deep) копирование объектов, включая вложенные структуры.

```js
const obj = { name: "Alice", details: { age: 25 } };
const clone = structuredClone(obj);
clone.details.age = 30;

console.log(obj.details.age); // 25 (оригинал не изменился)
```

⚠ Ранее использовали `JSON.parse(JSON.stringify(obj)`, но он не работает с `Map`, `Set`, `Date`.

---

### 🚀 **Практика**

Попробуй написать функцию, которая группирует пользователей по возрасту и возвращает объект, где ключи — возраст, а значения — массивы имён.

```js
const users = [
  { name: "Alice", age: 25 },
  { name: "Bob", age: 30 },
  { name: "Charlie", age: 25 },
];

function groupUsers(users) {
  return Object.groupBy(users, (user) => user.age);
}

console.log(groupUsers(users));
```

### Уровень 2

- Следит за развитием языка (поддерживает актуальность своих знаний), понимает как устроен TC39 process.
- Знает историю языка, не применяет устаревшие подходы к написанию кода на js.

Например:

- правильно использует фичи с ранних стадий спецификации
- не использует устаревшие конструкции языка, если есть новый, широко принятый подход.

---

## **1️⃣ Как следить за развитием языка? (TC39 Process) 🚀**  

**TC39** — комитет, который разрабатывает спецификацию ECMAScript (основа JavaScript).  
Новые фичи проходят **5 стадий** перед добавлением в язык:  

🔹 **Stage 0 ("Strawman")** – идея, обсуждаемая внутри комитета.  
🔹 **Stage 1 ("Proposal")** – есть черновой дизайн, но может измениться.  
🔹 **Stage 2 ("Draft")** – чёткое описание, можно пробовать в Babel/Polyfills.  
🔹 **Stage 3 ("Candidate")** – фича готова, ждёт финального утверждения.  
🔹 **Stage 4 ("Finished")** – официально включена в стандарт.  

👉 **Где следить за нововведениями?**  
- [🔗 TC39 proposals](https://github.com/tc39/proposals) — список всех фич и их статусы  
- [🔗 ECMAScript Latest Features](https://tc39.es/) — официальная спецификация  
- [🔗 Kangax Compatibility Table](https://kangax.github.io/compat-table/es2016plus/) — поддержка в браузерах  
- [🔗 @DailyJS](https://twitter.com/dailyjs) и [🔗 @TC39](https://twitter.com/TC39) — Twitter-аккаунты  

**Пример:** Если фича на **Stage 3**, её уже можно тестировать в коде (с Babel или V8 флагами).  

---

## **2️⃣ История JavaScript и устаревшие подходы**  

Знание истории языка помогает понимать, **почему** появились те или иные конструкции.  

### 🔥 **Чего не стоит использовать в современном JS?**  

### ❌ **1. `var` вместо `let/const`**  
Раньше `var` использовался повсеместно, но он имеет проблемы с **hoisting** и **областью видимости**.  

**❌ Плохая практика:**  
```js
function example() {
  if (true) {
    var x = 10;
  }
  console.log(x); // 10 (хотя объявили в блоке!)
}
```
**✅ Современный подход:**  
```js
function example() {
  if (true) {
    let x = 10;
  }
  console.log(x); // ReferenceError
}
```

---

### ❌ **2. `arguments` вместо rest-параметров**  
Раньше использовали `arguments`, но у него нет методов массива.  

**❌ Плохая практика:**  
```js
function sum() {
  return Array.prototype.reduce.call(arguments, (a, b) => a + b);
}
```
**✅ Современный подход (`...rest`)**  
```js
function sum(...nums) {
  return nums.reduce((a, b) => a + b);
}
```

---

### ❌ **3. `for...in` для массивов**  
Использование `for...in` для массивов может привести к багам, так как он проходит по **всем** свойствам объекта, включая прототипные.  

**❌ Плохая практика:**  
```js
Array.prototype.customMethod = () => {};
const arr = [1, 2, 3];
for (let i in arr) {
  console.log(arr[i]); // Выведет 1, 2, 3 и customMethod!
}
```
**✅ Современный подход:**  
```js
const arr = [1, 2, 3];
for (let num of arr) {
  console.log(num); // Чистый перебор без проблем
}
```

---

### ❌ **4. `new Object()`, `new Array()` вместо `{}` и `[]`**  
Создание объектов через `new Object()` — устаревший стиль.  

**❌ Плохая практика:**  
```js
const obj = new Object();
const arr = new Array();
```
**✅ Современный подход:**  
```js
const obj = {};  
const arr = [];
```

---

### ❌ **5. `function` вместо стрелочных функций, если контекст не нужен**  
Обычные `function` имеют свой `this`, что может привести к неожиданным ошибкам.  

**❌ Плохая практика:**  
```js
const obj = {
  value: 42,
  getValue: function () {
    setTimeout(function () {
      console.log(this.value); // undefined
    }, 1000);
  }
};
```
**✅ Современный подход:**  
```js
const obj = {
  value: 42,
  getValue() {
    setTimeout(() => {
      console.log(this.value); // 42
    }, 1000);
  }
};
```

---

### ❌ **6. `==` вместо `===`**  
Оператор `==` может приводить к неочевидным ошибкам.  

**❌ Плохая практика:**  
```js
console.log(0 == false); // true (WTF?)
console.log("" == false); // true
```
**✅ Современный подход:**  
```js
console.log(0 === false); // false
console.log("" === false); // false
```

---

## **3️⃣ Как правильно использовать новые фичи?**  

Чтобы код оставался актуальным:  
✅ Используй **новые API**, если они поддерживаются  
✅ Избегай **устаревших конструкций**, даже если браузеры их поддерживают  
✅ Экспериментируй с **Stage 3+ фичами**, если работаешь с Babel  

### **Примеры новых возможностей:**  

🔹 **Optional Chaining (`?.`)** – безопасный доступ к вложенным свойствам  
```js
const user = { profile: { name: "Alice" } };
console.log(user.profile?.name); // Alice
console.log(user.address?.city); // undefined (не ошибка)
```

🔹 **Nullish Coalescing (`??`)** – правильная проверка `null/undefined`  
```js
const value = 0 ?? 42;
console.log(value); // 0 (а не 42!)
```

🔹 **Top-level `await`** – теперь можно использовать `await` в корне модуля  
```js
const data = await fetch("https://jsonplaceholder.typicode.com/posts/1").then(res => res.json());
console.log(data);
```

🔹 **Records & Tuples (Stage 2)** – неизменяемые структуры данных  
```js
const person = #{
  name: "Alice",
  age: 25
};
console.log(person.name); // "Alice"
```
*(Пока только экспериментально в V8 и Babel.)*

---

## **Вывод**  
🎯 Если ты хочешь писать актуальный и чистый JS-код:  
✅ **Следи за TC39** и новыми фичами  
✅ **Избегай устаревших практик**  
✅ **Используй современные API** и `ES6+`  
✅ **Экспериментируй** с `Stage 3+` через Babel  

### Уровень 3

- Практически идеально знает спецификацию языка, знает тонкие моменты (прокси, проперти дескрипторы, Typed Arrays и т.д.).

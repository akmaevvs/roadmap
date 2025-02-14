# JS — Base

## Оглавление

- [Уровень 1](#уровень-1)
  - [1️⃣ Основные конструкции языка](#1️⃣-основные-конструкции-языка)
  - [2️⃣ Реализация алгоритмов (простые и средние)](#2️⃣-реализация-алгоритмов-простые-и-средние)
  - [3️⃣ Механизм замыканий и передача контекста](#3️⃣-механизм-замыканий-и-передача-контекста)
  - [4️⃣ Как работают классы под капотом](#4️⃣-как-работают-классы-под-капотом)
  - [5️⃣ API работы с объектами и массивами](#5️⃣-api-работы-с-объектами-и-массивами)
- [Уровень 2](#уровень-2)
  - [1️⃣ Глубокое понимание JS-спецификации (ECMA-262)](#1️⃣-глубокое-понимание-js-спецификации-ECMA-262)
  - [2️⃣ История JavaScript и устаревшие подходы](#2️⃣-история-javascript-и-устаревшие-подходы)
  - [3️⃣ Как правильно использовать новые фичи?](#3️⃣-как-правильно-использовать-новые-фичи)
- [Уровень 3](#уровень-3)
  - 1️⃣ Глубокое понимание JS-спецификации (ECMA-262)
  - 2️⃣ Proxy и Reflect API
  - 3️⃣ Property Descriptors & Object.defineProperty()
  - 4️⃣ Typed Arrays и ArrayBuffer
  - 5️⃣ Symbols и скрытые свойства
  - 6️⃣ WeakMap и WeakSet (Сборка мусора и память)
  - 7️⃣ Event Loop & Microtasks
  - 8️⃣ Generator Functions & Async Iterators

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

---

# **1️⃣ Глубокое понимание JS-спецификации (ECMA-262)**  
Спецификация **ECMAScript** определяет поведение языка. Если хочешь знать **"как это работает под капотом"**, изучай [🔗 спецификацию](https://tc39.es/ecma262/).  

✅ **Что важно знать?**  
- **Как работает Event Loop** (и разница между `microtask` и `macrotask`)  
- **Execution Context и Call Stack**  
- **Memory Management (GC, WeakRef, FinalizationRegistry)**  
- **Object Internal Slots (`[[Prototype]]`, `[[DefineOwnProperty]]`)**  
- **Как движки (V8, SpiderMonkey) оптимизируют код**  

🔥 **Глубокое понимание JavaScript: Разбираем спецификацию (ECMA-262) детально**  

Чтобы разбираться в JavaScript на **экспертном уровне**, важно понимать, **как язык работает под капотом**. Это требует изучения **ECMAScript Specification (ECMA-262)**, где описаны все внутренние механизмы JS.  

Разберём **каждый из ключевых пунктов** более детально:  

---

## **1️⃣ Event Loop: Как работает асинхронность в JS**  
**Event Loop** – это механизм, который позволяет JavaScript **быть асинхронным** и управлять выполнением кода.  

### 🔹 Как работает Event Loop?  
1. **Call Stack (Стек вызовов)**  
   - Выполняет синхронный код  
   - Работает по принципу **LIFO** (Last In, First Out)  

2. **Web APIs** (например, `setTimeout`, `fetch`)  
   - Обрабатывают асинхронные задачи (таймеры, HTTP-запросы)  

3. **Callback Queue (Очередь макрозадач)**  
   - Выполняет `setTimeout`, `setInterval`, события DOM  

4. **Microtask Queue (Очередь микрозадач)**  
   - Включает **Promise callbacks, MutationObserver, queueMicrotask**  
   - **Приоритет выше**, чем у макрозадач  

---

### 🔹 Пример работы Event Loop  
```js
console.log("Start");

setTimeout(() => console.log("setTimeout"), 0);
Promise.resolve().then(() => console.log("Promise"));

console.log("End");

// Вывод:
// Start
// End
// Promise
// setTimeout
```
**Почему `Promise` выполняется раньше, чем `setTimeout`?**  
🔹 **Promise попадает в microtask queue** (выполняется сразу после стека вызовов)  
🔹 **setTimeout** – это макрозадача, которая выполняется **после** всех микрозадач  

➡ **Практика:** Напиши код с `setImmediate`, `requestAnimationFrame` и `queueMicrotask`, чтобы увидеть разницу в порядке выполнения.

---

## **2️⃣ Execution Context и Call Stack**  
### 🔹 Что такое Execution Context?  
**Execution Context (Контекст выполнения)** – это среда, в которой выполняется код.  

🔹 **Глобальный контекст (Global Execution Context)**  
🔹 **Контекст функций (Function Execution Context)**  
🔹 **Контекст модуля (Module Execution Context, ES6)**  

### 🔹 Как работает Call Stack?  
Каждый вызов функции создаёт **новый Execution Context** и помещается в стек вызовов (Call Stack).  

```js
function a() {
  console.log("A");
  b();
}

function b() {
  console.log("B");
}

a();
```
**Как Call Stack обрабатывает код:**  
1️⃣ Входит `a()` → создаётся `Execution Context`  
2️⃣ Входит `b()` → создаётся `Execution Context`  
3️⃣ Выводится `"B"`, затем `b()` удаляется из стека  
4️⃣ Выводится `"A"`, затем `a()` удаляется из стека  

---

## **3️⃣ Memory Management (GC, WeakRef, FinalizationRegistry)**  
JavaScript **автоматически управляет памятью**, но важно понимать, как это работает.  

### 🔹 Как работает Garbage Collection (GC)?  
GC использует **алгоритм "Mark-and-Sweep"**:  
1. Помечает **доступные** объекты  
2. Удаляет **недоступные** объекты  

```js
let obj = { name: "Alice" };
obj = null; // Объект теперь "недоступен" → GC его удалит
```

### 🔹 WeakRef и FinalizationRegistry  
🔹 **WeakRef** – позволяет создавать слабые ссылки (объект может быть удалён GC)  
🔹 **FinalizationRegistry** – выполняет код, когда объект удаляется  

```js
let obj = { name: "Alice" };
const registry = new FinalizationRegistry(() => console.log("Object deleted"));

let weakRef = new WeakRef(obj);
registry.register(obj, "Cleanup");

obj = null; // GC удалит объект
```
➡ **Практика:** Напиши кеш данных с `WeakMap`, который автоматически очищается при удалении объектов.

---

## **4️⃣ Object Internal Slots (`[[Prototype]]`, `[[DefineOwnProperty]]`)**  
Каждый объект в JS имеет **внутренние слоты**, которые определяют его поведение.  

🔹 `[[Prototype]]` – ссылка на прототип объекта  
🔹 `[[DefineOwnProperty]]` – механизм создания/изменения свойств  

### **Как работает `[[Prototype]]`?**
```js
const parent = { greet() { console.log("Hello!"); } };
const child = Object.create(parent);

child.greet(); // "Hello!" (ищет в прототипе)
```
**Как движок ищет свойство?**  
1️⃣ Ищет свойство в `child`  
2️⃣ Если нет – идёт в `[[Prototype]]`  
3️⃣ Если не найдено – идёт выше по цепочке  

➡ **Практика:** Реализуй `Object.create()` вручную.

---

## **5️⃣ Как движки JS (V8, SpiderMonkey) оптимизируют код?**  
### 🔹 Just-In-Time (JIT) Compilation  
JS **интерпретируемый**, но современные движки используют **JIT-компиляцию**:  
1. **Parser** – разбирает код в AST (Abstract Syntax Tree)  
2. **Interpreter** – выполняет байткод (Baseline Compiler)  
3. **Optimizing Compiler (TurboFan)** – ускоряет код во время работы  

### 🔹 Inline Caching  
Если функция вызывается **с одинаковыми типами данных**, движок её **оптимизирует**.  

```js
function add(x, y) {
  return x + y;
}

add(10, 20); // Быстро
add("Hello", "World"); // Замедление (разные типы)
```
➡ **Практика:** Напиши код, который форсирует деоптимизацию (например, меняя типы аргументов в цикле).

---

## **Вывод**  
🎯 Если ты хочешь **разбираться в JS на экспертном уровне**, тебе нужно:  
✅ Изучать **Event Loop, Call Stack, Execution Context**  
✅ Понимать **Garbage Collection, WeakRef, Memory Management**  
✅ Разбираться в **Prototype Chain, Internal Slots**  
✅ Понимать **как движки JS (V8) оптимизируют код**  

📌 **Практическое задание:**  
🔹 Реализуй **свой Event Loop** (минимальную версию)  
🔹 Напиши **WeakMap-кеш**, который автоматически очищается  
🔹 Создай **Proxy-объект**, который логирует доступ к свойствам  

---

# **2️⃣ Proxy и Reflect API**  
🔹 **Proxy** – позволяет перехватывать операции над объектами (`get`, `set`, `has`, `deleteProperty`, `apply`, `construct`).  
🔹 **Reflect API** – служит для работы с объектами без прямого вмешательства в их прототипы.  

### **Пример: Защита объекта от изменения**  
```js
const user = { name: "Alice", age: 30 };

const protectedUser = new Proxy(user, {
  set(target, prop, value) {
    if (prop === "age" && value < 18) {
      throw new Error("Age must be 18+");
    }
    target[prop] = value;
    return true;
  }
});

protectedUser.age = 25;  // ✅ Работает
protectedUser.age = 15;  // ❌ Ошибка
```

### **Пример: Автологирование доступа к объекту**  
```js
const logger = new Proxy(user, {
  get(target, prop) {
    console.log(`Reading property "${prop}"`);
    return target[prop];
  }
});

console.log(logger.name); // Reading property "name" → Alice
```

➡ **Практика:** Напиши прокси, который запрещает удаление свойств объекта.

---

# **3️⃣ Property Descriptors & Object.defineProperty()**  
Каждое свойство объекта содержит скрытые атрибуты:  
- `writable` (можно ли изменять)  
- `enumerable` (участвует ли в `for...in`)  
- `configurable` (можно ли удалять/изменять)  

### **Пример: создание неизменяемого свойства**  
```js
const obj = {};
Object.defineProperty(obj, "constant", {
  value: 42,
  writable: false,
  enumerable: false,
  configurable: false
});

obj.constant = 100; // ❌ Ошибка в strict mode
console.log(obj.constant); // 42
```

➡ **Практика:** Создай объект, в котором свойства нельзя удалять (`configurable: false`), но можно изменять (`writable: true`).

---

# **4️⃣ Typed Arrays и ArrayBuffer**  
🔹 **Typed Arrays** позволяют работать с бинарными данными (`Int8Array`, `Float32Array`).  
🔹 **ArrayBuffer** – низкоуровневое представление памяти.  
🔹 **DataView** – даёт контроль над байтами.  

### **Пример: Создание `Uint8Array`**  
```js
const buffer = new ArrayBuffer(4);  // 4 байта памяти
const view = new Uint8Array(buffer);

view[0] = 255;  // 0b11111111 (максимальное значение)
view[1] = 128;  // 0b10000000
console.log(view); // Uint8Array(4) [ 255, 128, 0, 0 ]
```

➡ **Практика:** Напиши функцию, которая конвертирует строку в `Uint8Array` и обратно.

---

# **5️⃣ Symbols и скрытые свойства**  
🔹 **Symbols** – уникальные ключи, которые не конфликтуют с обычными строковыми свойствами.  
🔹 Можно использовать для **скрытых полей** объектов.  

### **Пример: скрытое свойство в объекте**  
```js
const ID = Symbol("id");

const user = {
  name: "Bob",
  [ID]: 12345
};

console.log(user[ID]); // 12345
console.log(Object.keys(user)); // ["name"]
console.log(Object.getOwnPropertySymbols(user)); // [Symbol(id)]
```

➡ **Практика:** Используй `Symbol` для создания приватных методов в объекте.

---

# **6️⃣ WeakMap и WeakSet (Сборка мусора и память)**  
🔹 **WeakMap** хранит ссылки на объекты **с возможностью их удаления сборщиком мусора**.  
🔹 **WeakSet** аналогично, но для значений.  

### **Пример: кеширование объектов (автоматическое удаление)**  
```js
const cache = new WeakMap();

function processUser(user) {
  if (!cache.has(user)) {
    cache.set(user, Date.now());  // Записываем дату обработки
  }
  return cache.get(user);
}

let user = { name: "Alice" };
processUser(user);
console.log(cache.get(user)); // Дата

user = null;  // Объект удалится из WeakMap автоматически!
```

➡ **Практика:** Напиши `WeakSet`, который отслеживает объекты, но позволяет сборщику мусора удалять их.

---

# **7️⃣ Event Loop & Microtasks**  
🔹 **Microtasks** (Promise, MutationObserver, `queueMicrotask`) выполняются **до** macrotasks (setTimeout, setImmediate).  
🔹 **Call Stack → Microtask Queue → Macrotask Queue**  

### **Пример: порядок выполнения кода**  
```js
console.log("Start");

setTimeout(() => console.log("setTimeout"), 0);
Promise.resolve().then(() => console.log("Promise"));

console.log("End");

// Вывод:
// Start
// End
// Promise
// setTimeout
```

➡ **Практика:** Объясни, почему `Promise` выполняется раньше, чем `setTimeout`.

---

# **8️⃣ Generator Functions & Async Iterators**  
🔹 **Generators (`function*`)** позволяют **приостанавливать** выполнение функции (`yield`).  
🔹 **Async Generators (`async function*`)** работают с `await`.  

### **Пример: генератор чисел**  
```js
function* numbers() {
  yield 1;
  yield 2;
  yield 3;
}

const gen = numbers();
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
console.log(gen.next().value); // 3
```

### **Пример: асинхронный генератор API данных**  
```js
async function* fetchPosts() {
  const res = await fetch("https://jsonplaceholder.typicode.com/posts");
  const posts = await res.json();
  
  for (let post of posts) {
    yield post;
  }
}

(async () => {
  for await (let post of fetchPosts()) {
    console.log(post.title);
  }
})();
```

➡ **Практика:** Напиши `async generator`, который загружает данные постранично.

---

# **Вывод**  
🎯 Если ты хочешь **глубоко понимать JavaScript**, тебе нужно:  
✅ Читать **ECMA-262** (разделы по **Execution Context, Memory, Event Loop**)  
✅ Разбираться в **Proxy, Reflect, Property Descriptors**  
✅ Понимать **Typed Arrays, WeakMap/WeakSet, Garbage Collection**  
✅ Знать тонкости **Symbols, Generators, Async Iterators**  


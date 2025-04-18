# Typescript 

## Оглавление

### Уровень 1
*Знание:*

- [Уровень 1](#уровень-1)
  - [1️⃣ Виды типизации и их отличия](#1️⃣-виды-типизации-и-их-отличия)
  - [2️⃣ Какая типизация используется в JS и TS](#2️⃣-какая-типизация-используется-в-js-и-ts)
  - [3️⃣ Что такое интерфейсы и type-алиасы](#3️⃣-интерфейсы-и-type-алиасы)
  - [4️⃣ Основные функции TS и ключевые слова](#4️⃣-основные-функции-ts)
- [Уровень 2](#уровень-2)
  - [1️⃣ Прочие основные функции TS](#1️⃣-Прочие основные функции TS)
  - [2️⃣ Встроенные утилитарные типы TS](#2️⃣-Встроенные утилитарные типы TS)
- [Уровень 3](#уровень-3)
  - [1️⃣ Strict-mode](#1️⃣-Strict-mode)
  - [2️⃣ Перегрузка функций](#2️⃣-Перегрузка функций)
  - [3️⃣ Рекурсивные типы](#3️⃣-Рекурсивные-типы)
  - [3️⃣ Conditional types](#3️⃣-Conditional-types)
  - [3️⃣ Выводимость типов](#3️⃣-Выводимость-типов)
  - [3️⃣ Mapped types](#3️⃣-Mapped-types)
- [Уровень 4](#уровень-4)
  - [1️⃣ Type soundness и Type safety](#1️⃣-Type-soundness-и-Type-safety)
  - [1️⃣ Инвариантность, ковариантность, контравариантность и бивариантность](#1️⃣-Инвариантность-ковариантность-контравариантность-и-бивариантность)
  - [1️⃣ Полиморфизм в TS](#1️⃣-Полиморфизм-в-ts)



### Уровень 1
### 1️⃣ Виды типизации и их отличия

#### 1. Статическая и динамическая типизация

| Типизация       | Описание                                                                 | Примеры языков       |
|------------------|--------------------------------------------------------------------------|----------------------|
| **Статическая**   | Типы переменных определяются **во время компиляции**.                   | TypeScript, Java     |
| **Динамическая**  | Типы переменных определяются **во время выполнения (runtime)**.         | JavaScript, Python   |


#### Явная и неявная типизация

`Явная`	Тип переменной указывается явно разработчиком.	
```ts
let count: number = 10;
```

`Неявная`	Тип выводится автоматически из присвоенного значения.	
```ts
let message = "Hello"; // string
```
### 2️⃣ Какая типизация используется в JS и TS
#### Статическая типизация (TypeScript):
```ts
let name: string = "Alice"; // ошибка, если позже присвоить число
name = 42; // ❌ ошибка: number не совместим с string
```
### Динамическая типизация (JavaScript):
```ts
let name = "Alice";
name = 42; // ✅ допустимо, тип может меняться
```

### 3️⃣ Интерфейсы и type-алиасы

Что такое интерфейсы

Интерфейс (`interface`) описывает форму объекта: какие свойства и методы он должен иметь.
Применяется в основном для описания структуры объектов и классов.
```ts
interface User {
id: number;
name: string;
isAdmin?: boolean; // необязательное свойство
}

const user: User = {
id: 1,
name: "Alice",
};
```

Type-алиас (`type`) позволяет задать имя для любого типа: примитивов, объединений, пересечений, объектов и т.д.
```ts
type ID = number;

type User = {
  id: ID;
  name: string;
  isAdmin?: boolean;
};
```
#### Отличия между interface и type

| Характеристика      | interface                                                                 | type                                                                 |
|---------------------|---------------------------------------------------------------------------|----------------------------------------------------------------------|
| **Расширение**      | `extends` и повторное объявление                                          | `&` (пересечения), нельзя повторно объявлять                         |
| **Композиция**      | Через `extends`                                                           | Через `&` (пересечения) и `\|` (объединения)                         |
| **Использование**   | Объекты, классы                                                           | Любые типы: объекты, примитивы, объединения, кортежи                  |
| **Объединение**     | Нет (только слияние деклараций)                                           | Да (`\|`)                                                            |
| **Примитивы**       | Нет                                                                       | Да                                                                   |
| **Слияние**         | Автоматическое при повторном объявлении                                   | Не поддерживается                                                   |
| **Реализация**      | `implements` для классов                                                  | Только для простых типов (не объединений)                            |
| **Сложные типы**    | Ограничены объектами и классами                                           | Поддерживают условные типы, маппинг                                  |


Рекомендации по использованию

Используй `interface`, когда описываешь структуру объекта или класса.

Используй `type`, когда нужно описать сложный тип, объединения (|), пересечения (&) или любые типы, кроме объектов.
```ts
// объединение через type
type Status = "loading" | "success" | "error";

// пересечение типов
type Admin = User & { role: string };
```

### 4️⃣ Основные функции TypeScript

Ключевые слова

| Ключевое слово | Назначение | Пример |
|----------------|------------|--------|
| **type** | Создание пользовательских типов (включая примитивы, объединения, кортежи) | `type Id = string \| number;` |
| **interface** | Описание структуры объектов/классов с возможностью слияния | `interface User { name: string; age: number; }` |
| **extends** | Наследование классов/интерфейсов | `interface Admin extends User { role: string; }` |
| **implements** | Реализация интерфейса классом | `class Member implements User { name: string; age: number; }` |
| **enum** | Создание перечислений | `enum Drink { Beer = 'beer', Water = 'water' }` |
| **keyof** | Получение union-типа ключей объекта | `type UserKeys = keyof User; // "name" \| "age"` |
| **typeof** | Получение типа переменной | `const sizes = { small: '470px' }; type Sizes = typeof sizes;` |
| **infer** | Извлечение типа в условных типах | `type ArrayType<T> = T extends (infer U)[] ? U : never;` |
| **as** | Приведение типов | `const element = document.getElementById('root') as HTMLElement;` |
| **is** | Тип-гард (type predicate) | `function isNumber(x: any): x is number { return typeof x === 'number'; }` |
| **never** | Тип для недостижимых значений | `function error(message: string): never { throw new Error(message); }` |
| **Record** | Создание типа-словаря | `const prices: Record<Drink, number> = { beer: 100, water: 20 };` |
| **Partial** | Делает все свойства необязательными | `type OptionalUser = Partial<User>;` |
| **Readonly** | Запрещает модификацию свойств | `type ImmutableUser = Readonly<User>;` |
| **Generics** | Универсальные типы (T, K, V) | `function identity<T>(arg: T): T { return arg; }` |

Примеры использования в коде (дополнительно):

```ts
// Условные типы с infer
type UnpackArray<T> = T extends (infer U)[] ? U : T;
type NumArray = number[];
type Num = UnpackArray<NumArray>; // number

// Тип-гард с is
function isAdmin(user: User | Admin): user is Admin {
return 'role' in user;
}

// Дженерик с несколькими параметрами
type Pair<T, U> = { first: T; second: U };
const pair: Pair<string, number> = { first: 'Age', second: 30 };
```

#### Специфичный синтаксис

`?. — Optional Chaining`

Проверка существования свойства/метода перед доступом к нему.


```ts
const user = {
    profile: {
    name: "Alice",
 },
};

console.log(user.profile?.name); // "Alice"
console.log(user.settings?.theme); // undefined, без ошибки
```
`! — Non-null Assertion`

Говорим TypeScript, что значение точно не null или undefined.
```ts
function process(name?: string) {
  const length = name!.length;
  console.log(length);
}
```
⚠️ Используй `! `только если уверен, что значение не `null/undefined`

### Уровень 2

### 1️⃣ Прочие основные функции TS

#### Интерфейсы
Интерфейсы могут наследоваться друг от друга и объединяться:

```ts
interface A {
  a: string;
}

interface B {
  b: number;
}

interface C extends A, B {
  c: boolean;
}

const example: C = {
  a: 'hello',
  b: 42,
  c: true
};
```

#### Классы
Классы могут наследоваться от других классов:

```ts
class Animal {
  move() {
    console.log('Moving...');
  }
}

class Dog extends Animal {
  bark() {
    console.log('Woof!');
  }
}
```

#### Имплементация интерфейсов
Класс может реализовывать несколько интерфейсов:
```ts
interface Flyable {
  fly(): void;
}

interface Swimmable {
  swim(): void;
}

class Duck implements Flyable, Swimmable {
  fly() {
    console.log('Flying');
  }
  swim() {
    console.log('Swimming');
  }
}
```

#### Абстрактные классы
Абстрактные классы задают общую структуру, но не реализуют всё поведение. 
Они не могут быть инстанцированы напрямую.

```ts
abstract class Shape {
  abstract area(): number;

  printArea() {
    console.log('Area:', this.area());
  }
}

class Circle extends Shape {
  constructor(private radius: number) {
    super();
  }

  area(): number {
    return Math.PI * this.radius ** 2;
  }
}
```
Абстрактные методы обязаны быть реализованы в наследниках.

#### Type Guards
Тайпгард — это способ уточнить тип внутри условия. Это важно, когда переменная может быть нескольких типов.

`typeof` — для примитивов

```ts
function printValue(val: string | number) {
    if (typeof val === 'string') {
    console.log(val.toUpperCase());
    } else {
    console.log(val.toFixed(2));
 }
}
```

`in` — для объектов
```ts
interface Cat {
    meow: () => void;
}

interface Dog {
    bark: () => void;
}

function makeSound(animal: Cat | Dog) {
    if ('meow' in animal) {
    animal.meow();
} else {
    animal.bark();
 }
}
```

`instanceof` — для классов
```ts
class Car {
    drive() {}
}

class Bike {
    pedal() {}
}

function useVehicle(v: Car | Bike) {
    if (v instanceof Car) {
    v.drive();
    } else {
    v.pedal();
 }
}
```

#### Union (|) и Intersection (&) типы
`Union` (объединение)
Переменная может быть одного из нескольких типов:
```ts
type A = { a: string };
type B = { b: number };

type Union = A | B;

const u: Union = { a: 'hello' }; // или { b: 42 }
```
`Intersection` (пересечение)
Переменная должна соответствовать всем типам одновременно:
```ts
type Intersection = A & B;

const i: Intersection = { a: 'hi', b: 100 };
```

#### Const assertion (as const) и Enum

`as const`
Позволяет задать литеральные типы, делая объект или массив неизменяемым:
```ts
const point = {
x: 10,
y: 20
} as const;

// point.x = 30 ❌ — ошибка, поле "x" только для чтения

function draw(p: { x: 10; y: 20 }) {}
draw(point); // ✅
```

#### Enum (перечисления)
Enum задаёт набор именованных значений:
```ts
enum Direction {
    Up,
    Down,
    Left,
    Right
}

const dir: Direction = Direction.Up;

enum Role {
  Admin = 'admin',
  User = 'user'
}
```

`const enum `— для оптимизации
При использовании const enum, значения инлайнятся на этапе компиляции:

```ts
const enum Status {
  Success = 'success',
  Fail = 'fail'
}

const s: Status = Status.Success;
```
### 2️⃣ Встроенные утилитарные типы TS

#### `Partial<T>`

**Делает все поля типа `T` необязательными**.

```ts
interface User {
  name: string;
  age: number;
}

const updateUser = (user: Partial<User>) => {
  // можно передать только часть полей
  console.log(user.name);
};
```

#### Readonly<T>
Делает все поля типа T только для чтения (immutable).
```ts
interface User {
    name: string;
    age: number;
}

const user: Readonly<User> = {
    name: 'Alice',
    age: 25
};

// user.age = 30 ❌ — нельзя изменить
```

#### Required<T>
Превращает все необязательные поля типа T в обязательные.
```ts
interface User {
  name?: string;
  age?: number;
}

const fullUser: Required<User> = {
  name: 'Bob',
  age: 30
};

```

#### Record<K, T>
Создаёт объект с ключами K и значениями типа T.
```ts
type Roles = 'admin' | 'user' | 'guest';

const permissions: Record<Roles, boolean> = {
    admin: true,
    user: true,
    guest: false
};
```

#### Pick<T, K>
Выбирает только указанные ключи K из типа T.
```ts
interface User {
    id: number;
    name: string;
    email: string;
}

type PublicUser = Pick<User, 'id' | 'name'>;

const user: PublicUser = {
    id: 1,
    name: 'Alice'
};
```

#### Omit<T, K>
Удаляет указанные ключи K из типа T (противоположность Pick).
```ts
type PrivateUser = Omit<User, 'email'>;

const user: PrivateUser = {
    id: 1,
    name: 'Bob'
};
```

#### Exclude<T, U>
Исключает из объединения T все члены, входящие в U.
```ts
type Status = 'success' | 'error' | 'loading';

type NotLoading = Exclude<Status, 'loading'>; // 'success' | 'error'
```

#### NonNullable<T>
Удаляет null и undefined из типа T.
```ts
type MaybeUser = string | null | undefined;

type SafeUser = NonNullable<MaybeUser>; // string
```

#### ReturnType<T>
Получает тип возвращаемого значения функции T.

```ts
function getUser() {
    return {
    name: 'Alice',
    age: 30
 };
}

type User = ReturnType<typeof getUser>; // { name: string; age: number }
```

#### Parameters<T>
Получает кортеж типов параметров функции T.

```ts
function greet(name: string, age: number) {}

type GreetParams = Parameters<typeof greet>; // [string, number]
```

#### InstanceType<T>
Получает тип экземпляра класса T.
```ts
class User {
    constructor(public name: string) {}
}

type UserInstance = InstanceType<typeof User>; // User
```

#### ThisType<T>
Позволяет указать тип this внутри объекта, используется в контексте object literals и с bind.

```ts
type Helper = {
    message: string;
};

const obj: ThisType<Helper> & {
    setMessage(msg: string): void;
    } = {
    setMessage(msg) {
    this.message = msg; // this имеет тип Helper
    }
};
```
`ThisType` не влияет сам по себе — он нужен в библиотеках и generic-коде, например, во Vue (data + methods).



### Уровень 3

### Strict-mode

`Strict Mode` в TypeScript — это специальный режим компилятора, который включает набор строгих проверок типов и правил, направленных на повышение качества и безопасности кода за счёт более жёсткой типизации и предупреждения потенциальных ошибок.

Включение флага --strict в конфигурации TypeScript (например, в tsconfig.json) активирует сразу несколько подфлагов, каждый из которых усиливает проверки:

* `strictNullChecks` — исключает возможность неявного использования null и undefined там, где ожидается другой тип. Это помогает избежать ошибок, связанных с null pointer exception (NPE).

* `noImplicitAny` — запрещает неявное присваивание типа any, заставляя явно указывать типы там, где компилятор не может их вывести.

* `noImplicitThis` — требует явного указания типа для this в функциях.

* `strictBindCallApply` — усиливает проверки при использовании методов bind, call и apply.

* `strictFunctionTypes` — строгая проверка совместимости типов функций, предотвращающая ошибки при передаче функций с несовместимыми типами параметров.

* `strictPropertyInitialization` — проверяет, что все свойства класса инициализированы в конструкторе или объявлены с дефолтными значениями.

* `alwaysStrict` — включает генерацию "use strict"; в выходных JavaScript-файлах, что активирует строгий режим исполнения JavaScript.

#### Перегрузка функций

Перегрузка функций в TypeScript — это возможность определить несколько вариантов одной функции с разными наборами параметров и возвращаемыми типами. Это позволяет одной функции работать с разными типами и количеством аргументов, обеспечивая более гибкий и типобезопасный код.

Как работает перегрузка функций в TypeScript
Сигнатуры перегрузки (Overload Signatures) — объявляются несколько вариантов функции с разными параметрами и возвращаемыми типами, но без реализации.

Сигнатура реализации (Implementation Signature) — одна функция с реализацией, которая объединяет все варианты, описанные в сигнатурах перегрузки. Внутри этой функции происходит проверка типов и логика, соответствующая разным вариантам вызова.

Пример перегрузки функции
```ts
// Сигнатуры перегрузки
function makeDate(timestamp: number): Date;
function makeDate(m: number, d: number, y: number): Date;

// Сигнатура реализации
function makeDate(mOrTimestamp: number, d?: number, y?: number): Date {
    if (d !== undefined && y !== undefined) {
    return new Date(y, mOrTimestamp, d);
    } else {
    return new Date(mOrTimestamp);
 }
}
```

#### Рекурсивные типы
Рекурсивные типы в TypeScript — это типы, которые ссылаются сами на себя в своем определении. 
Они позволяют описывать сложные вложенные структуры данных, например, деревья, JSON-объекты или связанные списки, с полной типобезопасностью.

Основная идея рекурсивных типов
Рекурсивный тип содержит в себе ссылку на сам себя,
что позволяет описать структуры с произвольной глубиной вложенности. 
Например, дерево, где каждый узел может содержать массив дочерних узлов того же типа:

```ts
type TreeNode<T> = {
  value: T;
  children: TreeNode<T>[];
};
```
Здесь TreeNode рекурсивно определён через себя — поле children это массив таких же узлов.

Пример: рекурсивный тип для JSON
JSON-объекты могут быть примитивами, массивами или объектами с ключами, значения которых тоже могут быть JSON. 
Это классический пример рекурсивного типа:
```ts
type JSONValue =
    | string
    | number
    | boolean
    | null
    | JSONObject
    | JSONArray;

interface JSONObject {
    [key: string]: JSONValue;
}

interface JSONArray extends Array<JSONValue> {}
```
Здесь JSONValue включает в себя JSONObject и JSONArray, 
которые в свою очередь содержат JSONValue — рекурсия позволяет описать вложенные структуры любой глубины.

#### Conditional types
`Conditional Types` (условные типы) позволяют создавать типы, 
которые зависят от других типов и вычисляются по определённому условию, похожему на тернарный оператор в JavaScript. 
Это мощный инструмент для создания гибких и динамичных типовых конструкций,
особенно полезный при разработке сложных и переиспользуемых библиотек.

```ts
type MyType<T> = T extends U ? X : Y;
```
Если тип T совместим с типом U, итоговый тип будет X.

В противном случае — Y.

Примеры
Пример 1: Проверка 
```ts
type IsString<T> = T extends string ? 'Yes' : 'No';

type Test1 = IsString<string>; // 'Yes'
type Test2 = IsString<number>; // 'No'
```
Здесь IsString возвращает 'Yes', если переданный тип — строка, иначе 'No'.

Пример 2: Выбор возвращаемого типа
```ts
type Result<T> = T extends string ? string[] : number[];

let a: Result<string>; // string[]
let b: Result<number>; // number[]
```

В зависимости от типа T, тип Result<T> будет либо массивом строк, либо массивом чисел.

Пример 3: Извлечение типа из Promise
```ts
type Awaited<T> = T extends Promise<infer R> ? R : T;

type A = Awaited<Promise<number>>; // number
type B = Awaited<string>;          // string
```
Ключевое слово `infer` позволяет извлекать вложенный тип из Promise.

Применение

* Создание универсальных утилит (например, Partial<T>, ReturnType<T>)

* Генерация типов на основе условий (например, для API-ответов)

* Работа с обобщёнными типами и сложными структурами данных

#### Выводимость типов
`Выводимость типов` (Type Inference) в TypeScript — это механизм, 
при котором компилятор сам определяет тип переменной, функции или выражения, 
даже если он не указан явно. Это позволяет писать меньше типовой аннотации, сохраняя при этом типовую безопасность.

1. Присваивание значения
```ts
let message = "Hello, world!"; // message: string
```
2. Функции
```ts
function add(a: number, b: number) {
  return a + b; // return type inferred as number
}
```
Если аргументы имеют явные типы, возвращаемое значение тоже будет выведено (number в этом случае).

3. Контекстная типизация (Contextual Typing)
   Тип определяется из контекста, например, при передаче функции как аргумента:
```ts
const numbers = [1, 2, 3];
    numbers.forEach(num => console.log(num)); // num: number
```

4. Деструктуризация
```ts
const point = { x: 10, y: 20 };
const { x, y } = point; // x: number, y: number
```

5. Типы в JSX/Vue
В <script setup lang="ts"> типы тоже часто выводятся автоматически:
```ts
const count = ref(0); // count: Ref<number>
```

Иногда TypeScript не может корректно вывести тип, и тогда лучше указать его явно:
```ts
// Плохо — тип будет (string | number)[]
const mixed = ["hello", 42];

// Лучше:
const mixed: (string | number)[] = ["hello", 42];
```

#### Mapped types
`Mapped types` в TypeScript — это способ создавать новые типы на основе существующих, проходясь по ключам типа и трансформируя их.

Активно используются внутри типов вроде `Partial`, `Readonly`, `Record`, `Pick`, `Omit` и т.д.

Общий синтаксис mapped type:
```ts
type MyMappedType<T> = {
  [K in keyof T]: SomeTransformation<T[K]>
}
```
* T — исходный тип.

* K in keyof T — перебираем все ключи типа T.

* SomeTransformation<T[K]> — можно изменить тип значения.

#### Дженерики

`Дженерики` (Generics) в TypeScript — это мощный механизм, позволяющий создавать универсальные, гибкие и многократно используемые компоненты (функции, классы, интерфейсы), которые могут работать с разными типами данных, сохраняя при этом строгую типизацию и безопасность типов.

Что такое дженерики?
Дженерики — это параметризированные типы, которые позволяют передавать типы как параметры в функции, классы или интерфейсы. Это похоже на передачу аргументов в функции, но вместо значений передаются типы. Благодаря этому можно писать один универсальный код, который будет работать с любыми типами данных, указанными при вызове.

Пример базовой функции с дженериком:
```ts
function identity<T>(arg: T): T {
  return arg;
}

let output = identity<string>("hello"); // output имеет тип string
```

Здесь T — параметр типа, который при вызове функции заменяется на конкретный тип (например, string), что позволяет функции принимать и возвращать значения этого типа.

Зачем нужны дженерики?
* Позволяют писать универсальный и переиспользуемый код, не дублируя функции для каждого типа.

* Обеспечивают безопасность типов, предотвращая ошибки во время компиляции.

* Позволяют избежать использования типа any, сохраняя строгую типизацию.

* Повышают читаемость и поддержку кода, делая его более понятным для других разработчиков.

Примеры использования
Универсальная функция
```ts
function firstElement<T>(arr: T[]): T {
  return arr[0];
}
```

Эта функция возвращает первый элемент массива любого типа.

Ограничения дженериков (Generic Constraints)
Иногда нужно ограничить типы, которые могут быть переданы в дженерик.
Например, если функция использует свойство length, нужно убедиться, что тип аргумента содержит это свойство:
```ts
interface Lengthwise {
  length: number;
}

function getLength<T extends Lengthwise>(arg: T): number {
  return arg.length;
}

getLength([1, 2, 3]); // 3
getLength("hello");   // 5
// getLength(123);    // Ошибка, у number нет length
```

Здесь T extends Lengthwise означает, что тип T должен иметь свойство length типа number.

Функция для получения значения свойства объекта по ключу с ограничением ключа
```ts
class Queue<T> {
  private data: T[] = [];

  push(item: T) {
    this.data.push(item);
  }

  pop(): T | undefined {
    return this.data.shift();
  }
}
```
Такой класс можно использовать для очереди чисел, строк или любых других типов.

В итоге, дженерики в TypeScript — это инструмент для создания гибкого, 
переиспользуемого и типобезопасного кода, который может работать с разными типами данных, что значительно улучшает качество и поддержку проектов.

### Уровень 4
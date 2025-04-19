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
  - [1️⃣ Прочие основные функции TS](#1️⃣-прочие-основные-функции-ts)
  - [2️⃣ Встроенные утилитарные типы TS](#2️⃣-встроенные-утилитарные-типы-ts)
- [Уровень 3](#уровень-3)
  - [1️⃣ Strict-mode](#1️⃣-strict-mode)
  - [2️⃣ Перегрузка функций](#2️⃣-перегрузка-функций)
  - [3️⃣ Рекурсивные типы](#3️⃣-рекурсивные-типы)
  - [4️⃣ Conditional types](#4️⃣-conditional-types)
  - [5️⃣ Выводимость типов](#5️⃣-выводимость-типов)
  - [6️⃣ Mapped types, Generics](#6️⃣-mapped-types)
- [Уровень 4](#уровень-4)
  - [1️⃣ Type soundness и Type safety](#1️⃣-type-soundness-и-type-safety)
  - [2️⃣ Инвариантность, ковариантность, контравариантность и бивариантность](#2️⃣-инвариантность-ковариантность-контравариантность-и-бивариантность)
  - [3️⃣ Полиморфизм в TS](#3️⃣-полиморфизм-в-ts)

  
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

### 4️⃣ Основные функции TS

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

### 1️⃣ Strict-mode

`Strict Mode` в TypeScript — это специальный режим компилятора, который включает набор строгих проверок типов и правил, направленных на повышение качества и безопасности кода за счёт более жёсткой типизации и предупреждения потенциальных ошибок.

Включение флага --strict в конфигурации TypeScript (например, в tsconfig.json) активирует сразу несколько подфлагов, каждый из которых усиливает проверки:

* `strictNullChecks` — исключает возможность неявного использования null и undefined там, где ожидается другой тип. Это помогает избежать ошибок, связанных с null pointer exception (NPE).

* `noImplicitAny` — запрещает неявное присваивание типа any, заставляя явно указывать типы там, где компилятор не может их вывести.

* `noImplicitThis` — требует явного указания типа для this в функциях.

* `strictBindCallApply` — усиливает проверки при использовании методов bind, call и apply.

* `strictFunctionTypes` — строгая проверка совместимости типов функций, предотвращающая ошибки при передаче функций с несовместимыми типами параметров.

* `strictPropertyInitialization` — проверяет, что все свойства класса инициализированы в конструкторе или объявлены с дефолтными значениями.

* `alwaysStrict` — включает генерацию "use strict"; в выходных JavaScript-файлах, что активирует строгий режим исполнения JavaScript.

#### 2️⃣ Перегрузка функций

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

#### 3️⃣ Рекурсивные типы
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

#### 4️⃣ Conditional types
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

#### 5️⃣ Выводимость типов
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

#### 6️⃣ Mapped types
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

#### 1️⃣ Type soundness и Type safety

`Type safety` (безопасность типов) в TypeScript с примером
TypeScript обеспечивает безопасность типов на этапе компиляции, то есть предупреждает о несоответствиях типов до запуска кода.

```ts
function add(a: number, b: number): number {
  return a + b;
}

add(5, 10);       // ОК
add(5, "hello");  // Ошибка компиляции: аргумент типа 'string' нельзя назначить параметру типа 'number'
```

`Type soundness` (корректность типов) и пример "несовершенной soundness" в TypeScript
Type soundness — это гарантия, что если код прошёл проверку типов, то во время выполнения не будет ошибок типов. TypeScript не гарантирует полную soundness, так как допускает некоторые небезопасные конструкции для совместимости с JavaScript.

```ts
let value: any = "I am a string";

let length: number = value.length;  // ОК, но value имеет тип any

value = 42;                        // Теперь value — число

console.log(length);               // length всё ещё содержит длину строки, но value — число, runtime не выдаст ошибку, но логика может сломаться
```

Или пример с утверждением типа (type assertion):

```ts
let someValue: unknown = "hello";

// Принудительное утверждение типа
let strLength: number = (someValue as string).length;  // Компилятор верит, что someValue — string

someValue = 123;

// Во время выполнения length будет вычислен для числа, что может привести к ошибке или неожиданному поведению
console.log(strLength);
```

Здесь TypeScript не может гарантировать, что утверждение типа корректно на этапе выполнения, поэтому type soundness нарушается.

Пример с защитниками типов (Type Guards) для повышения безопасности типов
TypeScript позволяет создавать защитники типов, чтобы уточнять типы во время выполнения и минимизировать ошибки.

```ts
function isString(value: unknown): value is string {
  return typeof value === "string";
}

function printLength(value: unknown) {
  if (isString(value)) {
    console.log(value.length);  // Безопасно, т.к. value — string
  } else {
    console.log("Not a string");
  }
}
```

Такой подход повышает type safety во время выполнения, снижая риск ошибок типов.

Итог
* Type safety в TypeScript — предотвращение ошибок типов на этапе компиляции (например, передача неправильного типа аргумента).

* Type soundness — формальная гарантия, что при корректном типе программа не упадёт с ошибкой типов во время выполнения. В TypeScript эта гарантия не абсолютна из-за гибкости и совместимости с JavaScript.

* Использование защитников типов (Type Guards) помогает повысить безопасность типов и приблизиться к soundness в реальных приложениях.

Эти примеры показывают, как TypeScript обеспечивает безопасность типов, но не всегда гарантирует полную soundness.

#### 2️⃣ Инвариантность, ковариантность, контравариантность и бивариантность

Вариантность — это способ, которым наследование между типами переносится на производные типы, такие как обобщённые типы, контейнеры, делегаты и т. п. Вариантность бывает трёх основных видов: инвариантность, ковариантность и контравариантность. Иногда упоминают и бивариантность, которая менее распространена и часто считается нежелательной с точки зрения безопасности типов.

`Инвариантность`
Инвариантность означает, что наследование между исходными типами не переносится на производные типы. То есть, если есть два типа A и B, где B — наследник A, то обобщённые типы Container<A> и Container<B> считаются несовместимыми и не связаны отношением наследования.

Пример:

```ts
class Animal {}
class Cat extends Animal {}

let animals: Array<Animal> = [new Animal()];
let cats: Array<Cat> = [new Cat()];

// Ошибка, потому что Array<T> в TypeScript инвариантен по T
animals = cats;  // Ошибка компиляции
```

Здесь нельзя присвоить Array<Cat> переменной типа Array<Animal>, потому что массивы в TypeScript инвариантны по типу элементов.

`Ковариантность`
Ковариантность — это ситуация, когда наследование между исходными типами сохраняется в том же направлении для производных типов. То есть если Cat наследуется от Animal, то Container<Cat> является наследником Container<Animal>.

Это часто встречается для типов, которые только читают данные (например, коллекции для чтения).

Пример:

```ts
class Animal {}
class Cat extends Animal {}

let cats: ReadonlyArray<Cat> = [new Cat()];
let animals: ReadonlyArray<Animal> = cats;  // Ковариантность — разрешено

// Можно читать животных из animals, но нельзя добавлять
let firstAnimal: Animal = animals[0];
```

ReadonlyArray<T> в TypeScript ковариантен по T, потому что он только читает элементы, не изменяя коллекцию.

`Контравариантность`
Контравариантность — это ситуация, когда наследование между исходными типами обращается в обратную сторону для производных типов. Если Cat наследуется от Animal, то Container<Animal> является наследником Container<Cat>.

Это характерно для типов, которые только принимают данные (например, функции с параметрами).

Пример:

```ts
class Animal {}
class Cat extends Animal {}

type Handler<T> = (arg: T) => void;

let animalHandler: Handler<Animal> = (animal) => console.log(animal);
let catHandler: Handler<Cat>;

// Контравариантность: Handler<Animal> можно присвоить Handler<Cat>
catHandler = animalHandler;  // Разрешено

catHandler(new Cat());  // Вызов корректен
```

Здесь функция, принимающая Animal, может использоваться там, где требуется функция, принимающая Cat, потому что она умеет обрабатывать любой Animal, а значит и Cat.

`Бивариантность`
Бивариантность — это ситуация, когда наследование между исходными типами переносится в обе стороны. То есть Container<A> и Container<B> считаются взаимозаменяемыми, даже если A и B связаны наследованием.

В программировании бивариантность обычно считается небезопасной, так как может приводить к ошибкам типов. Однако в некоторых языках (например, в TypeScript для некоторых случаев с функциями) она допускается ради удобства.

| Тип вариантности    | Отношение наследования между исходными типами | Отношение наследования между производными типами | Пример в программировании                         |
|---------------------|-----------------------------------------------|-------------------------------------------------|--------------------------------------------------|
| **Инвариантность**   | B ≤ A                                         | Container<B> и Container<A> не связаны          | Массивы в TypeScript (`Array<T>`)                 |
| **Ковариантность**   | B ≤ A                                         | Container<B> ≤ Container<A>                      | `ReadonlyArray<T>` в TypeScript, `IEnumerable<T>` в C# |
| **Контравариантность** | B ≤ A                                       | Container<A> ≤ Container<B>                      | Делегаты, функции с параметрами (`(T) => void`)   |
| **Бивариантность**   | B ≤ A                                         | Container<A> ↔ Container<B>                      | Иногда функции в TypeScript (небезопасно)          |


Визуализация (на примере дерева и плодов)
* Инвариантность — "Можно взять только конкретный плод с конкретной ветки" (например, только яблоки из ветки яблони).

* Ковариантность — "Можно взять плод с более широкой ветки" (например, яблоко или любой фрукт из дерева).

* Контравариантность — "Можно использовать более общий тип" (например, обработчик, который умеет работать с любым фруктом, может заменить обработчик для яблок).

Итоги
* Инвариантность — строгая несовместимость между параметризованными типами с разными параметрами.

* Ковариантность — позволяет использовать более конкретный тип там, где ожидается более общий.

* Контравариантность — позволяет использовать более общий тип там, где ожидается более конкретный.

* Бивариантность — допускает взаимозаменяемость в обе стороны, но часто небезопасна.

Эти концепции помогают создавать гибкие и при этом безопасные системы типов в языках программирования и особенно важны при работе с обобщёнными типами и функциями.


#### 3️⃣ Полиморфизм в TS

Полиморфизм в TypeScript — это способность функций, методов и объектов работать с разными типами данных через единый интерфейс или обобщённые конструкции. В TypeScript выделяют несколько основных видов полиморфизма:

Виды полиморфизма в TypeScript с примерами
`Полиморфизм подтипов` (Subtyping Polymorphism)
Это классический полиморфизм, основанный на наследовании или реализации интерфейсов. Объекты разных конкретных типов могут использоваться там, где ожидается базовый тип.

```ts
class Person {
  constructor(protected name: string) {}
  getName(): string {
    return this.name;
  }
}

class Guest extends Person {
  constructor(name: string, private age: number) {
    super(name);
  }
  getName(): string {
    return super.getName() + ' ' + this.age;
  }
}

function greet(p: Person) {
  console.log(p.getName());
}

const guest = new Guest("Alice", 30);
greet(guest);  // Работает, т.к. Guest — подтип Person
```

Здесь функция greet принимает объект типа Person, но можно передать и Guest — подтип Person.

`Параметрический полиморфизм` (Parametric Polymorphism)
Реализуется через дженерики (обобщённые типы). Позволяет писать функции и классы, которые работают с любыми типами, заданными параметром.

```ts
function identity<T>(arg: T): T {
  return arg;
}

const num = identity<number>(42);
const str = identity<string>("hello");
```

Функция identity одинаково работает с разными типами, заданными параметром T.

`Ад-хок полиморфизм` (Ad-hoc Polymorphism)
Это перегрузка функций или операторов — одна и та же функция может иметь несколько реализаций для разных типов.

```ts
function fn(a: number, b: number): string;
function fn(a: string, b?: number): string;
function fn(a: any, b?: any): string {
  if (typeof a === "number" && typeof b === "number") {
    return (a + b).toString();
  } else if (typeof a === "string") {
    return a.toUpperCase();
  }
  return "";
}
```

Такая перегрузка позволяет функции вести себя по-разному в зависимости от типов аргументов.

`Полиморфный тип this` (F-бounded полиморфизм)
TypeScript поддерживает полиморфный тип this в классах и интерфейсах, который позволяет методам возвращать тип текущего экземпляра, учитывая наследование.

```ts
class Box {
  set(value: string): this {
    // возвращаем текущий экземпляр с типом потомка
    return this;
  }
}

class ColorBox extends Box {
  setColor(color: string): this {
    return this;
  }
}

const box = new ColorBox();
box.set("value").setColor("red");  // цепочка вызовов с правильным типом this
```


Это позволяет методам в цепочках сохранять точный тип экземпляра, а не базового класса.

Кратко о полиморфизме в TypeScript

| Вид полиморфизма          | Описание                                         | Пример в TypeScript                              |
|--------------------------|-------------------------------------------------|-------------------------------------------------|
| Полиморфизм подтипов     | Использование объектов подтипов через базовый тип | Классы `Person` и `Guest` с общим методом       |
| Параметрический полиморфизм | Обобщённые функции и классы с параметрами типов | Дженерики `function identity<T>(arg: T): T`     |
| Ад-хок полиморфизм       | Перегрузка функций и операторов                  | Перегруженная функция `fn` с разными сигнатурами |
| Полиморфный тип `this`   | Методы с возвращаемым типом текущего экземпляра | Классы с методами, возвращающими `this`         |


Полиморфизм позволяет писать более гибкий, переиспользуемый и расширяемый код, что особенно важно в TypeScript с его статической типизацией и поддержкой дженериков.

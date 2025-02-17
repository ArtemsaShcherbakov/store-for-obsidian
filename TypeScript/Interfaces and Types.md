Принято считать, что с помощью интерфейсов описываются объекты и классы, а все остальное через типы (**union types, intersection, примитивов и сложных типов**). Это больше относиться к симантики ts. Описывать объекты можно как через типы, так и через интерфейсы.

```ts
// Через type
type User = {
  name: string;
  age: number;
};

// Через interface
interface UserInterface {
  name: string;
  age: number;
}

```

Работа с типами:
##### **Union** _(Объединение)_ - механизм, позволяющий создавать из множества существующих типов логическое условие, по которому данные могут принадлежать только к одному из указанных типов.

```ts
let a: Type1 | Type2 | Type3
```

##### **Intersection** (_Пересечение_) - позволяет рассматривать множество типов данных как единое целое. Переменной, которой был указан тип пересечение `A` и `B` и `С`, должно быть присвоено значение, принадлежащее к типам `A` и `B` и `C` одновременно.

```ts
class A {
  a: number;
}
class B {
  b: string;
}
class C {
  c: boolean;
}

let name: A & B & C; // значение должно принадлежать ко всем типам одновременно
```

##### **Discriminated Union** (Дискриминирующие объединения) - позволяет безопасно работать с объединёнными (`union`) типами в TypeScript, используя общий дискриминирующий ключ (discriminant).

Допустим, у нас есть два типа `Circle` и `Rectangle`, объединённые в `Shape`:

```ts
type Circle = {
  radius: number;
};

type Rectangle = {
  width: number;
  height: number;
};

type Shape = Circle | Rectangle;

```

Если мы хотим вычислить площадь (`area`), то TypeScript не знает, какой конкретный тип передан:

```ts
function getArea(shape: Shape): number {
  if (shape.radius) { // ❌ Ошибка: Свойство 'radius' не существует в типе 'Rectangle'.
    return Math.PI * shape.radius ** 2;
  }
  return shape.width * shape.height; // ❌ Ошибка: 'width' и 'height' не существуют в 'Circle'.
}

```

TypeScript не может гарантировать, что у `shape` есть `radius`, `width` или `height`. Добавляем **общее поле** (например, `kind`), которое позволяет однозначно определить тип объекта.

```ts
type Circle = {
  kind: "circle"; // Дискриминирующий ключ
  radius: number;
};

type Rectangle = {
  kind: "rectangle"; // Дискриминирующий ключ
  width: number;
  height: number;
};

type Shape = Circle | Rectangle;


function getArea(shape: Shape): number {
  if (shape.kind === "circle") {
    return Math.PI * shape.radius ** 2;
  } else {
    return shape.width * shape.height;
  }
}

console.log(getArea({ kind: "circle", radius: 5 })); // 78.54
console.log(getArea({ kind: "rectangle", width: 4, height: 5 })); // 20

```

Пример с обработкой событий: 

```ts
type ClickEvent = { type: "click"; x: number; y: number };
type KeyPressEvent = { type: "keypress"; key: string };

type Event = ClickEvent | KeyPressEvent;

function handleEvent(event: Event) {
  switch (event.type) {
    case "click":
      console.log(`Клик по координатам (${event.x}, ${event.y})`);
      break;
    case "keypress":
      console.log(`Нажата клавиша ${event.key}`);
      break;
  }
}
```

Работа с Интерфейсами

Интерфейсы можно расширять через наследование или слияния:

```ts
interface A {
	prop1: 'prop1'
}

interface B extends A {
	prop2: 'prop2'
}

// или

interface User {
  name: string;
}

interface User {
  age: number;
}

const person: User = { name: "Alice", age: 25 }; // Работает!
```

Интерфейсы лучше подходят для классов, так как их можно имплементировать.

```ts
interface Printable {
  print(): void;
}

class Document implements Printable {
  print() {
    console.log("Printing document...");
  }
}

```

Используйте `interface`, если:
	Определяете объект или класс
	Хотите использовать `extends`
	Планируете объединение типов

Используйте `type`, если:
	Определяете `union` или `intersection`
	Нужно описать примитивы
	Описываете сложные структуры данных

`interface` и `type` **не компилируются** в js и исчезают. Используется только во время разработки для проверки типов и исчезает после компиляции.

`Awaited<T>` — определяет тип, который будет возвращён из асинхронной функции.

```ts
async function getData(): Promise<string> {
    return 'hello';
}

let awaitedData: Awaited<ReturnType<typeof getData>>;
// теперь awaitedData может быть 'hello'
```

`Partial<T>` — делает все свойства объекта `T` необязательными.

```ts
interface Person {
  name: string;
  age: number;
}

let partialPerson: Partial<Person>;
// теперь partialPerson может быть { name?: string; age?: number; }
```

`Required<T>` — делает все свойства объекта `T` обязательными.

```ts
interface Person {
  name?: string;
  age?: number;
}

let requiredPerson: Required<Person>;
// теперь requiredPerson может быть { name: string; age: number; }
```

`Readonly<T>` — делает все свойства объекта `T` доступными только для чтения.

```ts
interface Point {
  x: number;
  y: number;
}

let readonlyPoint: Readonly<Point>;
// теперь readonlyPoint имеет тип { readonly x: number; readonly y: number; }
```

`Record<Keys, Type>` — создаёт объект с ключами `Keys` и значениями `Type`.

```ts
type Keys = 'a' | 'b' | 'c';
type RecordType = Record<Keys, number>;

let record: RecordType;
// теперь record имеет тип { a: number; b: number; c: number; }
```

`Pick<T, K>` — выбирает из `T` только указанные свойства `K`.

```ts
interface Person {
  name: string;
  age: number;
}

let pickedPerson: Pick<Person, 'name'>;
// теперь pickedPerson имеет тип { name: string; }
```

`Omit<T, K>` — удаляет указанные свойства `K` из `T`.

```ts
interface Person {
  name: string;
  age: number;
}

let omittedPerson: Omit<Person, 'age'>;
// теперь omittedPerson имеет тип { name: string; }
```

`Exclude<UnionType, ExcludedMembers>` — исключает из объединённого типа `UnionType` указанные типы `ExcludedMembers`.

```ts
type A = 'a' | 'b' | 'c';
type B = Exclude<A, 'a' | 'b'>;
// теперь B имеет тип 'c'
```

`Extract<Type, Union>` — извлекает из `Type` только те типы, которые присутствуют в `Union`.

```ts
type A = 'a' | 'b' | 'c';
type B = 'a' | 'b';
type C = Extract<A, B>;
// теперь C имеет тип 'a' | 'b'
```

`Parameters<Type>` — извлекает типы аргументов функции `Type`.

```ts
function foo(a: string, b: number) {}
type FooParameters = Parameters<typeof foo>;
// теперь FooParameters имеет тип [string, number]
```

`NonNullable<Type>` — удаляет `null` и `undefined` из `Type`.

```ts
let value: string | null | undefined;
let nonNullableValue: NonNullable<typeof value>;
// теперь nonNullableValue имеет тип string
```

`ReturnType<Type>` — извлекает тип возвращаемого значения функции `Type`.

```ts
function foo(): string { return 'hello'; }
type FooReturnType = ReturnType<typeof foo>;
// теперь FooReturnType имеет тип string
```

`InstanceType<Type>` — извлекает тип экземпляра класса `Type`.

```ts
class Foo { x: number }
type FooInstance = InstanceType<typeof Foo>;
// теперь FooInstance имеет тип { x: number }
```
Дженерики (Generics)  — это способ создания **обобщённого кода**, который может работать с разными типами данных, сохраняя их **безопасность**. Они позволяют писать более **гибкие и переиспользуемые** функции, классы и интерфейсы.

Когда используется `any`, мы теряем **проверку типов**, а с **дженериками** TypeScript сохраняет информацию о типах и проверяет их на этапе компиляции.

При использовании `any` теряется информация о типе, и TypeScript не может гарантировать, что мы используем переменные правильно.

```js
function identity(value: any): any {
  return value;
}

let result = identity(10); // TypeScript не знает, что result — число
result.toUpperCase(); // ошибка будет на этапе компиляции
```

С дженериками TypeScript сохраняет тип переданного аргумента и применяет его к `return`.

```js
const identity = <T>(value: T): T  => {
  return value;
}

let result = identity(10);
result.toUpperCase();  // Ошибка на этапе написание кода Property 'toUpperCase' does not exist on type 'number'.
```

Дженерики в интерфейсах и типах 

```js
interface Box<T> {
  content: T;
}

const stringBox: Box<string> = { content: "Hello" };
const numberBox: Box<number> = { content: 42 };
```

С помощью extends можно ограничивать дженерик (тип).

```js
type ID<T extends string | number> = {
  id: T;
};

const user1: ID<number> = { id: 123 }; //  ОК
const user2: ID<string> = { id: "abc" }; //  ОК
const user3: ID<boolean> = { id: true }; //  Ошибка
```


### Ограничения (Constraints) в дженериках

Можно **ограничить** дженерики, чтобы они соответствовали определённым требованиям.

Пример: функция работает **только с объектами**, у которых есть поле `length`:

```js
const getLength = <T extends { length: number }>(value: T): number  => {
  return value.length;
}

console.log(getLength('hello'));
console.log(getLength([1, 2, 3]));
```


### Пример использование Generics в React

```js
type ButtonProps<T> = {
  label: string;
  onClick: (data: T) => void;
};

function Button<T>({ label, onClick }: ButtonProps<T>) {
  return <button onClick={() => onClick({} as T)}>{label}</button>;
}

// Использование с разными типами
<Button<string> label="Click" onClick={(data) => console.log(data.length)} />;
<Button<number> label="Click" onClick={(data) => console.log(data.toFixed(2))} />;
```
Type guard — это некоторое выражение, которое выполняет проверку во время выполнения, гарантирующую тип в некоторой области видимости. Он помогает **избежать ошибок типов**, которые могут возникнуть при использовании `Union Types` или `any`.

```ts
const isNumber = (value: unknown): value is number => {
    return typeof value === 'number';
} 

const message:string = "hello world!";
console.log(isNumber(message)); // false
console.log(isNumber(10)); // true
```

**Главное отличие от обычной проверки `typeof`** — аннотация `value is number`. Она позволяет TypeScript **понимать, что после проверки значение точно является `number`**. Type Guard (`value is Type`) помогает **TypeScript понять тип внутри блока кода**.

```ts
function isString(value: unknown): value is string {
  return typeof value === "string";
}

function printLength(value: unknown) {
  if (isString(value)) {
    console.log(value.length); // TypeScript теперь знает, что это string
  }
}
```

Разница typeof в ts от js заключается в том, что typeof в ts можно использовать для получения типа переменной. В **TypeScript** `typeof variable` используется для **получения типа уже существующей переменной**. Это называется **Type Query** (_запрос типа_).

```ts
let message = "hello";
let newMessage: typeof message; // newMessage будет string

// or

const person = {
  name: "Alice",
  age: 25
};

type PersonType = typeof person; // { name: string; age: number; }
```

![[Pasted image 20250128180649.png]]
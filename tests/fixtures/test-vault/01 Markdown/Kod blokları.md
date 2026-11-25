# Kod blokları

```js
// JavaScript
const greet = (name) => `Merhaba, ${name}!`;
console.log(greet("Demirkan"));
```

```ts
interface Note { path: string; tags: string[] }
export function hasTag(n: Note, t: string): boolean {
  return n.tags.includes(t);
}
```

```python
def fib(n: int) -> int:
    return n if n < 2 else fib(n - 1) + fib(n - 2)
```

```bash
bun install && bun run dev
```

```vue
<template><button @click="count++">{{ count }}</button></template>
```

```
Dil belirtilmemiş kod bloğu.
    Girinti korunmalı.
```

~~~markdown
Tilde ile açılmış blok, içinde ``` üç backtick var.
~~~

    Dört boşlukla girintili eski tarz kod bloğu.

Kod bloğu içindeki [[link]] ve #etiket link ya da etiket SAYILMAMALI:

```
[[Bu bir link değil]] #buetiketdeğil
```

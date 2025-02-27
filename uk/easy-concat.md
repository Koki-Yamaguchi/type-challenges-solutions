---
id: 533
title: Concat
lang: uk
level: easy
tags: array
---

## Завдання

Створіть JavaScript функцію `Array.concat` використовуючи тільки систему типів.
Тип має приймати два аргументи.
Результатом має бути новий масив, що містить об'єднання двох вхідних масивів.

Наприклад:

```ts
type Result = Concat<[1], [2]> // [1, 2]
```

## Розв'язок

Працюючи з масивами в TypeScript, варіативні типи часто спрощують життя в моделюванні потрібної поведінки.
Вони дозволяють нам використовувати "spread" оператор (`...`) перед типом-параметром.
Зачекайте, зараз поясню.

Розгляньмо на прикладі нашого завдання варіативні типи детальніше.
Ми знаємо, що для реалізації об'єднання двох масивів в один мовою JavaScript, достатньо повернути новий масив, в якому, за допомогою `...`, з'єднати два вхідних:

```js
function concat(arr1, arr2) {
  return [...arr1, ...arr2];
}
```

Тобто, використовуючи оператор `...`, ми перебираємо елементи з першого масиву `arr1` і вставляємо їх в наш новий масив.
Те ж саме робимо й з масивом `arr2`.
В результаті, отримуємо новий масив, в якому зберігаються елементи з першого та другого.

Варіативні типи спрощують моделювання такої поведінки в системі типів.
Коли нам потрібно об'єднати два масиви на рівні типів, ми можемо повернути новий тип, що міститиме елементи з двох вхідних масивів.

```ts
type Concat<T, U> = [...T, ...U]
```

Зачекайте, в такому разі ми ж отримаємо помилку “A rest element type must be an array type.”.
TypeScript нам каже, що не може застосувати оператор `...` до наших типів-параметрів, бо вони не є масивами.
Виправмо це, вказавши, що ці типи будуть масивами:

```ts
type Concat<T extends unknown[], U extends unknown[]> = [...T, ...U]
```

## Посилання

- [Варіативні типи](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-0.html#variadic-tuple-types)

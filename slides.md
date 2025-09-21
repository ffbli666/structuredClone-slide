---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Deep copy 使用 structuredClone (❁´3`❁)╭♡
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply UnoCSS classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
---

# Deep copy 使用 structuredClone 
# (❁´3`❁)╭♡

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---

# What is structuredClone?

The structuredClone() method of the Window interface creates a deep clone of a given value using the structured clone algorithm.

The method also allows transferable objects in the original value to be transferred rather than cloned to the new object. Transferred objects are detached from the original object and attached to the new object; they are no longer accessible in the original object.

- native 用來做 object 的 deep copy 的 API
- 可以不用再 JSON.parse(JSON.stringify(object)); 
  - or 引用第三方 loadash.cloneDeep
  - or 自已寫一個遍步 object 的 copy


<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/features/slide-scope-style
-->

<style>
h1 {
  background-color: #rd;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# Supported types
- Null、Undefined、Boolean、Number、 BigInt、String、(not include Symbol)
- Array
- ArrayBuffer
- Boolean
- DataView
- Date
- Map
- Number
- Object objects: but only plain objects (e.g., from object literals).
- RegExp: but note that lastIndex is not preserved.
- Set
- String
- TypedArray

---

# structuredClone

![Can i use](/public/assets/img/structuredClone-CanIUse.png "Can i use")

<style>
h1 + p {
   opacity: 1;
}
</style>
---

# structuredClone
```js
const obj = {
    int: 1,
    string: "string",
    // func: () => { console.log("func") }, Function 不能被複製, 因為 throw error, 需要刪除
    childObj: { message: 'hello world' },
    array: [1, 2, 3, 4, 5],
    bool: true,
    nil: null,
    map: new Map([['key1', 'value1'], ['key2', 'value2']]),
    set: new Set([1, 2, 3, 4, 5]),
    date: new Date(),
    regex: /ab+c/i,
    // symbol: Symbol('sym'), Symbol 不能被複製, 因為 throw error, 需要刪除
    bigInt: BigInt(12345678901234567890),
    ArrayBuffer: new ArrayBuffer(8),
    typedArray: new Uint8Array([1, 2, 3, 4, 5]),
    car: new car("Ford"),
    undefined: undefined,
    // dom: helloDiv, dom 不能被複製, 因為 throw error, 需要刪除
    error: new Error('This is an error message'),
}
```

---

# structuredClone(obj)

![structuredClone(obj)](/public/assets/img/structuredClone(obj).png "structuredClone(obj)")

<style>
h1 + p {
   opacity: 1;
}
</style>

---

# JSON.parse(JSON.stringify(obj))
```js
const jsonObj = {
    int: 1,
    string: "string",
    func: () => { console.log("func") },
    childObj: { message: 'hello world' },
    array: [1, 2, 3, 4, 5],
    bool: true,
    nil: null,
    map: new Map([['key1', 'value1'], ['key2', 'value2']]),
    set: new Set([1, 2, 3, 4, 5]),
    date: new Date(),
    regex: /ab+c/i,
    symbol: Symbol('sym'),
    // bigInt: BigInt(12345678901234567890), bigInt 不能被複製, 因為 throw error, 需要刪除
    ArrayBuffer: new ArrayBuffer(8),
    typedArray: new Uint8Array([1, 2, 3, 4, 5]),
    car: new car("Ford"),
    undefined: undefined,
    dom: helloDiv,
    error: new Error('This is an error message'),
}

---

# JSON.parse(JSON.stringify(obj))

![JSON.parse(JSON.stringify(obj))](/public/assets/img/JSON.parse(JSON.stringify(obj)).png "JSON.parse(JSON.stringify(obj))")

<style>
h1 + p {
   opacity: 1;
}
</style>
---

# structuredClone VS. JSON.parse(JSON.stringify())
| structuredClone | JSON.parse(JSON.stringify())|
| --------------- | ------------- |
| 支援型態較完整 | 支援型態較少 |
| 需要較新版本的瀏覽器(2022年2月) | 大物件較慢 |

---
# Reference

- [structuredClone](https://developer.mozilla.org/en-US/docs/Web/API/Window/structuredClone)
- [Structured clone algorithm](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Structured_clone_algorithm)

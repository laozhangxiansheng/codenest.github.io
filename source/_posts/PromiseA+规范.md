---
title: PromiseA+规范
tags: Promise
index_img: https://cdn.houdemingxin.com/image/default/F07EA3DBA53744D4A2B16565EAF2E2B5-6-2.png
banner_img: https://cdn.houdemingxin.com/image/default/F07EA3DBA53744D4A2B16565EAF2E2B5-6-2.png
date: 2024-08-28 15:23:01
---

## PromiseA+规范

### 1. 术语

- Promise 是一个拥有 `then` 方法的对象或函数，其行为符合本规范。
- thenable 是定义了 `then` 方法的对象或函数。
- value 是任何合法的 JavaScript 值（包括 undefined, thenable, 或 promise）。
- exception 是一个使用 throw 语句抛出的值。
- reason 是一个表明 promise 为什么被拒绝的值。

### 2. 要求

#### 2.1 Promise 状态

一个 promise 必须处于以下三个状态之一：`pending`，`fulfilled`，或 `rejected`。

- 当处于 pending 状态时，promise：

  - 可能会转变为 `fulfilled` 状态并传递一个值给相应的 `onFulfilled` 回调函数。
  - 也可能会转变为 `rejected` 状态并传递一个值给相应的 `onRejected` 回调函数。

- 当处于 `fulfilled` 状态时，promise：

  - 必须不会转变为其他任何状态。
  - 必须有一个值，且这个值不能被改变。

- 当处于 `rejected` 状态时，promise：

  - 必须不会转变为其他任何状态。
  - 必须有一个值，且这个值不能被改变。

#### 2.2 then 方法

一个 promise 必须提供一个 `then` 方法以访问其当前值、最终值或拒绝原因。

promise 的 then 方法接收两个参数：

```javascript
promise.then(onFulfilled, onRejected);
```

- onFulfilled 和 onRejected 都是可选参数。

  - 如果 onFulfilled 不是函数，它必须被忽略。
  - 如果 onRejected 不是函数，它必须被忽略。

- 如果 onFulfilled 是一个函数：

  - 它必须在 promise 被 fulfilled 后调用，并且 promise 的值作为它的第一个参数。
  - 它不能被调用超过一次。
  - 它必须以函数的形式被调用（即没有 this 值）。

- 如果 onRejected 是一个函数：

  - 它必须在 promise 被 rejected 后调用，并且 promise 的拒绝原因作为它的第一个参数。
  - 它不能被调用超过一次。
  - 它必须以函数的形式被调用（即没有 this 值）。

- then 方法必须返回一个 promise。

```javascript
promise2 = promise1.then(onFulfilled, onRejected);
```

- 如果 onFulfilled 或 onRejected 抛出一个异常 e，promise2 必须以 e 为拒绝原因被拒绝。
- 如果 onFulfilled 是一个函数且返回一个值 x，运行 [[PromiseResolve]](promise2, x)。
- 如果 onRejected 是一个函数且返回一个值 x，运行 [[PromiseResolve]](promise2, x)。
- 如果 onFulfilled 不是函数且 promise1 被 fulfilled，promise2 必须以与 promise1 相同的值被 fulfilled。
- 如果 onRejected 不是函数且 promise1 被 rejected，promise2 必须以与 promise1 相同的原因被 rejected。

#### 2.3 Promise 解析过程

[[PromiseResolve]](promise, x) 的执行过程如下：

- 如果 promise 和 x 指向同一个对象，promise 必须以 TypeError 为拒绝原因被拒绝。
- 如果 x 是一个 thenable 对象，则尝试以 x 为基础执行，即尝试执行 x.then(resolvePromise, rejectPromise)：
  - 如果 resolvePromise 以值 y 为参数被调用，如果 y 不是 thenable，则用 y 作为 promise 的值，否则继续执行 [[PromiseResolve]](promise, y)。
  - 如果 rejectPromise 以原因 r 为参数被调用，则以 r 为拒绝原因拒绝 promise。
  - 如果 resolvePromise 和 rejectPromise 都被调用，或者被同一个参数调用多次，则第一次调用优先，后续调用都会被忽略。
  - 如果调用 then 方法抛出异常 e，则：
    - 如果 resolvePromise 或 rejectPromise 已经被调用，则忽略这个异常。
    - 否则，以 e 为拒绝原因拒绝 promise。
- 如果 x 不是 thenable 对象或函数，则用 x 作为 promise 的值，fulfill promise。
- 如果在尝试执行 x.then 时抛出异常 e，则：
  - 如果 resolvePromise 或 rejectPromise 已经被调用，则忽略这个异常。
  - 否则，以 e 为拒绝原因拒绝 promise。

### 3. 注意事项

- 本规范没有定义 promise 的构造函数，也没有定义如何创建一个 promise。本规范假定 promise 的构造函数是 Promise，Promise 的构造函数是 Promise 构造器。
- 本规范假定 promise 的 then 方法是 Promise.prototype.then，then 方法是 then 方法。
- 本规范假定 promise 的 resolve 方法是 Promise.resolve，resolve 方法是 resolve 方法。
- 本规范假定 promise 的 reject 方法是 Promise.reject，reject 方法是 reject 方法。
- 本规范假定 promise 的 all 方法是 Promise.all，all 方法是 all 方法。
- 本规范假定 promise 的 race 方法是 Promise.race，race 方法是 race 方法。
- 本规范假定 promise 的 any 方法是 Promise.any，any 方法是 any 方法。
- 本规范假定 promise 的 allSettled 方法是 Promise.allSettled，allSettled 方法是 allSettled 方法。
- 本规范假定 promise 的 catch 方法是 Promise.prototype.catch，catch 方法是 catch 方法。
- 本规范假定 promise 的 finally 方法是 Promise.prototype.finally，finally 方法是 finally 方法。

转载：https://promisesaplus.com/

## ES2020

#### 指数运算符

ES2016 新增了一个指数运算符 (\*\*)

```jsx
2 ** 2; // 4
2 ** 3; // 8
// 指数运算符的一个特点是右结合，而不是常见的左结合。多个指数运算符连用时，是从最右边开始计算的。
2 ** (3 ** 2); // 相当于2**（3**2）

// 指数运算符可以与等号结合，形成一个新的赋值运算符（**=）
let a = 2;
a **= 2; // 等同于 a = a * a
```

#### 链判断运算符

```jsx
const useName = message.body.user.firstName; // 错误的写法，容易报错

// 正确的写法
const useName =
	(message &&
		message.body &&
		message.body.user &&
		message.body.user.firstName) ||
	"default";

const fooInput = myForm.querySelector("input[name=foo]");
const fooValue = fooInput ? fooInput.value : undefined;

// 链判断运算符的写法

const useName = message?.body?.user.firstName;
const fooValue = myForm.querySelector("input[name=foo]")?.value; // 链判断运算符默认返回的是undefined
```

#### null 判断运算符

ES2020 引入一个新的 null 判断运算符 ?? ，他的行为类似 逻辑或 || ,但是只有运算符左侧的值为 null 或 undefined 时，才会返回右侧的值

```jsx
const num = 0;
const name = "";
console.log(num || 18); // default
console.log(name || "张三"); // 张三

// null 判断运算符
console.log(num ?? 18); // 0
console.log(name ?? "张三"); // ''
```

#### BigInt 数据类型

JavaScript 所有数字都保存为 64 为浮点数，这给数值带来两大限制。

- 一是数值的精度只能到 53 个二进制位（相当于 16 个十进制位），大于这个范围的整数，JS 无法精确计算
- 二是大于或等于 2 的 1024 次方的数值，会返回 Infinity
  为解决这个问题，ES2020 引入了一种新的数据类型 BigInt（大整数），这是 ECMAScript 的第八种数据类型。BigInt 只用来表示整数，没有位数的限制，任何位数的整数都可以精确表示。

```jsx
console.log(2 ** 1024); // Infinity

// bigint 类型如何表示？
const num = 23324n;
console.log(typeof num); // bigint
console.log(1n + 2n); // 3n
```

和其他数据类型一样，JS 也原生提供 BigInt 对象，可以作为构造函数生成 BigInt 类型的数值，转换规则 Number()一致

```jsx
const num = 134;
console.log(BigInt(num)); // 134n
```

#### Promise.allSettled()

Promise.allSettled()方法接受一组 Promise 实例作为参数，包装成一个新的 Promise 实例。只有等到所有这些参数实例都返回结果，不管是 fulfilled 还是 rejected，包装实例才会结束。该方法由 ES2020 引入。

```jsx
const promise_1 = new Promise((resolves, reject) => setTimeout(resolves, 100));
const promise_2 = new Promise((resolves, reject) => setTimeout(reject, 100));

Promise.allSettled([promise_1, promise_2]).then((data) => console.log(data));
// [
//   Object { status: "fulfilled", value: undefined},
//   Object { status: "rejected", reason: undefined}
// ]
```

#### import()函数动态引入

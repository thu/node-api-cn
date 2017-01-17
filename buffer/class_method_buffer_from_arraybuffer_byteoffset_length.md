<!-- YAML
added: v5.10.0
-->

* `arrayBuffer` {ArrayBuffer} [`TypedArray`] 或 [`ArrayBuffer`] 的 `.buffer` 属性
* `byteOffset` {Integer} 从 `arrayBuffer` 开始拷贝的位置。 **默认:** `0`
* `length` {Integer} 从 `arrayBuffer` 拷贝多少字节。
  **默认:** `arrayBuffer.length - byteOffset`

当传入一个 [`TypedArray`] 实例的 `.buffer` 属性的引用时，这个新建的 `Buffer` 会像 [`TypedArray`] 那样共享同一分配的内存。

例子：

```js
const arr = new Uint16Array(2);

arr[0] = 5000;
arr[1] = 4000;

// 与 `arr` 共享内存
const buf = Buffer.from(arr.buffer);

// 输出: <Buffer 88 13 a0 0f>
console.log(buf);

// 改变原始的 Uint16Array 也会改变 Buffer
arr[1] = 6000;

// 输出: <Buffer 88 13 70 17>
console.log(buf);
```

可选的 `byteOffset` 和 `length` 参数指定将与 `Buffer` 共享的 `arrayBuffer` 的内存范围。

例子：

```js
const ab = new ArrayBuffer(10);
const buf = Buffer.from(ab, 0, 2);

// 输出: 2
console.log(buf.length);
```

如果 `arrayBuffer` 不是一个 [`ArrayBuffer`]，则抛出 `TypeError` 错误。

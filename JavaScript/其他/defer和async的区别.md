## defer和async的区别

>  `浏览器碰到 `script` 脚本的顺序`
>
> 1.`<script src="a.js"></script>`
>
> 没有 defer 或 async，浏览器会立即加载并执行指定的脚本，“立即”指的是在渲染该 script 标签之下的文档元素之前，也就是说不等待后续载入的文档元素，读到就加载并执行。
>
> 2.`<script async src="a.js"></script>`
>
> 有 `async`，加载和渲染后续文档元素的过程将和 `a.js `的加载与执行并行进行（异步）。
>
> 3.`<script defer src="a.js"></script>`
>
> 有 defer，加载后续文档元素的过程将和 a.js 的加载并行进行（异步），但是 a.js 的执行要在所有元素解析完成之后，DOMContentLoaded 事件触发之前完成。
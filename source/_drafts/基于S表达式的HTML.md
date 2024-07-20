---
title: 基于S表达式的HTML
date: 2024-07-20
---

比如

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" name="viewport" />
    <title>Hello World</title>
  </head>
  <body>
    <h1>Hello, World!</h1>
    <div class="1">She says "Hi!"</div>
  </body>
</html>
```

可以写成

```lisp
(DOCTYPE html)
(html lang:"en"
  (head
    (meta charset:"UTF-8" name:"viewport")
    (title "Hello World")
  )
  (body
    (h1 "Hello, World!")
    (div class:"1" "She says \"Hi!\"")
  )
)
```

这样在保持功能不变的情况下可以大大节约网络带宽，比如这个例子： 221 bytes -> 189 bytes, 带宽占用减少约 14.5% ，而在大型网页的传输中可以节约更可观的资源；同时有更好的易读性。

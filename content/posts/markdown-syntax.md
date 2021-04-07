

+++

title = "Markdown 语法"
description = "本文介绍了Markdown 语法"
author = "adeng"
tags = [
    "markdown"
]
date = "2021-03-25"
categories = [
    "Write",
]
menu = "main"

mermaid = true

+++



```flow
flow
st=>start: Start
op=>operation: Your Operation
cond=>condition: Yes or No?
e=>end
st->op->cond
cond(yes)->e
cond(no)->o
```





```mermaid
sequenceDiagram 
客户->>银行柜台: 我要存钱  
银行柜台->>后台: 改一下这个账户数字哦  
后台->>银行柜台: 账户的数字改完了，明天起息  
银行柜台->>客户: 好了，给你回单 ，下一位
```


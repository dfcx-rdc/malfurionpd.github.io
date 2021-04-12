+++

title = "Hugo中使用Mermaid画图"
description = "本文介绍了Hugo中使用Mermaid画图的一种方式"
author = "adeng"
tags = [
    "markdown"
]
date = "2021-04-12"
categories = [
    "Write",
]
menu = "main"

mermaid = true

+++



使用Mermaid给Markdown增加更多的表现力。

在theme/hugo-theme-stack/layouts/partials/footer/customer.html中加入如下内容：

```html
{{ if .Params.mermaid }}
<script
  src="https://cdn.jsdelivr.net/npm/mermaid@8.8.2/dist/mermaid.min.js"
  integrity="sha256-KqisLh8jVMBRjpNkOhH5W9VWs+F6x6vQksLqxs7+x9A="
  crossorigin="anonymous"
></script>
<script>
  // Replace mermaid pre.code to div
  Array.from(document.getElementsByClassName("language-mermaid")).forEach(
    (el) => {
      el.parentElement.outerHTML = `<div class="mermaid">${el.innerText}</div>`;
    }
  );
</script>
<style>
  /* Set svg to center */
  .mermaid svg {
    display: block;
    margin: auto;
  }
</style>
{{ end }}
```

Hugo模板中添加了`if .Params.mermaid`的检查，避免所有页面都需要加载它。

在需要使用的Hugo页面，可以在Front Matter中添加一个配置 `mermaid = true`，显式指定使用Mermaid。 





# 参考

[使用Mermaid在hugo的Markdown中绘制UML]( https://note.qidong.name/2020/07/mermaid/)
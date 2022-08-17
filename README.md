# Markdown 试题

这是 Markdown 试题，主要记录一些刚接触 Markdown 或者只阅读了快速指南会遇到的一些易错点。

环境是符合 CommonMark 规范的渲染器，比如 GFM 和 Python-Markdown 等。

合格标准：使用 [babelmark3](https://babelmark.github.io) 这个测试工具进行校验，合格数量过半即可。

## 第 1 题

书写两个斜体的星号。

要求：禁止使用 HTML 转义字符，比如 &#95、&lowbar，可以使用 Markdown 的反斜杠转义。

备注：星号是指「*」。

<details>
    <summary>第 1 题的答案</summary>

```markdown
_\*\*_
```

此题考验的是<ruby>[反斜杠转义](https://spec.commonmark.org/0.30/#backslash-escapes)<rp>(</rp><rt>Backslash escapes</rt><rp>)</rp></ruby>。

</details>

## 第 2 题

书写两个加粗的下划线。

要求：禁止使用 HTML 转义字符，比如 &#95、&lowbar，可以使用 Markdown 的反斜杠转义。

备注：下划线是指「_」。

<details>
    <summary>第 2 题的答案</summary>

```markdown
**\_\_**
```

此题考验的是<ruby>[反斜杠转义](https://spec.commonmark.org/0.30/#backslash-escapes)<rp>(</rp><rt>Backslash escapes</rt><rp>)</rp></ruby>。

</details>

## 第 3 题

在<ruby>[内联元素](https://spec.commonmark.org/0.30/#inlines)<rp>(</rp><rt>Inlines</rt><rp>)</rp></ruby>中使用含有重音符「\`」（或者抑音符），请书写以下三条内容被内联元素包括住的样子。

1.  a\`b
2.  \`ab
3.  a\`\`b\`c\`\`\`d

要求：禁止使用 HTML 转义字符，比如 &#95、&lowbar，可以使用 Markdown 的反斜杠转义。

备注：内联元素在一些教程中可能会被叫做「代码」「单行代码」。

<details>
    <summary>第 3 题的答案</summary>

```markdown
``a`b``
`` `ab``
````a``b`c```d````
```

这是考验反斜杠转义并不适用于内联元素，需要使用其他的手段规避，比如内容中有一个重音符「\`」（或者抑音符），那么开头和结尾就可以使用两个重音符。

第二个答案稍微在不同的 Markdown 渲染器上有些差异，即最前方是否留下空格的问题，在这种情况下还是使用 HTML 转义字符比较好。
</details>

## 第 4 题

请描述下面的有序列表为什么会出错。

```markdown
前略

99. 第九十九条

    测试内容

100. 第一百条

    测试内容
```

<details>
    <summary>第 4 题的答案</summary>

这是一个超过 100 编号的有序列表，

并且每个列表都含有额外的多行内容。简单的来说，「99. 第九十九条」这段 Markdown 内容的「正文」部分的前面空了 4 个空位，而它下面同样是 4 个空格，所以是正常的。但「100. 第一百条」的「正文」部分的前面有 5 个空位，而它下面只有 4 个空格，造成了解析错误。

解决方式就是同步空位，将 100 以及之后的多行内容都要修改为 5 个空位才行，需要形成「对齐」的效果，不过等于小于 8 个空位也行，具体可以研究 CommonMark 规范。

</details>

## 第 5 题

```markdown
Markdown 对中文
的支持有些微妙，
《化物语》
《伪物语》
```

以上文字在 babelmark3 中会转换为：

```html
<p>Markdown 对中文
的支持有些微妙，
《化物语》
《伪物语》</p>
```

但下方的演示会显示「Markdown 对中文 的支持有些微妙， 《化物语》 《伪物语》」，在换行处增加了三处空格，这是怎么回事呢？

<details>
    <summary>第 5 题的答案</summary>

这是 babelmark3 出错了，它没有考虑到 CJK 亚洲的字符的情况，这也是部分解析器可能会出现的问题，尤其是基于 JavaScript 的渲染器，比如 Visual Studio Code 和 GitHub 的 Markdown 预览模式都有相同的问题，而 GitHub 在发送后才能看到正确渲染的内容。

</details>

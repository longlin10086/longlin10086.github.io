# Hugo ShortCode | 丰富你的 Markdown


<!--more-->
<br>

## Hugo ShortCode

> Hugo loves Markdown because of its simple content format, but there are times  when Markdown falls short. Often, content authors are forced to add raw HTML  (e.g., video `<iframe>`’s) to Markdown content. We think this contradicts the beautiful simplicity of Markdown’s syntax.

由 [Hugo 官方文档](https://gohugo.io/content-management/shortcodes/)中我们可以得知，为了在丰富 Markdown 文本的同时仍然保持其简约性，Hugo 创造了短代码对繁缛的 Html 进行替代。我们可以简单的将其理解为 Markdown 的一种插件，一种拓展语法，一个 template，它的出现为文本增添了许多新功能。

<br>

### 使用方法

短代码的常见格式为 `{{%/* shortcode parameter */%}}` 或 `{{</* shortcode parameter */>}}`

- shortcode 为我们所定义的方法，具体代码需要写在 `/layouts/shortcodes` 文件夹中新建的同名 html 文件里；parameter 则类似 css 中的标签，可以方便我们定位

- % 所包裹的代码内容会被 markdown 引擎渲染解析后再传入，而 <> 的代码内容不会被渲染
- 我们可以将其理解为 `{{</* shortcode */>}}` 的实质是将同名 `shortcode.html` 文件内容复制到 markdown 中并执行

和 `Html` 一样，shortcode 也有opening 和 closing 两种方式：

- opening: `{{%/* shortcode */%}}`
- closing: `{{%/* shortcode */%}} A bunch of code here {{%/* /shortcode */%}}`

如果参数过长，则可以考虑用以下形式传递：

```markdown
{{</*  myshortcode `This is some <b>HTML</b>,
and a new line with a "quoted string".` */>}}
```

<br>

下面是一个官方提供的 youtube 教程
{{< youtube Eu4zSaKOY4A >}}

<br>

### 简单语法

- `{{ .Inner }}` 获取 closing shortcode 中被包裹的所有内容
- `{{ .Get 'foo' }}` 获取参数名为 `foo` 的参数，注意其中 foo 两侧应该为反引号
- `{{ index .Params 0 }}` 获取 shortcode 中的**第一个参数**（和 c 语言中的数组一样，以 0 为起始位）

下面以一个具体例子进行说明：

1. 先创建 `/layouts/shortcodes/abbr.html`


2. 接下来在博客的 markdown 中写入：

```markdown
{{</* abbr title="Yahooooooooooooooooooooooooo~" text="Yaho~" */>}}
```

3. 现在我们便可以在之前所创建的 `abbr.html` 中进行编辑了，比如使用如下代码：

```html
<abbr title="{{ .Get `title` }}">
  {{ .Get `text` }}
</abbr>
```

4. 如此一来在 `./assets/css/_custom.scss` 这个自定义 css 文件中（如果你使用的也是 LoveIt 主题的话）我们就可以用 css 对刚才的代码块进行修饰，从而减轻我们在 markdown 中的书写负担（markdown 中只要写 shortcode 就行了，并且这种方法类似函数调用，复用性很高）

**例子在这（把鼠标放过来看看吧~）**：{{< abbr title="Yahooooooooooooooooooooooooo~" text="Yaho~" >}}

从官方文档我们可以发现，短代码能做的不只这些，它们组合起来可以进行很复杂的操作，条件判断，循环语句都有对应的短代码，它就像一款新的编程语言，只不过是针对博客上的元素进行操作。

并且，Hugo 官方已经帮我们实现好了不少 shortcode ，即取即用，它们被统称为 [Custom shortcode](https://gohugo.io/templates/shortcode-templates/)，在官网可以进行查看。

另外，在 LoveIt 主题中，诸如 bilibili , music 这些短代码也已经帮我们实现好了，具体可以在 `/theme/layouts/shortcodes` 里查看。

网上也有不少大佬对短代码进行了整理，现在也贴在下面以供读者查看：
- [山茶花舍的博客](https://irithys.com/p/hugo-shortcode-list)
- [书藏的博客](https://shuzang.github.io/2019/hugo-blog-article-write)

<br>

### 一些插曲
在写这篇博客时，我发现无论如何 `{{</* shortcode */>}}` 中的短代码都会比 markdown 语法更快渲染出来，导致网页因为无法识别未定义的 shortcode 而崩溃。为此我在 Google 上查了一个多小时，没有发现任何一篇中文博客提到了这点特性。最终在我将要放弃的时候居然在 [Hugo官方的Help界面](https://discourse.gohugo.io/t/how-to-write-text-shortcodes-so-it-will-not-rendering-as-shortcodes-in-markdown/20203) 发现了问题的答案。只需写成 `{{</* /*shortcode*/ */>}}` 就能正常让 shortcode stop rendering 从而被正常渲染。此外，不包含 <> 或 % 的短代码如果加上 `/* */` 反而是画蛇添足，正常书写即可。

与此同时，我在不经意间发现了 [风月大佬写的将近 5 万字 Hugo 博客详解](https://kuang.netlify.app/blog/hugo.html) , 让我受益匪浅，也大受震撼。

当下的互联网，太多人只是单纯从别人手中照抄照搬，这在中文互联网更是屡见不鲜。
别人的项目，稍微修改一下名字就当作自己的内容发布，这种低质量的水文遍地都是。
高质量的长篇博文却无人问津，甚至连被抄袭的可能性都失去，实在荒唐。
<br>
{{< mark >}}
满地六便士，我幻想成为月亮。
{{< /mark >}}


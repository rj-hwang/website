---
layout: blog
title: Markdown 与 HTML 间的映射
---

{{page.title}}
---
用易读易写的 Markdown 撰写常规的博客文章，没有了 HTML 复杂标签的干扰，写起来很是得心应手，很是对得起易读易写这个终极目标。为了方便记忆、翻查，特将最近用到的一些Markdown 语法摘记在此。

### 标题

<table style="float:left;margin-bottom:.25em">
<tr><th>Markdown</th><th>HTML</th></tr>
<tr><td># 标题</td><td>&lt;h1&gt;标题&lt;/h1&gt;</td></tr>
<tr><td>## 标题</td><td>&lt;h2&gt;标题&lt;/h2&gt;</td></tr>
<tr><td>### 标题</td><td>&lt;h3&gt;标题&lt;/h3&gt;</td></tr>
<tr><td>#### 标题</td><td>&lt;h4&gt;标题&lt;/h4&gt;</td></tr>
<tr><td>##### 标题</td><td>&lt;h5&gt;标题&lt;/h5&gt;</td></tr>
<tr><td>###### 标题</td><td>&lt;h6&gt;标题&lt;/h6&gt;</td></tr>
</table>
<table style="float:left;margin-left:2px">
<tr><th colspan="2">效果</th></tr>
<tr><td><h1>h1 标题</h1></td><td><h4>h4 标题</h4></td></tr>
<tr><td><h2>h2 标题</h2></td><td><h5>h5 标题</h5></td></tr>
<tr><td><h3>h3 标题</h3></td><td><h6>h6 标题</h6></td></tr>
</table>
<div style="clear:both"></div>

### 样式

<table>
<tr><th>Markdown</th><th>HTML</th><th>效果</th></tr>
<tr><td>*斜体*</td><td>&lt;em&gt;斜体&lt;/em&gt;</td><td><em>斜体</em></td></tr>
<tr><td>_斜体_</td><td>&lt;em&gt;斜体&lt;/em&gt;</td><td><em>斜体</em></td></tr>
<tr><td>**粗体**</td><td>&lt;strong&gt;粗体&lt;/strong&gt;</td><td><strong>粗体</strong></td></tr>
<tr><td>__粗体__</td><td>&lt;strong&gt;粗体&lt;/strong&gt;</td><td><strong>粗体</strong></td></tr>
</table>

### 段落与换行

一个 Markdown 段落是由一个或多个连续的文本行组成，它的前后要有一个以上的空行。转换为 HTML 后为 `<p>段落文本</p>`。若要 Markdown 插入 `<br>` 标签换行，则在行尾添加不少于两个空格然后回车。

### 链接

`[显示文本](链接地址)` 或 `[显示文本](链接地址 "提示信息")`
<table>
<tr><th>Markdown</th><th>HTML</th><th>效果</th></tr>
<tr><td>[Text](http://my.com)</td><td>&lt;a href="http://my.com"&gt;Text&lt;/a&gt;</td><td><a href="http://my.com">http://my.com</a></td></tr>
<tr><td>[Text](http://my.com "Title")</td><td>&lt;a href="http://my.com" title="Title"&gt;Text&lt;/a&gt;</td><td><a href="http://my.com" title="Title">http://my.com</a></td></tr>
</table>

### 自动链接

`<链接地址或邮箱地址>`
<table>
<tr><th>Markdown</th><th>HTML</th><th>效果</th></tr>
<tr><td>&lt;http://my.com&gt;</td><td>&lt;a href="http://my.com"&gt;http://my.com&lt;/a&gt;</td><td><a href="http://my.com">http://my.com</a></td></tr>
<tr><td>&lt;ad@my.com&gt;</td><td>&lt;a href="mailto:ad@my.com"&gt;ad@my.com&lt;/a&gt;</td><td><a href="mailto:ad@my.com">ad@my.com</a></td></tr>
</table>

### 图片

`![](图片链接地址)`

注：图片语法和链接语法相似，只是前面多了一个英文的 `!` 号。

### 无序列表

<table>
<tr><th>Markdown</th><th>HTML</th><th>效果</th></tr>
<tr>
  <td>* A<br>* B<br></td>
  <td>&lt;ul&gt;<br>
      &nbsp;&nbsp;&lt;li&gt;A&lt;/li&gt;<br>
      &nbsp;&nbsp;&lt;li&gt;B&lt;/li&gt;<br>
    &lt;/ul&gt;
  </td>
  <td><ul><li>A</li><li>B</li></ul></td>
<tr>
</tr>
  <td>* A<br><br>* B<br></td>
  <td>&lt;ul&gt;<br>
      &nbsp;&nbsp;&lt;li&gt;&lt;p&gt;A&lt;/p&gt;&lt;/li&gt;<br>
      &nbsp;&nbsp;&lt;li&gt;&lt;p&gt;B&lt;/p&gt;&lt;/li&gt;<br>
    &lt;/ul&gt;
  </td>
  <td><ul><li><p>A</p></li><li><p>B</p></li></ul></td>
</tr>
</table>

注：格式为符号＋不少于一个空格，符号为 \*(星号)、\-(减号)、\+(加号) 任一均可。如果列表项目间用空行分开，在输出 HTML 时 Markdown 就会将项目内容用 `<p>` 标签包起来。

### 有序列表

<table>
<tr><th>Markdown</th><th>HTML</th><th>效果</th></tr>
<tr>
  <td>1. A<br>1. B<br></td>
  <td>&lt;ol&gt;<br>
      &nbsp;&nbsp;&lt;li&gt;A&lt;/li&gt;<br>
      &nbsp;&nbsp;&lt;li&gt;B&lt;/li&gt;<br>
    &lt;/ol&gt;
  </td>
  <td><ol><li>A</li><li>B</li></ol></td>
<tr>
</tr>
  <td>2. A<br><br>2. B<br></td>
  <td>&lt;ol&gt;<br>
      &nbsp;&nbsp;&lt;li&gt;&lt;p&gt;A&lt;/p&gt;&lt;/li&gt;<br>
      &nbsp;&nbsp;&lt;li&gt;&lt;p&gt;B&lt;/p&gt;&lt;/li&gt;<br>
    &lt;/ol&gt;
  </td>
  <td><ol><li><p>A</p></li><li><p>B</p></li></ol></td>
</tr>
</table>

注：格式为数字＋英文句点＋不少于一个空格，句点前使用的数字并不影响实际输出的 HTML 结果。如果列表项目间用空行分开，在输出 HTML 时 Markdown 就会将项目内容用 `<p>` 标签包起来。

### 代码块

<table>
<tr><th>Markdown</th><th>HTML</th><th>效果</th></tr>
<tr>
  <td style="text-align:center">`代码`</td>
  <td>&lt;code&gt;代码&lt;/code&gt;</td>
  <td style="text-align:center"><code>代码</code></td>
<tr>
</tr>
  <td>(至少1个空行)<br>····function a() {<br>········var a = 1;<br>····}<br>(至少1个空行)
  </td>
  <td>&lt;pre&gt;&lt;code&gt;function a() {<br>
····var a = 1;<br>
}&lt;/code&gt;&lt;/pre&gt;
  </td>
  <td><pre><code>function a() {
····var a = 1;
}</code></pre></td>
</tr>
</tr>
  <td>(至少1个空行)<br>~~~<br>function a() {<br>····var a = 1;<br>}<br>~~~<br>(至少1个空行)
  </td>
  <td>&lt;pre&gt;&lt;code&gt;function a() {<br>
····var a = 1;<br>
}&lt;/code&gt;&lt;/pre&gt;
  </td>
  <td><pre><code>function a() {
····var a = 1;
}</code></pre></td>
</tr>
</table>

#### 注：建立 `pre` 代码块有两种方式：
1. 简单地缩进 4 个空格或是 1 个制表符，代码块会一直持续到无缩进的那一行（或文件结尾）。每行一阶的缩进（4 个空格或是 1 个制表符）在生成的 HTML 中都会被移除。
2. 用两行波浪号（每行至少带 3 个连续的波浪号 `~` ）包住代码块，这种方式的好处是不需要方式 1 那样缩进 4 个空格或 1 个制表符。同时可以在第一行波浪号的末尾指定代码所使用的语言；这可以充分利用 CSS 高亮显示代码的关键字。

在代码块里面 `&、<、>` 会自动转成 HTML 实体 `&amp;、&lt;、&gt;`。

### 引用

<table>
<tr><th>Markdown</th><th>HTML</th><th>效果</th></tr>
<tr>
  <td>&gt; 引用文字</td>
  <td>&lt;blockquote&gt;&lt;p&gt;引用文字&lt;/p&gt;&lt;/blockquote&gt;</td>
  <td><blockquote>引用文字</blockquote></td>
</tr>
<tr>
  <td>&gt; 引用<br>&gt; 文字</td>
  <td>&lt;blockquote&gt;&lt;p&gt;引用文字&lt;/p&gt;&lt;/blockquote&gt;</td>
  <td><blockquote>引用文字</blockquote></td>
</tr>
<tr>
  <td>&gt; 引用<br>&nbsp;&nbsp;&nbsp;文字</td>
  <td>&lt;blockquote&gt;&lt;p&gt;引用文字&lt;/p&gt;&lt;/blockquote&gt;</td>
  <td><blockquote>引用文字</blockquote></td>
</tr>
<tr>
  <td>&gt; 引用<br>&gt; &gt; 嵌套<br>&gt; 文字</td>
  <td>&lt;blockquote&gt;<br>
  &nbsp;&nbsp;&nbsp;&nbsp;&lt;p&gt;引用&lt;/p&gt;<br>
  &nbsp;&nbsp;&nbsp;&nbsp;&lt;blockquote&gt;<br>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;p&gt;嵌套&lt;/p&gt;<br>
  &nbsp;&nbsp;&nbsp;&nbsp;&lt;/blockquote&gt;<br>
  &nbsp;&nbsp;&nbsp;&nbsp;&lt;p&gt;文字&lt;/p&gt;<br>
  &lt;/blockquote&gt;
  </td>
  <td><blockquote>
    <p>引用</p>
    <blockquote><p>嵌套</p></blockquote>
    <p>文字</p>
    </blockquote>
  </td>
</tr>
<tr>
  <td>&gt; 引用<br>&gt; 1. A<br>&gt; 1. B<br>&gt; 文字</td>
  <td>&lt;blockquote&gt;<br>
  &nbsp;&nbsp;&nbsp;&nbsp;&lt;p&gt;引用&lt;/p&gt;<br>
  &nbsp;&nbsp;&nbsp;&nbsp;&lt;ol&gt;<br>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;li&gt;A&lt;/li&gt;<br>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;li&gt;B&lt;/li&gt;<br>
  &nbsp;&nbsp;&nbsp;&nbsp;&lt;/ol&gt;<br>
  &nbsp;&nbsp;&nbsp;&nbsp;&lt;p&gt;文字&lt;/p&gt;<br>
  &lt;/blockquote&gt;
  </td>
  <td><blockquote>
    <p>引用</p>
    <ol><li>A</li><li>B</li></ol>
    <p>文字</p>
    </blockquote>
  </td>
</tr>
</table>

### 水平分隔线

在一行中用不少于三个的星号`***`、减号（破折号）`---`或下划线（底线）`___`来建立一个分隔线，行内不能有其他东西。注意若使用减号且上一行是文字，将不是生成 `<hr>` 而是生成 `<h2>文字</h2>`，因此若要保证生成 `<hr>`，只需在前面添加一个空行即可。

<table>
<tr><th>Markdown</th><th>HTML</th><th>效果</th></tr>
<tr><td>___</td><td rowspan="3">&lt;hr&gt;</td><td rowspan="3"><hr></td></tr>
<tr><td>---</td></tr>
<tr><td>***</td></tr>
</table>

### 反斜杠

TODO

### 友情链接
[kramdown Quick Reference](http://kramdown.gettalong.org/quickref.html){:target="_blank"}

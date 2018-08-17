
[TOC]

>[danger] # 基本语法

模板引擎统一使用了 `{{` 和 `}}` 作为左右标签，没有其他的标签符号。

使用 `.` 来访问当前对象的值(模板全局变量)。

使用 `$` 来引用当前模板根级的上下文。

使用 `$var` 来访问特定的模板变量。


**模板中支持的 go 语言符号**

```
{{"string"}}     // 一般 string
{{`raw string`}} // 原始 string
{{'c'}}          // byte
{{print nil}}    // nil 也被支持
```

**模板中的 pipeline**

可以是上下文的变量输出，也可以是函数通过管道传递的返回值

```
{{. | FuncA | FuncB | FuncC}}
```

当 pipeline 的值等于:

* false 或 0
* nil 的指针或 interface
* 长度为 0 的 array, slice, map, string

那么这个 pipeline 被认为是空

>[success] ## if ... else ... end

```
{{if pipeline}}{{end}}
```

if 判断时，pipeline 为空时，相当于判断为 false


支持嵌套的循环

```
{{if .condition}}
{{else}}
	{{if .condition2}}{{end}}
{{end}}
```

也可以使用 else if 进行

```
{{if .condition}}
{{else if .condition2}}
{{else}}
{{end}}
```

>[success] ## range ... end

```
{{range pipeline}}{{.}}{{end}}
```

pipeline 支持的类型为 array, slice, map, channel

range 循环内部的 `.` 改变为以上类型的子元素

对应的值长度为 0 时，range 不会执行，`.` 不会改变

>[success] ## with ... end

```
{{with pipeline}}{{end}}
```

with 用于重定向 pipeline

```
{{with .Field.NestField.SubField}}
	{{.Var}}
{{end}}
```


>[success] ## define

define 可以用来定义自模板，可用于模块定义和模板嵌套

```
{{define "loop"}}
	<li>{{.Name}}</li>
{{end}}
```

使用 template 调用模板

```
<ul>
	{{range .Items}}
		{{template "loop" .}}
	{{end}}
</ul>
```

>[success] ## template

```
{{template "模板名" pipeline}}
```

将对应的上下文 pipeline 传给模板，才可以在模板中调用。


>[success] ## include

**该标签为gf模板引擎新增标签**

```
{{include "模板文件名(需要带完整文件名后缀)" pipeline}}
```

在模板中可以使用include标签载入其他模板，并且使用当前模板引擎已有的数据对于模板的分模块处理很有用处。模板文件名支持相对路径以及文件的系统绝对路径。如果想要把当前模板的模板变量传递给子模板(嵌套模板)，可以这样：
```
{{include "模板文件名" .}}
```

>[success] ## 注释

允许多行文本注释，不允许嵌套

```
{{/* 
comment content
support new line
*/}}
```
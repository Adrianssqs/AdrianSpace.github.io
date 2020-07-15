---
layout: article
title: Sass总结与归纳（下）
tags: sass
key: article-sass-2
---

> 简介：Sass 是一款强化 CSS 的辅助工具，它在 CSS 语法的基础上增加了变量 (variables)、嵌套 (nested rules)、混合 (mixins)、导入 (inline imports) 等高级功能，这些拓展令 CSS 更加强大与优雅。使用 Sass 以及 Sass 的样式库（如 Compass）有助于更好地组织管理样式文件，以及更高效地开发项目。

<!--more-->

> 本篇是对Sass的归纳总结，通过使用Sass也可以像写js一样调用变量，编写函数以及判断、循环，甚至只用样式就写出轮播图的逻辑，而不用像以前那样，不只写样式，还要单独写js才能实现。通过阅读Sass的文档，发现css这块还是有很大提升空间的。

### 6. 控制指令 (Control Directives)

  SassScript 提供了一些基础的控制指令，比如在满足一定条件时引用样式，或者设定范围重复输出格式。控制指令是一种高级功能，日常编写过程中并不常用到，主要与混合指令 (mixin) 配合使用，尤其是用在 Compass 等样式库中。

  - **6.1. @if**

    当 `@if` 的表达式返回值不是 `false` 或者 `null` 时，条件成立，输出 `{}` 内的代码：

    ```scss
      p {
        @if 1 + 1 == 2 { border: 1px solid; }
        @if 5 < 3 { border: 2px dotted; }
        @if null  { border: 3px double; }
      }
    ```

    编译为

    ```css
      p {
        border: 1px solid; }
    ```

    `@if` 声明后面可以跟多个 `@else if` 声明，或者一个 `@else` 声明。如果 `@if` 声明失败，Sass 将逐条执行 `@else if` 声明，如果全部失败，最后执行 `@else` 声明，例如：

    ```scss
      $type: monster;
      p {
        @if $type == ocean {
          color: blue;
        } @else if $type == matador {
          color: red;
        } @else if $type == monster {
          color: green;
        } @else {
          color: black;
        }
      }
    ```

    编译为

    ```css
      p {
        color: green; }
    ```

  - **6.2. @for**

    `@for` 指令可以在限制的范围内重复输出格式，每次按要求（变量的值）对输出结果做出变动。这个指令包含两种格式：`@for $var from <start> through <end>`，或者 `@for $var from <start> to <end>`，区别在于 through 与 to 的含义：当使用 through 时，条件范围包含 `<start>` 与 `<end>` 的值，而使用 to 时条件范围只包含 `<start>` 的值不包含 `<end>` 的值。另外，`$var` 可以是任何变量，比如 `$i`；`<start>` 和 `<end>` 必须是整数值。

    ```scss
      @for $i from 1 through 3 {
        .item-#{$i} { width: 2em * $i; }
      }
    ```

    编译为

    ```css
      .item-1 {
        width: 2em; }
      .item-2 {
        width: 4em; }
      .item-3 {
        width: 6em; }
    ```

  - **6.3. @each**

    `@each` 指令的格式是 `$var in <list>`, `$var` 可以是任何变量名，比如 `$length` 或者 `$name`，而 `<list>` 是一连串的值，也就是值列表。

    `@each` 将变量 `$var` 作用于值列表中的每一个项目，然后输出结果，例如：

    ```scss
      @each $animal in puma, sea-slug, egret, salamander {
        .#{$animal}-icon {
          background-image: url('/images/#{$animal}.png');
        }
      }
    ```

    编译为

    ```css
      .puma-icon {
        background-image: url('/images/puma.png'); }
      .sea-slug-icon {
        background-image: url('/images/sea-slug.png'); }
      .egret-icon {
        background-image: url('/images/egret.png'); }
      .salamander-icon {
        background-image: url('/images/salamander.png'); }
    ```

    - **6.3.1 多重数组 Multiple Assignment**

      `@each`指令也可以使用多个变量，如`$var1`，`$var2`... 子列表的每个元素都分配给相应的变量。例如：

      ```scss
        @each $animal, $color, $cursor in (puma, black, default),
                                          (sea-slug, blue, pointer),
                                          (egret, white, move) {
          .#{$animal}-icon {
            background-image: url('/images/#{$animal}.png');
            border: 2px solid $color;
            cursor: $cursor;
          }
        }
      ```

      编译为

      ```css
        .puma-icon {
          background-image: url('/images/puma.png');
          border: 2px solid black;
          cursor: default; }
        .sea-slug-icon {
          background-image: url('/images/sea-slug.png');
          border: 2px solid blue;
          cursor: pointer; }
        .egret-icon {
          background-image: url('/images/egret.png');
          border: 2px solid white;
          cursor: move; }
      ```

      同样适用于键值对的列表：

      ```scss
        @each $header, $size in (h1: 2em, h2: 1.5em, h3: 1.2em) {
          #{$header} {
            font-size: $size;
          }
        }
      ```

      编译为

      ```css
        h1 {
          font-size: 2em; }
        h2 {
          font-size: 1.5em; }
        h3 {
          font-size: 1.2em; }
      ```

  - **6.4. @while**

    `@while` 指令重复输出格式直到表达式返回结果为 `false`。这样可以实现比 `@for` 更复杂的循环，只是很少会用到。例如：

    ```scss
      $i: 6;
      @while $i > 0 {
        .item-#{$i} { width: 2em * $i; }
        $i: $i - 2;
      }
    ```

    编译为

    ```css
      .item-6 {
        width: 12em; }

      .item-4 {
        width: 8em; }

      .item-2 {
        width: 4em; }
    ```

### 7. 混合指令 (Mixin Directives)

  - **7.1. 定义混合指令 @mixin (Defining a Mixin: @mixin)**

    混合指令的用法是在 `@mixin` 后添加名称与样式，比如名为 `large-text` 的混合通过下面的代码定义：

    ```scss
      @mixin large-text {
        font: {
          family: Arial;
          size: 20px;
          weight: bold;
        }
        color: #ff0000;
      }
    ```

    混合也需要包含选择器和属性，甚至可以用 `&` 引用父选择器：

    ```css
      @mixin clearfix {
        display: inline-block;
        &:after {
          content: ".";
          display: block;
          height: 0;
          clear: both;
          visibility: hidden;
        }
        * html & { height: 1px }
      }
    ```

  - **7.2. 引用混合样式 @include (Including a Mixin: @include)**

    使用 `@include` 指令引用混合样式，格式是在其后添加混合名称，以及需要的参数（可选）：

    ```scss
      .page-title {
        @include large-text;
        padding: 4px;
        margin-top: 10px;
      }
    ```

    编译为

    ```css
      .page-title {
        font-family: Arial;
        font-size: 20px;
        font-weight: bold;
        color: #ff0000;
        padding: 4px;
        margin-top: 10px; }
    ```

    也可以在最外层引用混合样式，不会直接定义属性，也不可以使用父选择器。

    ```scss
      @mixin silly-links {
        a {
          color: blue;
          background-color: red;
        }
      }
      @include silly-links;
    ```

    编译为

    ```css
      a {
        color: blue;
        background-color: red; }
    ```

    > <b style="color:red;">混合样式中应该只定义后代选择器，这样可以安全的导入到文件的任何位置。</b>

  - **7.3. 参数 (Arguments)**

    参数用于给混合指令中的样式设定变量，并且赋值使用。在定义混合指令的时候，按照变量的格式，通过逗号分隔，将参数写进圆括号里。引用指令时，按照参数的顺序，再将所赋的值对应写进括号：

    ```scss
      @mixin sexy-border($color, $width) {
        border: {
          color: $color;
          width: $width;
          style: dashed;
        }
      }
      p { @include sexy-border(blue, 1in); }
    ```

    编译为

    ```css
      p {
        border-color: blue;
        border-width: 1in;
        border-style: dashed; }
    ```

    混合指令也可以使用给变量赋值的方法给参数设定默认值，然后，当这个指令被引用的时候，如果没有给参数赋值，则自动使用默认值：

    ```scss
      @mixin sexy-border($color, $width: 1in) {
        border: {
          color: $color;
          width: $width;
          style: dashed;
        }
      }
      p { @include sexy-border(blue); }
      h1 { @include sexy-border(blue, 2in); }
    ```

    编译为

    ```css
      p {
        border-color: blue;
        border-width: 1in;
        border-style: dashed; }

      h1 {
        border-color: blue;
        border-width: 2in;
        border-style: dashed; }
    ```

    - **7.3.1 关键词参数 (Keyword Arguments)**

      混合指令也可以使用关键词参数，上面的例子也可以写成：

      ```
        p { @include sexy-border($color: blue); }
        h1 { @include sexy-border($color: blue, $width: 2in); }
      ```

      > 虽然不够简明，但是阅读起来会更方便。关键词参数给函数提供了更灵活的接口，以及容易调用的参数。关键词参数可以打乱顺序使用，如果使用默认值也可以省缺，另外，参数名被视为变量名，下划线、短横线可以互换使用。

    - **7.3.2 参数变量 (Variable Arguments)**

      有时，不能确定混合指令需要使用多少个参数，比如一个关于 `box-shadow` 的混合指令不能确定有多少个 'shadow' 会被用到。这时，可以使用参数变量 `…` 声明（写在参数的最后方）告诉 Sass 将这些参数视为值列表处理：

      ```scss
        @mixin box-shadow($shadows...) {
          -moz-box-shadow: $shadows;
          -webkit-box-shadow: $shadows;
          box-shadow: $shadows;
        }
        .shadows {
          @include box-shadow(0px 4px 5px #666, 2px 6px 10px #999);
        }
      ```

      编译为

      ```css
        .shadowed {
          -moz-box-shadow: 0px 4px 5px #666, 2px 6px 10px #999;
          -webkit-box-shadow: 0px 4px 5px #666, 2px 6px 10px #999;
          box-shadow: 0px 4px 5px #666, 2px 6px 10px #999;
        }
      ```

      参数变量也可以用在引用混合指令的时候 `(@include)`，与平时用法一样，将一串值列表中的值逐条作为参数引用：

      ```scss
        @mixin colors($text, $background, $border) {
          color: $text;
          background-color: $background;
          border-color: $border;
        }
        $values: #ff0000, #00ff00, #0000ff;
        .primary {
          @include colors($values...);
        }
      ```

      编译为

      ```css
        .primary {
          color: #ff0000;
          background-color: #00ff00;
          border-color: #0000ff;
        }
      ```

  - **7.4. 向混合样式中导入内容 (Passing Content Blocks to a Mixin)**

    在引用混合样式的时候，可以先将一段代码导入到混合指令中，然后再输出混合样式，额外导入的部分将出现在 @content 标志的地方：

    ```scss
      @mixin apply-to-ie6-only {
          * html {
            @content;
          }
        }
        @include apply-to-ie6-only {
          #logo {
            background-image: url(/logo.gif);
          }
        }
    ```

    编译为

    ```css
      * html #logo {
        background-image: url(/logo.gif);
      }
    ```

    > <b style="color:red;">注意：</b> 当 `@content` 在指令中出现过多次或者出现在循环中时，额外的代码将被导入到每一个地方。

    - **7.4.1 可变范围和内容块**

      传递给mixin的内容块在定义块的范围内进行计算，而不是在mixin的范围内。这意味着mixin的本地变量不能在传递的样式块中使用，变量将解析为全局值：

      ```scss
        $color: white;
        @mixin colors($color: blue) {
          background-color: $color;
          @content;
          border-color: $color;
        }
        .colors {
          @include colors { color: $color; }
        }
      ```

      编译为

      ```css
        .colors {
          background-color: blue;
          color: white;
          border-color: blue;
        }
      ```

### 8. 函数指令 (Function Directives)

  Sass 支持自定义函数，并能在任何属性值或 SassScript 中使用：

  ```scss
    $grid-width: 40px;
    $gutter-width: 10px;

    @function grid-width($n) {
      @return $n * $grid-width + ($n - 1) * $gutter-width;
    }

    #sidebar { width: grid-width(5); }
  ```

  编译为

  ```css
    #sidebar {
      width: 240px; }
  ```

  与 mixin 相同，也可以传递若干个全局变量给函数作为参数。一个函数可以含有多条语句，需要调用 `@return` 输出结果。

  自定义的函数也可以使用关键词参数，上面的例子还可以这样写：

  ```scss
    #sidebar { width: grid-width($n: 5); }
  ```

  > 建议在自定义函数前添加前缀避免命名冲突，其他人阅读代码时也会知道这不是 Sass 或者 CSS 的自带功能。

### 9. 输出格式 (Output Style)

  Sass 提供了四种输出格式，可以通过 `:style option` 选项设定，或者在命令行中使用 `--style` 选项。

  - **9.1. `:nested`**

    Nested （嵌套）样式是 Sass 默认的输出格式，能够清晰反映 CSS 与 HTML 的结构关系。选择器与属性等单独占用一行，缩进量与 Sass 文件中一致，每行的缩进量反映了其在嵌套规则内的层数。当阅读大型 CSS 文件时，这种样式可以很容易地分析文件的主要结构。

    ```css
      #main {
        color: #fff;
        background-color: #000; }
        #main p {
          width: 10em; }

      .huge {
        font-size: 10em;
        font-weight: bold;
        text-decoration: underline; }
    ```

  - **9.2. `:expanded`**

    Expanded 输出更像是手写的样式，选择器、属性等各占用一行，属性根据选择器缩进，而选择器不做任何缩进。

    ```css
      #main {
        color: #fff;
        background-color: #000;
      }
      #main p {
        width: 10em;
      }

      .huge {
        font-size: 10em;
        font-weight: bold;
        text-decoration: underline;
      }
    ```

  - **9.3. `:compact`**

    Compact 输出方式比起上面两种占用的空间更少，每条 CSS 规则只占一行，包含其下的所有属性。嵌套过的选择器在输出时没有空行，不嵌套的选择器会输出空白行作为分隔符。

    ```css
      #main { color: #fff; background-color: #000; }
      #main p { width: 10em; }

      .huge { font-size: 10em; font-weight: bold; text-decoration: underline; }
    ```

  - **9.4. `:compressed`**

    Compressed 输出方式删除所有无意义的空格、空白行、以及注释，力求将文件体积压缩到最小，同时也会做出其他调整，比如会自动替换占用空间最小的颜色表达方式。

    ```css
      #main{color:#fff;background-color:#000}#main p{width:10em}.huge{font-size:10em;font-weight:bold;text-decoration:underline}
    ```

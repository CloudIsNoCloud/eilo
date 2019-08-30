# CSS 开发技巧笔记

[原文点这里](https://juejin.im/post/5d4d0ec651882549594e7293#heading-18)，来自掘金[@
JowayYoung](https://juejin.im/user/584ec3a661ff4b006cd6383e)

## 布局部分

使用 `vw` 定制 `rem` 自适应移动端布局， `rem` 的单位长度是根据 `html` 节点的 `font-size` 而来的，再配合 `calc()` 的计算，实现自适应

```CSS
html{
  /* 7.5 应根据 UI 图进行调节，此处基于 width=750px DPR=2 */
  font-size: calc(100vm / 7.5);
}
```

`writing-mode` 属性用来调整文字排版方向，其属性如下

- `horizontal-tb`：默认排版
- `vertical-rl`：竖排，从右向左排版
- `vertical-lr`：竖排，从左向右排版

使用 `text-align-last: justify` 设置文本在容器中两端对齐，效果类似 Flex 布局中的 `justify-content: space-between`，`text-align-last` 用来设置文本在强制换行符之前的块或行的最后一行是如何对齐的，它的属性与 `text-align` 基本相同，效果也一样，只是多了一个 `auto` 属性

`:not()` 用来表示出了，需要给一个选择器类型的参数，比如 `:not(.class)`，参数可以是任何标准的选择器，使用十分灵活

`object-fit` 用来指定可替换元素（如 `<img>`）的内容应该如何适应容器，其属性如下

- `contain`：被替换的内容将被缩放，并且保持长宽比填充元素的内容框，其长的那一边完整的显示，会存在“黑边”
- `cover`：被替换的内容在保持其宽高比的同时填充元素的整个容器，如果容器大小不足以填充，则会进行裁切
- `fill`：被替换的内容正好填充元素的内容框，内容会被拉伸导致变形
- `none`：默认尺寸
- `scale-down`：内容的尺寸与 none 或 contain 中的一个相同，取决于它们两个之间谁得到的对象尺寸会更小一些

使用 Flex 或 `inline-block` 横向排布元素，使用 `overflow-x` 进行控制滚动，当然，要点不是这个，而是，可以使用 `::-webkit-scrollbar`、`::-webkit-scrollbar-track`、`::-webkit-scrollbar-thumb` 进行滚动条美化，仅限于 `webkit` 渲染引擎

使用 `text-overflow: ellipsis` 表示对于溢出容器的文本省略，并在尾部添加 `...`，单行的实现自然简单，多行则让人头疼，但是有补救的方法

```CSS
/* webkit */
.class {
  display: -webkit-box;
  overflow: hidden;
  text-overflow: ellipsis;
  -webkit-line-clamp: 3;
  /* autoprefixer: off */
  -webkit-box-orient: vertical;
   /* autoprefixer: on */
}

/* 非 webkit */
/* 这个不管几行文本都会加 ...，但是可以借助 JS 动态添加 class 来实现稍好一些的效果 */
.class{
  overflow: hidden;
  position: relative;
  max-height: 90px;

  &::after {
    position: absolute;
    right: 0;
    bottom: 0;
    padding-left: 40px;
    background: linear-gradient(to right, transparent, #fff 50%);
    content: "...";
  }
}
```

论如何画出细腻的 `1px` 边框，借助 `::before` 或者 `::after` 配合以 `transform: scale()`，其实就是先做大号，再缩小一倍

```JavaScript
&::after {
  position: absolute;
  left: 0;
  top: 0;
  border: 1px solid $red;
  width: 200%;
  height: 200%;
  content: "";
  transform: scale(.5);
  transform-origin: left top;
}
```

使用 `transform: scale3d()` 通过控制不同的参数达成水平翻转（`transform: scale3d(1, -1, 1)`）、垂直翻转（`transform: scale3d(-1, 1, 1)`）、倒序翻转（`transform: scale3d(-1, -1, 1)`）

使用 `letter-spacing` 设置负值，可以实现文本倒序，但是这个负值，至少是 `font-size` 的两倍

使用 Flex 横向布局时，配合 `margin-left: auto`，让最后一个元素向右对齐，竖向布局类似

## 行为部分

## 色彩部分

## 图形部分

## 组件部分

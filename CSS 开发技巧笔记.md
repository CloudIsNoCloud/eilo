# CSS 开发技巧笔记

[原文点这里](https://juejin.im/post/5d4d0ec651882549594e7293#heading-18)，来自掘金[@
JowayYoung](https://juejin.im/user/584ec3a661ff4b006cd6383e)

此处的内容基本和原文一样，仅仅是加上了一些额外的内容，所以请去看原文吧

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

使用 Flex 或 `inline-block` 横向排布元素，使用 `overflow-x` 进行控制滚动，当然，要点不是这个，而是，可以使用 `::-webkit-scrollbar`、`::-webkit-scrollbar-track`、`::-webkit-scrollbar-thumb` 进行滚动条美化

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

使用 `-webkit-overflow-scrolling: touch` 优化页面滚动的流畅度

使用 `transform: translateZ(0)` 开启特定元素使用硬件加速

使用 `attr()` 抓取标签中的 `data-*` 属性，之后将其赋值到 `content`，如 `content: attr(data-*)`，当然，`attr()` 支持其他任意标签属性

给 `<input>` 标签加上 `:valid`（验证通过）和 `:invalid`（验证未通过）配合 `pattern` 实现表单验证效果

使用 `pointer-events:none` 禁用事件触发(默认事件、冒泡事件、鼠标事件、键盘事件等)，相当于 `<button>` 的 `disabled`

使用 `+` 或 `~` 配合 `label` 的 `for`，美化 `radio` 或 `checkbox` 的选择行为，其实就是将 `radio` 或 `checkbox` 进行隐藏处理，而使用 `label` 的 `for`，点了 `label` 就是点了 `radio` 或 `checkbox` 的效果，再利用 `radio` 或 `checkbox` 的 `:checked` 伪类选择器，配合上 `+` 或者 `~` 选择到要改变样式的元素，利用 `radio` 的 `:checked` 配合上 `+` 或 `~` 能实现点击后改变某一样式的效果，而不使用 Javascript

使用 `:focus-within` 捕获子元素表单控件触发 `focus` 和 `blur` 事件后往夫元素的冒泡来设置样式，可玩性极高，参考原文中的这个[案例](https://codepen.io/JowayYoung/pen/BaBjaBP)，使用 `:placeholder-shown` 在 `<input>` 设置的 `placeholder` 后，`placeholder` 还在显示时的样式，借助 `:not()` 再配合以 `+` 或 `~` 可以用来做 `<input>` 旁的内容根据 `<input>` 是否有输入来显示的效果，比使用 JavaScript 要轻松不知道多少

使用无数平铺的小单元格作为背景，配合 `:hover` 来实现鼠标轨迹效果

使用 `max-height` 定位收起的最小高度和展开的最大高度，配合 `:hover`，能实现隐藏子项的导航栏，和折叠的悬浮面板等效果，只是看起来的效果似乎离完美还差点意思，鼠标离开会存在收起延迟的情况

使用 `background-attachment: fixed` 或 `transform: translateZ()` 让多层背景以不同的速度移动，形成视觉差，使其有立体的运动效果，`translateZ()` 的参数值越小，移动速度越慢，可以是负数

使用 `transform-delay` 或 `animation-delay` 设置负值延时保留动画起始帧，让动画进入页面不用等待即可运行，用来做开场动画可还行，比如加载效果

使用 `resize` 设置自由拉伸来调整目标元素的宽度，其属性如下

- `none`：不使用 `resize`
- `both`：横竖均可调整
- `horizontal`：横向可调整
- `vertical`：竖向可调整

## 色彩部分

使用 `color` 可使 `border` 未设置 `border-color` 时，颜色与 `color` 所设置的相同

使用 `filter: grayscale()` 设置灰度来实现悼念效果或某些产品的售罄，`filter` 也就是容器滤镜，其属性值如下

- `url()`：接受一个 XML 文件，该文件设置了 一个 SVG 滤镜，且可以包含一个锚点来指定一个具体的滤镜元素 `<filter>`
- `blur()`：设置高斯模糊，如果没有设定值，则默认是 0，这个参数可设置 css 长度值，但不接受百分比值，值越大越模糊
- `brightness()`：设置亮度，如果值是 0%，图像会全黑，值是 100%，则图像无变化，超过 100% 图像会比原来更亮，如果没有设定值，默认是 1
- `contrast()`：设置对比度，值是 0% 的话，图像会全黑，值是 100%，图像不变，超过 100% 会运用更低的对比，若没有设置值，默认是 1
- `drop-shadow()`：设置阴影效果，阴影是合成在图像下面，可以有模糊度，可以以特定颜色画出的遮罩图的偏移版本，该函数与 `box-shadow` 属性很相似，不同之处在于通过 `filter`，一些浏览器为了更好的性能会提供硬件加速，以及不能用 `inset`
- `grayscale()`：设置灰度，值为 100% 则完全转为灰度图像，值为 0% 图像无变化，若未设置，值默认是 0，取值一般在 0% 到 100% 之间
- `hue-rotate()`：设置色相旋转，值为 0deg，则图像无变化，若值未设置，默认值是 0deg，该值虽然没有最大值，超过 360deg 的值相当于又从 0deg 开始，以此循环
- `invert()`：设置负片效果，值为 100% 为完全反转,值为 0% 则图像无变化，若值未设置，值默认是 0，取值一般在 0% 到 100% 之间
- `opacity()`：设置透明度，值为 0% 则是完全透明，值为 100% 则图像无变化，若值未设置，值默认是 1，取值一般在 0% 到 100% 之间，该函数与已有的 `opacity` 属性很相似，不同之处在于通过 `filter`，一些浏览器为了提升性能会提供硬件加速
- `saturate()`：设置饱和度，值为 `0%` 则是完全不饱和，值为 `100%` 则图像无变化，过 100%的值是允许的，则有更高的饱和度， 若值未设置，值默认是 1
- `sepia()`：设置深褐色滤镜，值为 100% 则完全是深褐色的，值为 0% 图像无变化，若未设置，值默认是 0，取值一般在 0% 到 100% 之间

`filter` 属性的函数，是可以任意进行组合的，所以其玩法巨多，可以实现各种图像滤镜和处理效果

使用 `::selection` 设置自定义的文本选择颜色，用来做主题化

使用巨大号的 `linear-gradient` 设置背景渐变色，并配合移动效果，能实现很好看的彩虹墙，参考原文中的这个[案例](https://codepen.io/JowayYoung/pen/oNvbRwN)

使用 `linear-gradient` 设置背景渐变色，配合 `background-clip:text` 对背景进行文本裁剪，再配合 `-webkit-text-fill-color` 设置其文字颜色为透明，实现文本渐变色，参考原文中的这个[案例](https://codepen.io/JowayYoung/pen/pozgQVo)

使用 `caret-color` 设置光标颜色，用来做主题化

## 图形部分

使用 `mask` 为图像背景生成蒙层提供遮罩效果，可以拿来高斯模糊蒙层、票劵(电影票、购物卡)和遮罩动画，但是应该用的不多，参考原文中的这个[案例](https://codepen.io/JowayYoung/pen/xxKZdZN)

使用 `linear-gradient` 绘制波浪线，参考原文中的这个[案例](https://codepen.io/JowayYoung/pen/EqEzwq)，应该说，这个属性不只能绘制波浪线，还能绘制很多其他效果，比如说间断颜色的彩带，参考原文中的这个[案例](https://codepen.io/JowayYoung/pen/bGbeXZG)，比如说方格背景，参考原文中的这个[案例](https://codepen.io/JowayYoung/pen/RwboXoV)

使用 `conic-gradient` 绘制饼图

使用 `box-shadow` 绘制单侧投影，这里利用的是定位取负值，以及 `box-shadow` 的取负值，当然，`box-shadow` 的可玩性非常非常高，可以同时设置很多次的，并且都会生效，这就是新世界的大门，这么说起来，`background`

使用 `filter` 配合 `:after` 或 `before`，再配合 `background: inherit`，实现描绘头像彩色阴影，再加以大小形状位置的调整，参考原文中的这个[案例](https://codepen.io/JowayYoung/pen/GRKjYap)

使用 `box-shadow` 模拟蒙层的中间镂空，其实就是设置一个值巨大的 `box-shadow`，由此，其实可以利用 `box-shadow` 实现模态框的背景，或者图片裁剪以及新手引导

使用 `outline` 描绘内边框，利用 `outline-offset` 属性设置负值，再配合以适当的 `padding`，岂不美哉

## 组件部分

使用 `counter-increment: index 1`（index 可以理解为计数器名字，1 表示权重） 配合 `counter(index)`，直接使用 CSS 实现计数器效果，再利用 `data-*` 配合 `attr()` 设置单位

使用 `+` 选择器，配合 `:hover`，能做出下划线跟随鼠标的导航栏，参考原文中的这个[案例](https://codepen.io/JowayYoung/pen/eYOJbNv)

使用 `mix-blend-mode` 设置元素的内容如何与元素父元素及其背景的混合模式，实现拾色器改变图像色相的换色器，其参数过多就不一一列举，可以去 MDN 查看其[详情](https://developer.mozilla.org/en-US/docs/Web/CSS/mix-blend-mode)

使用 `:before` 和 `:after` 配合形状，大小以及动画的设置，动画的时间要把握好，实现状态悬浮球效果，参考原文中的这个[案例](https://codepen.io/JowayYoung/pen/WNewOxa)

使用 `scroll-behavior` 当用户手动导航或者 CSSOM scrolling API 触发滚动操作时的效果，其属性值如下

- `auto`：基本上就是直接闪现
- `smooth`：平稳滚动

使用 `~` 选择器，配合 `<input type="radio" id="id">` 再配合 `<label for="id"></label>`，实现可切换内容的导航栏，而且很好看，参考原文中的这个[案例](https://codepen.io/JowayYoung/pen/oNvzoZg)，还可以配合 `<input type="checkbox" id="id">` 再配合 `<label for="id"></label>`，实现折叠面板，当然，也用到了 `max-length`，参考原文中的这个[案例](https://codepen.io/JowayYoung/pen/NWKRMjo)

使用 Flex 布局倒序五颗星星，配合 `<input type="radio">` 再配合 `:checked` 或 `:hover` 利用 `~` 选择器实现星级评分

## 总结

首先，此处列举的都是较为常用，且不复杂的内容，并非原文中的所有内容，其次，如果真的好好学 CSS，很多效果就完全没有 JavaScript 什么事情，但这就不意味着这些效果不要用 JavaScript 控制，而应该相互融合，使用最佳的解决方案，总之，还是要多思考，而 CSS 需要学习的东西也还有很多，不能说这个效果用 JavaScript 也能实现，但是，有的效果，真的就是纯 CSS 就能实现，并且实现效果，步骤，复杂度都还要更低，并且，界面好不好看，很多时候，都是 CSS 说了算

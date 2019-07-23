### CSS 常用书写顺序整理

规范的书写顺序对于后期维护作用巨大，随意整理仅留作参考，分类名称暂未想好。

对于括号内的内容基本可以理解为：若 `x(y)` 则有 `x-y` 这样的单独属性存在

---

#### 一

display,visibility,float,overflow(x,y),zoom

#### 二

table-layout,caption-side,border-spacing,border-collapse,
list-style(position,type,image)

#### 三

position,top,right,bottom,left,z-index (所有的有涉及上下左右的属性均按照上右下左的顺序)

#### 四

margin,box-sizing,border(width,style,color),
border-radius,border-image(source,slice,width,outset,repeat),
padding,width,min-width,max-width,height,min-width,max-height

#### 五

font(family,size,weight,style),line-height,text-align,
vertical-align,white-space,text-decoration,text-emphasis(color,style,position),
text-overflow,word-wrap,word-break

#### 六

color,background(color,image,repeat,attachment,position(x,y),clip,origin,size)

#### 七

opacity,filter,box-shadow,text-shadow

#### 八

transition(delay,timing-function,duration,property),
transform(origin),animation(name,duration,play-state,timing-function,delay,iteration-count,direction)

#### 九

content,quotes,resize,cursor,user-select,hyphens,pointer-events

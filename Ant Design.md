# Ant Design

[官网](https://ant.design/docs/spec/introduce-cn)

虽然并不算前端的内容，但是对于界面的布局的感觉会有很大帮助

## Ant Design 介绍

蚂蚁金服体验技术部经过大量的项目实践和总结，逐步打磨出的一个服务于企业级产品的设计体系，基于『确定』和『自然』的设计价值观，通过模块化的解决方案，降低冗余的生产成本，让设计者专注于更好的用户体验

## 设计价值观

设计价值观为 Ant Design 的设计者以及基于 Ant Design 进行产品设计的设计者，提供评价设计好坏的内在标准，并提供有效的设计实践所遵循的规则。同时，它启示并激发了设计原则和设计模式，为具体的设计问题提供向导和一般解决方案

### 自然

在行为的执行中，利用行为分析、人工智能、传感器、元数据等一系列方式，辅助用户有效决策、减少用户额外操作，从而节省用户脑力和体力，让人机交互行为更自然

在感知和认知中，视觉系统扮演着最重要的角色，通过提炼自然界中的客观规律并运用到界面设计中，从而创建更有层次产品体验；同时，适时加入听觉系统、触觉系统等，创建更多维、更真实的产品体验。详见视觉语言

### 确定

保持克制： 能做，但想清楚了不做。设计者应当聚焦在最有价值产品功能打磨，并用尽可能少的设计元素将其表达。正如 Antoine de St.Exupery 所说：完美不在于无以复加，而在于无可删减，万事莫不如此

面向对象的方法： 探索设计规律，并将其抽象成『对象』，增强界面设计的灵活性和可维护性，同时也减少『设计者』的主观干扰，从而降低系统的不确定性。例如：色值换算、间距排版

模块化设计： 将复杂或者重复出现的局部封装成模块，提供有限接口与其他模块互动，最终全面减少系统的复杂度，进而增进可靠性以及可维护性。设计者可运用现有的组件/模板或者自行抽象可复用的组件/模板，节约无谓的设计且保持系统一致性，让『设计者』把创造力专注在最需要的地方

## 设计原则

### 亲密性

如果信息之间关联性越高，它们之间的距离就应该越接近，也越像一个视觉单元；反之，则它们的距离就应该越远，也越像多个视觉单元。亲密性的根本目的是实现组织性，让用户对页面结构和信息层次一目了然

#### 纵向间距关系

通过『小号间距』（8px）、『中号间距』（16px）、『大号间距』（24px）这三种规格来划分信息层次

通过增加『分割线』来拉开层次

在这三种规格不适用的情况下，可以通过加减『基础间距』的倍数（`y = 8 + 8 * n`，`n >= 0`，y 是纵向间距，8 是『基础间距』），或者增加元素来拉开信息层次

#### 横向间距关系

为了适用不同尺寸的屏幕，在横向采用栅格布局来排布组件，从而保证布局的灵活性，并且在一个组件内部，元素的横向间距也应该有所不同

### 对齐

正如『格式塔学派』中的连续律（Law of Continuity）所描述的，在知觉过程中人们往往倾向于使知觉对象的直线继续成为直线，使曲线继续成为曲线。在界面设计中，将元素进行对齐，既符合用户的认知特性，也能引导视觉流向，让用户更流畅地接收信息

> 格式塔学派（德语：Gestalttheorie） ：是心理学重要流派之一，兴起于 20 世纪初的德国，又称为完形心理学；主张人脑的运作原理是整体的，『整体不同于其部件的总和』

#### 文案类对齐

如果页面的字段或段落较短、较散时，需要确定一个统一的视觉起点

#### 表单类对齐

冒号对齐（右对齐）能让内容锁定在一定范围内，让用户眼球顺着冒号的视觉流，就能找到所有填写项，从而提高填写效率

#### 数字类对齐

为了快速对比数值大小，建议所有数值取相同有效位数，并且右对齐

### 对比

对比是增加视觉效果最有效方法之一，同时也能在不同元素之间建立一种有组织的层次结构，让用户快速识别关键信息，要实现有效的对比，对比就必须强烈，切不可畏畏缩缩

#### 主次关系对比

为了让用户能在操作上（类似表单、弹出框等场景）快速做出判断， 来突出其中一项相对更重要或者更高频的操作，突出的方法，不局限于强化重点项，也可以是弱化其他项

在一些需要用户慎重决策的场景中，系统应该保持中立，不能替用户或者诱导用户做出判断

#### 总分关系对比

通过调整排版、字体、大小等方式来突出层次感，区分总分关系，使得页面更具张力和节奏感

#### 状态关系对比

通过改变颜色、增加辅助形状等方法来实现状态关系的对比，以便用户更好的区分信息，常见类型有『静态对比』、『动态对比』

### 重复

相同的元素在整个界面中不断重复，不仅可以有效降低用户的学习成本，也可以帮助用户识别出这些元素之间的关联性

#### 重复元素

重复元素可以是一条粗线、一种线框，某种相同的颜色、设计要素、设计风格，某种格式、空间关系等

### 直截了当

正如 Alan Cooper 所言：『需要在哪里输出，就要允许在哪里输入』，这就是直接操作的原理，eg：不要为了编辑内容而打开另一个页面，应该直接在上下文中实现编辑

#### 页内编辑

当『易读性』远比『易编辑性』重要时，可以使用『单击编辑』，大致的三个状态

- 状态一：普通的浏览模式，不区分可编辑行和不可编辑行
- 状态二：鼠标悬停时，『指针』变为『手型』，编辑区域底色变黄，出现『Tooltips』提示单击编辑
- 状态三：鼠标点击后，出现『输入框』、『确定』、『取消』表单元素，同时光标定位在『输入框』中

当『易读性』为主，同时又要突出操作行的『易编辑性』时，可使用『文字链/图标编辑』，大致的两个状态

- 状态一：在可编辑行附近出现文字链/图标
- 状态二：鼠标点击『编辑』后，出现『输入框』、『确定』、『取消』表单元素，同时光标定位在『输入框』中

多字段行内编辑，在不破坏整体性的前提下，可扩大空间，以便放下『输入框』等表单元素，其中，在 Table 中进行编辑模式切换时，需要保证每列的不跳动

在『多字段行内编辑』的情况下，显示的内容和编辑时所需的字段会存在比较大的差异，所以更需要『巧用过渡』原则中的『解释刚刚发生了什么』来消除这种视觉影响

#### 利用拖放

拖放列表，只能限制在一个维度（上/下或者左/右）进行拖放，大致的三个状态

- 状态一：鼠标悬停该行时，出现可移动的『图标』
- 状态二：鼠标悬停在该『图标』时，指针变为『手型』，点击即可进行拖动
- 状态三：拖动到可放置区块，出现蓝色描边，告知用户该区块可放置该对象

拖放图片/文件

### 足不出户

能在这个页面解决的问题，就不要去其它页面解决，因为任何页面刷新和跳转都会引起变化盲视（Change Blindness），导致用户心流（Flow）被打断，频繁的页面刷新和跳转，就像在看戏时，演员说完一行台词就安排一次谢幕一样

> 变化盲视（Change Blindness） ：指视觉场景中的某些变化并未被观察者注意到的心理现象。产生这种现象的原因包括场景中的障碍物，眼球运动、地点的变化，或者是缺乏注意力等。——摘自《维基百科》
> 心流（Flow） ：也有别名以化境 (Zone) 表示，亦有人翻译为神驰状态，定义是一种将个人精神力完全投注在某种活动上的感觉；心流产生时同时会有高度的兴奋及充实感。——摘自《维基百科》

#### 覆盖层

二次确认覆盖层：避免滥用 Modal 进行二次确认，应该勇敢的让用户去尝试，给用户机会『撤销』即可

- 用户点击『删除』后，直接操作；出现 Message 告知用户操作成功，并提供用户『撤销』的按钮；用户进行下一个操作或者 1 分钟内不进行任何操作， Message 消失，用户无法再『撤销』
- 在执行某些无法『撤销』的操作时，可以点击『删除』后，出现 Popconfirm 进行二次确认，在当前页面完成任务

一个不推荐示例

- 滥用 Modal 进行二次确认，就像『狼来了』一样，既打断用户心流（无法将上下文带到弹出框中），也无法避免失误的发生

详情覆盖层：一般在列表中，通过用户『悬停』/『点击』某个区块，在当前页加载该条列表项的更多详情信息

- 使用『悬停』激活时，当鼠标移入时，需要设置 0.5 秒左右的延迟触发，当鼠标移出时，立刻关闭覆盖层

输入覆盖层：在覆盖层上，让用户直接进行少量字段的输入

- 鼠标『点击』图标触发，鼠标『点击』悬浮层以外的其他区块后，直接保存输入结果并退出

#### 嵌入层

列表嵌入层：在列表中，显示某条列表项的详情信息，保持上下文不中断

标签页：将多个平级的信息进行整理和分类了，一次只显示一组信息

#### 虚拟页面

在交互过程中，『覆盖层』可以在当前页面上方显示附加内容和交互链接，『嵌入层』可以在页面内部实现同样效果；而『虚拟页面』不局限机械时代的『页面』，可以利用信息时代的特点构建一种新型『页面』

#### 流程处理

长期以来，Web 实现流程的方式就是把每个步骤放在一个单独的页面上，虽然这种做法是分解问题最简单的方式，但并不是最佳解决方案，对于某些『流程处理』而言，让用户始终待在同一个页面上则更有必要

渐进式展现：基于用户的操作/某种特定规则，渐进式展现不同的操作选项

配置程序：通过提供一系列的配置项，帮助用户完成任务或者产品组装

弹出框覆盖层：虽然弹出框的出现会打断用户的心流，但是有时候在弹出框中使用『步骤条』来管理复杂流程也是可行的

### 简化交互

根据费茨法则（Fitts's Law）所描述的，如果用户鼠标移动距离越少、对象相对目标越大，那么用户越容易操作，通过运用上下文工具（即：放在内容中的操作工具），使内容和操作融合，从而简化交互

> 费茨法则 ：到达目标的时间是到达目标的距离与目标大小的函数，具体：![公式](https://os.alipayobjects.com/rmsportal/wAcbQmeqTWDqsnu.png)，其中：1.设备当前位置和目标位置的距离（D）；2.目标的大小（W），距离越长，所用时间越长；目标越大，所用时间越短

#### 实时可见工具

如果某个操作非常重要，就应该把它放在界面中，并实时可见，大致的三个状态

- 状态一：在文案中出现一个相对明显的点击区域
- 状态二：鼠标悬停时，鼠标『指针』变为『手型』，底色发生变化，邀请用户点击
- 状态三：鼠标点击后，和未点击前有明显的区分

#### 悬停即现工具

如果某个操作不那么重要，或者使用『实时可见工具』过于啰嗦会影响用户阅读时，可以在悬停在该对象上时展示操作项

#### 开关显示工具

如果某些操作只需要在特定模式时显示，可以通过开关来实现

- 用户点击『修改』后，Table 中『文本』变成『输入框』，开启编辑功能

#### 可视区域 ≠ 可点击区域

在使用 Table 时，文字链的点击范围受到文字长短影响，可以设置整个单元格为热区，以便用户触发

- 当悬浮在 ID 所在的文字链单元格时，鼠标『指针』随即变为『手型』，单击即可跳转

当需要增强按钮的响应性时，可以通过增加用户点击热区的范围，而不是增大按钮形状，从而增强响应性，又不缺失美感，在移动端尤其适用

- 鼠标移入按钮附近，即可激活 Hover 状态

### 提供邀请

很多富交互模式（eg：『拖放』、『行内编辑』、『上下文工具』）都有一个共同问题，就是缺少易发现性，所以『提供邀请』是成功完成人机交互的关键所在

邀请就是引导用户进入下一个交互层次的提醒和暗示，通常包括意符（eg：实时的提示信息）和可供性，以表明在下一个界面可以做什么，当可供性中可感知的部分（Perceived Affordance）表现为意符时，人机交互的过程往往更加自然、顺畅

> 意符（Signifiers） ：一种额外的提示，告诉用户可以采取什么行为，以及应该怎么操作；必须是可感知（eg：视觉、听觉、触觉等）。——摘自《设计心理学 1 》
> 可供性（Affordance） ：也被翻译成『示能』，由 James J. Gibson 提出，定义为物品的特性与决定物品用途的主体能力之间的关系；其中部分可感知（此部分定义为 Perceived Affordance），部分不可感知。——摘自《设计心理学 1 》

#### 静态邀请

指通过可视化技术在页面上提供引导交互的邀请

引导操作邀请：一般以静态说明形式出现在页面上，不过它们在视觉上也可以表现出多种不同样式，常见类型：『文本邀请』、『白板式邀请』、『未完成邀请』

漫游探索邀请：是向用户介绍新功能的好方法，尤其是对于那些设计优良的界面，但是它不是『创口贴』，仅通过它不能解决界面交互的真正问题，应当保持漫游过程简单，让用户容易退出和重新启动，保持内容简明扼要，与功能密切相关

- 在用户首次登录时出现少量『探索点』，当用户点击『我知道了』，能快速切换到下一个探索点

#### 动态邀请

指以响应用户在特定位置执行特定操作的方式，提供特定的邀请

悬停邀请：在鼠标悬停期间提供邀请

- 鼠标『悬停』整个卡片时，可被点击部分变为蓝色的『文字链』
- 鼠标『悬停』时，出现『选择此模板』的按钮

推论邀请：用于交互期间，合理推断用户可能产生的需求

- 用户点击『赞』后，同时系统分析（既然用户喜欢这篇文章，那么可能对这一类文章都有兴趣）并提供开启『精打细算』的邀请

更多内容邀请：用于邀请用户查看更多内容

- 在 Modal 中会出现前后切换的箭头

### 巧用过渡

人脑灰质（Gray Matter）会对动态的事物（eg：移动、形变、色变等）保持敏感，在界面中，适当的加入一些过渡效果，能让界面保持生动，同时也能增强用户和界面的沟通

- Adding: 新加入的信息元素应被告知如何使用，从页面转变的信息元素需被重新识别。

- Receding: 与当前页无关的信息元素应采用适当方式移除。

- Normal: 指那些从转场开始到结束都没有发生变化的信息元素

#### 在视图变化时保持上下文

滑入与滑出：可以有效构建虚拟空间

传送带：可极大地扩展虚拟空间

折叠窗口：在视图切换时，有助于保持上下文，同时也能拓展虚拟空间

#### 解释刚刚发生了什么

对象增加：在列表/表格中，新增了一个对象

- 新增一条对象时，该行『高亮』告知用户这是新增项；几秒后『高亮』消失，以免过度干扰用户

对象删除：在列表/表格中，删除了一个对象

对象更改：在列表/表格中，更改了一个对象，大致的三个状态

- 状态一：用户更改了『详情』中的值
- 状态二：用户点击『保存』后，详情所在的网格出现『黄底』，表明该对象发生了更改
- 状态三：底色持续几秒后，恢复正常

对象呼出：点击页面中元素，呼出一个新对象

#### 改善感知性能

当无法有效提升『实际性能』时，可以考虑适当转移用户的注意力，来缩短某项操作的感知时间，改善感知性能

#### 自然运动

[Ant Motion 动画语言](http://motion.ant.design/language/basic-cn)

要做到自然，自然是很难的

### 即时反应

『提供邀请』的强大体现在交互之前给出反馈，解决易发现性问题，『巧用过渡』的有用体现在它能够在交互期间为用户提供视觉反馈，『即时反应』的重要性体现在交互之后立即给出反馈

就像『牛顿第三定律』所描述作用力和反作用一样，用户进行了操作或者内部数据发生了变化，系统就应该立即有一个对应的反馈，同时输入量级越大、重要性越高，那么反馈量级越大、重要性越高

虽然反馈太多（准确的说，错误的反馈太多）是一个问题，但是反馈太少甚至没有反馈的系统，则让人感觉迟钝和笨拙，用户体验更差

> 牛顿第三定律 ：当两个物体互相作用时，彼此施加于对方的力，其大小相等、方向相反。——摘自《维基百科》

#### 查询模式

自动完成：用户输入时，下拉列表会随着输入的关键词显示匹配项。根据查询结果分类的多少，可以分为『确定类目』、『不确定类目』两种类型

- 用户所查询的关键词，只会在『话题』、『问题』、『文章』这 3 种类目中出现
- 用户所查询的关键词，其所属的类目数量不确定，可能 4 个，可能 5 个，可能更多

实时搜索：随着用户输入，实时显示搜索结果。『自动完成』、『实时建议』的近亲

- 用户输入一个搜索值，系统随即显示查询结果

#### 反馈模式

实时预览：在用户提交输入之前，让他先行了解系统将如何处理他的输入

- 根据用户的输入，提供关于密码强度和有效性的实时反馈

解决错误最好的办法，就是不让错误发生，而『实时预览』就是有效避免错误的好设计

渐进式展现：在必要的时候提供必要的提示，而不是一股脑儿显示所有提示，导致界面混乱，增加认知负担

进度指示：当一个操作需要一定时间完成时，就需要即时告知进度，保持与用户的沟通。常见的进度指示：『按钮加载』、『表格加载』、『富列表加载』、『页面加载』，可根据操作的量级和重要性，展示不同类型的进度指示

点击刷新：告知用户有新内容，并提供按钮等工具帮助用户查看新内容

定时刷新：无需用户介入，定时展示新内容

- 新增的列表项『高亮』，持续几秒后恢复正常

## 视觉

### 色彩

Ant Design 将色彩体系解读成两个层面：系统级色彩体系和产品级色彩体系

系统级色彩体系主要定义了蚂蚁中台设计中的基础色板、中性色板和数据可视化色板，产品级色彩体系则是在具体设计过程中，基于系统色彩进一步定义符合产品调性以及功能诉求的颜色

[色板看这里](https://ant.design/docs/spec/colors-cn#%E5%9F%BA%E7%A1%80%E8%89%B2%E6%9D%BF)

其余的看色板中的介绍即可

### 布局

空间布局是体系化视觉设计的起点，和传统的平面设计的不同之处在于，UI 界面的布局空间要基于『动态、体系化』的角度出发展开，我们受到建筑界大师柯布西耶的模度思想的启发，基于『秩序之美』的原则，探索 UI 设计中的动态空间秩序，形成了 Ant Design 的界面布局方式，为设计者构筑具备理性之美的布局空间创造了条件

在中后台视觉体系中定义布局系统，我们建议从 5 个方面出发：

1. 统一的画板尺寸
2. 适配方案
3. 网格单位
4. 栅格
5. 常用模度

#### 统一画板

为了尽可能减少沟通与理解的成本，有必要在组织内部统一设计板的尺寸，蚂蚁中台设计团队统一的画板尺寸为 1440

#### 适配

在设计过程中，设计师还需要建立适配的概念，根据具体情况判断系统是否需要进行适配，以及哪些区块需要考虑动态布局，据统计，使用中台系统的用户的主流分辨率主要为 1920、1440 和 1366，个别系统还存在 1280 的显示设备

两种较为典型的适配方案

- 左右布局的适配方案：常被用于左右布局的设计方案中，常见的做法是将左边的导航栏固定，对右边的工作区域进行动态缩放

- 上下布局的适配方案：常被用于上下布局的设计方案中，做法是对两边留白区域进行最小值的定义，当留白区域到达限定值之后再对中间的主内容区域进行动态缩放

#### 网格单位

Ant Design 通过网格体系来实现视觉体系的秩序，网格的基数为 8，不仅符合偶数的思路同时能够匹配多数主流的显示设备，通过建立网格的思考方式，还能帮助设计者快速实现布局空间的设计决策同时也能简化设计到开发的沟通损耗

#### 栅格

Ant Design 采用 24 栅格体系，对开发者而言栅格是实现动态布局的手段，而设计师对于栅格的理解源自平面设计中的栅格，在具体落地中视角的不同就容易造成偏差，最终影响还原度，继而增加沟通成本

Ant Design 的设计师通过 4 点来实现设计过程中和工程师的沟通：

1. 清晰的定义动态布局范围
2. 尽量保持偶数思维
3. 关键数据的交付（Gutter、Column）
4. 区块的定义要从 column 开始到 column 结束

#### 常用模度

为了帮助不同设计能力的设计者们在界面布局上的一致性和韵律感，统一设计到开发的布局语言，减少还原损耗，Ant Design 提出了 UI 模度的概念，他们保持了 8 倍数的原则、具备动态的韵律感，可以在一定程度上帮助我们更快更好的实现布局空间上的设计决策

#### 是启发，而非限制

Ant Design 在布局空间上的成果并非要限制设计产出，更多的在于引导设计者如何做到『更好』，8 倍数的双数组通过排列组合的方式可以形成千变万化种可能性，但在无限的可能性之中依然存在着『只是简单的套用数据组合』同『看起来很精妙』的差别，实现合理优雅的界面布局，在对美感的追求之上，还应当结合可用性来看待，对于企业级应用界面布局的探索，我们依然在路上

### 字体

字体是体系化界面设计中最基本的构成之一

用户通过文本来理解内容和完成工作，科学的字体系统将大大提升用户的阅读体验及工作效率，。Ant Design 字体方案，是基于『动态秩序』的设计原则，结合了自然对数以及音律的规则得出的

建议从下面五个方面出发：

1. 字体家族
2. 主字体
3. 字阶与行高
4. 字重
5. 字体颜色

#### 字体家族

优秀的字体系统首先是要选择合适的字体家族，Ant Design 的字体家族中优先使用系统默认的界面字体，同时提供了一套利于屏显的备用字体库，来维护在不同平台以及浏览器的显示下，字体始终保持良好的易读性和可读性，体现了友好、稳定和专业的特性

另外，在中后台系统中，数字经常需要进行纵向对比展示，我们单独将数字的字体 `font-variant-numeric` 设置为 `tabular-nums`，使其为等宽字体

#### 主字体

基于电脑显示器阅读距离（50 cm）以及最佳阅读角度（0.3）对 Ant Design 的主字体进行了一次升级，从原先的 12 上升至 14，以保证在多数常用显示器上的用户阅读效率最佳

#### 字阶与行高

字阶和行高决定着一套字体系统的动态与秩序之美，字阶是指一系列有规律的不同尺寸的字体，行高可以理解为一个包裹在字体外面的无形的盒子

Ant Design 受到 5 音阶以及自然律的启发定义了 10 个不同尺寸的字体以及与之相对应的行高

![字阶与行高](https://gw.alipayobjects.com/zos/rmsportal/iFjgfIBExksqCqGMwUlw.png)

在 Ant Design 的视觉体系中，建议的主要字体为 14，与之对应的行高为 22，其余的字阶的选择可根据具体情况进行自由的定义，建议在一个系统设计中（展示型页面除外），字阶的选择尽量控制在 3-5 种之间，保持克制的原则

#### 字重

字重的选择同样基于秩序、稳定、克制的原则，多数情况下，只出现 regular 以及 medium 的两种字体重量，分别对应代码中的 400 和 500，在英文字体加粗的情况下会采用 semibold 的字体重量，对应代码中的 600

#### 字体颜色

文本颜色如果和背景颜色太接近就会难以阅读，考虑到无障碍设计的需求，我们参考了 WCAG 的标准，将正文文本、标题和背景色之间保持在了 7:1 以上的 AAA 级对比度

![字体颜色](https://gw.alipayobjects.com/zos/rmsportal/jPbEabWakVQHosHxhQPR.png)

#### 建议

字体系统的构建，是『动态秩序之美』的第一步，在实际的设计中，还有三点建议：

1. 建立体系化的设计思路：在同一个系统的 UI 设计中先建立体系化的设计思路，对主、次、辅助、标题、展示等类别的字体做统一的规划，再落地到具体场景中进行微调，建立体系化的设计思路有助于强化横向字体落地的一致性，提高字体应用的性价比，减少不必要的样式浪费
2. 少即是多：在视觉展现上能够用尽量少的样式去实现设计目的。避免毫无意义的使用大量字阶、颜色、字重强调视觉重点或对比关系
3. 尝试让字体像音符一样跳跃：在需要拉开差距的时候可以尝试在字阶表中跳跃的选择字体大小，会令字阶之间产生一种微妙的韵律感

### 图标

图标是 UI 设计中必不可少的组成，通常我们理解图标设计的含义，是将某个概念转换成清晰易读的图形，从而降低用户的理解成本，提升界面的美观度，在企业级应用设计范围中，图标在界面设计的诸多元素中往往只占了很小的比重，在调用时也会被缩到比设计稿小很多倍的尺寸，加上在图形素材极度丰富并且便于获取的今天，在产品设计体系中实现一套美观、一致、易用、便于延展的图标体系往往会被不小心忽略掉，Ant Design 相信一整套优质的图标对于设计质量的影响是非常巨大的，这考验着设计师的协作能力，以及对图形塑造的系统性思维，同时也能反映一个团队对于细节的追求

[图标库](https://ant.design/components/icon-cn/)

#### 设计原则

Ant Design 的图标设计原则源自"确定"和"自然"，落实到图标设计领域，一共有四个，他们分别为：

1. 准确： 设计造型准确的图标（保持偶数原则，去小数点）；选择表意准确的图标，不对用户的认知造成困扰
2. 简单： 在表意清晰准确的基础上，尽量保持图形的简洁，不做多余的修饰
3. 节奏： 挖掘构图中的秩序之美
4. 愉悦： 赋予适度的情感

#### 设计规格

Artboard： Ant Design 的系统图标都是按照 1024 x 1024 的画板进行制作的

![Artboard](https://gw.alipayobjects.com/zos/rmsportal/mrrFTiCWOyCsVOgAIBqg.png)

出血位： 在图标的设计过程中预留出血位的做法，可以预防某些造型的图标在具体应用时出现边缘被切掉的风险，同时在设计过程中，也为设计师把握图标间平衡留下了进退的余地，新版的设计规格在图形的外围预留了 64px 的出血位，多数的图标在设计中我们都不建议超过这个区域

![出血位](https://gw.alipayobjects.com/zos/rmsportal/FNXMpWnyvYfydiSnPCYg.png)

#### 分层

Ant Design 的图标设计对于设计稿的分层也有一定的要求，其目的除了让设计师实现有序的文档管理之外，更多的是便于团队间文档的传递，统一的设计框架像是无形的共识，可以让彼此间的理解得到进一步的提升

![分层](https://gw.alipayobjects.com/zos/rmsportal/bVtUZqDRbGuaoVbwYqua.png)

#### 轮廓线与模版

根据出血位的尺寸，调整轮廓线的宽高，同时增加两个等边三角形和一个圆，这些都是图标设计中最常用的基本形式，设计师可以快速的调用并在此基础上做变形

![轮廓线与模版](https://gw.alipayobjects.com/zos/rmsportal/ycDkLxfAqjnRsWZuHvik.png)

#### 图标设计指引

根据"确定性"和"自然"的价值观，当构图含义明确之后，图标设计所追求的便是秩序之美，Ant Design 的图标主要通过四方面去实现"秩序美"，分别是：形式、韵律、平衡以及辨识

[图标设计指引](https://ant.design/docs/spec/icon-cn#%E5%9B%BE%E6%A0%87%E8%AE%BE%E8%AE%A1%E6%8C%87%E5%BC%95)

#### 给设计师的一些建议

在完成图标设计后，保持图形的整洁，图层结构的清晰，也是构筑图标体系必不可少的部分，Ant Design 对设计师有几点建议如下：

- 干掉多余的节点，保持图形的整洁
- 合并图形，便于输出
- 对小数点以及奇数进行最后一遍的走查与修正
- 整洁的图层管理

#### 图标的设计总结

图标的设计是 UI 设计中非常容易被忽略的环节，建立优秀的图形体系也不是一、二个设计人员的事，需要整个团队在设计前、设计中以及设计后都能够达成共识并且通力合作去完成共建
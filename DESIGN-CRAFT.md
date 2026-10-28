# 界面设计技巧

适用于产品界面、数据工具和展示页面的设计与评审。优先建立清楚的内容层级、稳定的阅读节奏和明确的操作反馈，再用字体、色彩、材质与动效形成个性。审美判断首先落实在取舍上：什么值得强调，什么可以安静，什么应该省略。

1. **Avoid unnecessary secondary labels and descriptions. Let the layout do the explaining.**

   避免不必要的次级标签和说明，让布局承担解释。用位置说明归属，用对齐建立联系，用间距区分分组，用大小和对比表达优先级。标题已经叫“成员”，下面的人名、头像与邀请按钮就足以说明用途。

   每段文字都应增加识别、判断或行动所需的信息。字段名称、计量单位、比较周期、操作后果值得保留；重复标题、复述按钮、描述显而易见布局的文字可以省略。删除一段说明后，应重新调整间距，让内容自然收拢。

2. **让留白和动效承担表现力。**

   留白控制注意力的分布，动效说明注意力如何转移。给主标题、关键数据和主要操作足够的独立空间；通过展开、位移、淡入和状态过渡，让用户感知内容之间的关系。

   静止时，页面应有清楚的主次和节奏；操作时，变化应有起点、方向和落点。品牌表现可以集中在一个舒展的首屏、一张有分量的图片或一次连贯的展开中，其余区域保持平静。

3. **为每个任务区域确定一个视觉重心。**

   先确定用户进入这个区域最应该看到什么，再决定字号、面积、颜色和位置。编辑界面的重心可以是内容，分析界面的重心可以是异常数据，购买区域的重心可以是产品与购买动作。

   让其他元素围绕这个重心组织。相邻内容需要拉开权重时，先调整其中一个变量，例如缩小次要标题或扩大主内容面积。多个元素同时放大、加粗、着色，会削弱阅读顺序。

4. **按内容关系选择布局。**

   连续阅读适合文档流，同类对象适合列表，跨对象比较适合表格，可独立浏览和操作的内容适合卡片。只有当内容的优先级和展示需求确实不同，才用大小不等的网格。

   Bento 布局中的大块应容纳更重要或更需要空间的内容，小块应足够简明。先写出内容关系，再分配跨度、比例和留白。Magic UI 的网格与卡片结构提供了组合空间，具体面积应由内容决定。[^bento]

5. **用间距表达亲疏，并形成少量稳定的档位。**

   标签与字段、标题与正文、同组条目之间保持较小距离；不同任务组之间明显拉开。尤其要让说明文字更靠近它解释的对象。

   普通产品界面可以用以下尺度起稿，再根据字体、控件大小和信息密度调整。这是一组设计起点。

   | 关系 | 起稿间距 | 作用 |
   | --- | --- | --- |
   | 图标与文字、标题与紧随的说明 | 4–8 px | 建立紧密关联 |
   | 同组字段、列表条目、卡片内分区 | 12–16 px | 区分同一任务内的内容 |
   | 不同任务组、相邻内容模块 | 24–32 px | 形成可辨认的分组 |
   | 页面主要章节 | 48–64 px | 建立章节节奏 |

   优先维持这些关系，而后微调单个数值。窗口缩窄时可以整体收紧间距，但仍要保留组内紧、组间松的区别。

6. **先建立共同的对齐线。**

   标题、正文、表格和操作区尽量共享少量稳定的左右边界。重复卡片中的名称、数值和操作位置保持一致，让视线能够横向比较。

   图标与文字需要按视觉重量校准。圆形、箭头和不对称图标即使位于相同的几何中心，也可能显得偏移；可以在统一图标容器内作小幅光学校正。对齐线应在真实内容和换行后仍然成立。

7. **根据任务分配疏密。**

   概览区留出空间让人理解重点，操作区提供适合点击的控件，明细区用紧凑且稳定的行距支持连续比较。同一页面可以有不同密度，只要区域边界清楚。

   展示页可以用较大的章节间距和图片建立节奏；高频工具优先保证内容可见数量与定位效率。Tremor 的表格通过统一单元格内距和横向分隔组织信息，这种稳定的重复适合高密度内容。[^table]

8. **先确定文字角色，再选择字号。**

   从页面标题、区块标题、正文、辅助信息四种角色起步，为每种角色固定字号、字重和行高。标题控制断行，正文保持连续阅读，辅助信息保持清楚可辨。新增字号时，应能说清它承担的新角色。

   大标题与小字号正文要分别检查字形和间距。coss ui 收录的 Cal Sans 指南区分展示字体与 Text UI，并明确这套字体不额外添加字距；这提示我们按字体特性调校，而不是把某种字距当作通用风格。中文界面还要检查中英文混排、标点挤压、数字基线和字体回退。[^type]

   普通产品正文可从 14–16 px 起稿，较长中文正文可先试 1.6–1.8 倍行高，再以实际阅读效果调整。像 Mantine 一样，把字号、行高和字重分别组织成可复用的尺度。[^mantine]

9. **给颜色分配明确的职责。**

   用中性色组织页面、文本和容器，用强调色突出主要动作或选中对象，用状态色表达成功、警告和错误。同一含义保持相同颜色；重要状态同时提供文字、形状或图标线索。

   为背景和前景成对定义颜色，并区分正文、次要文字、边框和浮层。Chakra UI 的语义颜色与 daisyUI 的背景及内容色配对，都适合借鉴到自己的主题中。新增颜色时，先确认现有角色是否已经能够表达它。[^colors]

10. **让边框、底色和阴影各司其职。**

    底色区分区域，边框界定边界，阴影表现浮起的层级。信息已经能靠间距与对齐分组时，可以直接放在页面背景上。需要独立边界的容器，再增加合适的表面处理。

    卡片可以保持很轻的边缘和阴影，浮层则需要从背景中清楚分离。coss ui 的卡片组合了细边框、轻阴影与内侧明暗边缘；可取之处是细节之间的协调。文字、输入框和焦点仍须在实际背景上清楚可辨。[^surface]

11. **让圆角形成一致的几何关系。**

    先确定界面的形状倾向，再为容器、控件和小型标记分配圆角档位。同类控件保持一致，嵌套元素检查内外轮廓之间的距离。

    对均匀内缩、希望形成同心圆弧的容器，可以从“内圆角＝外圆角－内缩距离”起算，并将结果限制为非负值。例如外圆角 16 px、内缩 4 px，内圆角可以先试 12 px。胶囊按钮、图像裁切和独立形状仍按各自的视觉角色处理。

12. **让图标帮助识别，并统一它们的尺度。**

    图标适合表达动作、状态和熟悉的对象。先确保文字本身足够清楚，再判断是否需要图标。同一区域使用一致的线条风格、视觉大小和图文间距；装饰性图标降低存在感，承载操作的图标保持明确。

    图标的视觉尺寸与可点击范围分别设计。coss ui 的按钮在粗指针设备下扩展了命中区域，让紧凑外观仍然便于触摸。只有图标的按钮需要可访问名称，并在必要时提供可见的文字提示。[^button]

13. **让按钮的视觉重量对应操作优先级。**

    在同一个决策区域内，通常保留一个最突出的主要动作，其他动作使用较轻的底色、描边或文本形式。按钮文案直接说明结果，例如“创建项目”“保存设置”“邀请成员”。

    Hover 提示可以操作，按压反馈确认动作正在发生，加载状态说明处理仍在继续。HeroUI 的按钮将背景色变化与轻微按压缩放分开设置，值得借鉴的是反馈清楚且幅度克制。[^hero-button]

14. **把表单说明放在真正需要它的位置。**

    字段名称持续可见，输入示例放在占位文字中，格式要求紧邻字段，错误信息说明如何修正。只给存在歧义、限制或后果的字段增加辅助说明。

    简单表单优先保持单列阅读顺序，只有强相关且内容较短的字段才并排。提交失败后保留已填写内容，并把注意力引向需要处理的位置。coss ui 的 Field 将名称、说明和错误分别组织，方便按需要组合。[^field]

15. **清楚区分悬停、焦点和选中。**

    悬停表示指针所在位置，焦点表示键盘操作对象，选中表示已经生效的选择。三种状态可以同时存在，也应能同时辨认。

    Headless UI 的 Listbox 示例分别用背景强调当前活动项、用字重和勾选符号表达选中项。将这种区分落实到标签页、列表和菜单中，用户就能看清“正在操作哪里”和“已经选择什么”。[^listbox]

16. **为深色模式重新校准层级。**

    分别定义页面、容器、浮层、正文、次要文字和边界的颜色，逐项检查它们的关系。暗背景上的浮层可以通过更亮的表面和轻边缘分离，次要文字也要保留足够的可读性。

    HeroUI 的主题分别设置背景、surface、overlay、muted 和 border，并在深色模式下重新赋值。借鉴这种语义分层，检查悬停、选中、禁用和焦点在两种模式中是否同样明确。[^dark]

17. **让动效保持对象与空间的连续性。**

    菜单从触发位置附近展开，标签页指示器移动到新的选项，卡片展开后延续原来的图片和标题。用户应能沿着运动理解对象的去向。

    Base UI 的 Popover 示例使用与浮层定位关联的变换原点；Motion Primitives 的 Animated Background 与 Morphing Dialog 使用共享布局标识连接状态。应用这类机制时，优先保持对象身份和空间关系，减少不相关内容的同步移动。[^continuity]

18. **为不同动作分配不同节奏。**

    高频操作反馈尽快出现，局部展开给用户一点理解变化的时间，展示性入场可以稍舒展。以下时间可作为起稿范围，再根据位移距离、元素大小、缓动曲线和实际操作频率调校。

    | 动作 | 起稿范围 | 设计重点 |
    | --- | --- | --- |
    | 按压、勾选、颜色反馈 | 100–160 ms | 及时确认操作 |
    | 菜单、提示、局部切换 | 160–240 ms | 保持方向与位置关系 |
    | 抽屉、卡片展开、较大区域过渡 | 240–360 ms | 让空间变化容易跟随 |
    | 展示页面的一次性入场 | 300–500 ms | 建立阅读节奏 |

    入场可使用减速缓动，关闭通常可以更快。弹簧动画要检查回弹、阻尼和稳定时间。Magic UI 的 Blur Fade 提供位移、透明度、模糊和时序参数；正文和主要操作应及时可用，整组内容的等待时间也要一并检查。[^blur]

19. **控制同时发生的运动，并提供安静的状态。**

    一个视区通常只安排一个主要的表现性动效。让其他变化服务于具体操作，装饰性入场播放一次即可。持续运动应有明确用途，并检查是否影响阅读与操作。

    对减少动态效果的偏好，移除非必要位移、缩放和模糊，保留必要的状态区分。React Spectrum 的骨架动画会读取这一偏好；Mantine 的过渡则受主题配置控制。使用组件时，实际验证这一行为。[^reduced]

20. **把次要操作放到上下文中，同时保证可发现。**

    低频操作可以放在更多菜单、选中后的工具栏或对象附近；主要操作和当前任务需要的信息保持可见。

    悬停时出现的内容，也要能通过键盘聚焦或触摸获得。Magic UI 的 Bento Card 在较窄布局中直接显示行动入口，这种处理值得借鉴；最终还要覆盖宽屏触摸设备，并让键盘用户能看见获得焦点的入口。[^bento]

21. **让加载、空白和错误状态保持页面的秩序。**

    骨架屏尽量沿用最终内容的尺寸和位置，按钮进入加载状态时保持宽度，错误出现时尽量避免大幅推移整页。空状态说明当前情况，并给出适合下一步的动作；错误状态保留用户输入，提供明确的修复或重试路径。

    React Spectrum 的 Skeleton 在内容结构上应用占位样式，并同步加载动画的时间；coss ui 的按钮保留文字占位，将加载指示器叠在原位置。这些做法能够让状态变化更稳定。[^loading]

22. **让数据的比较关系成为视觉重点。**

    指标要带着名称、单位、时间范围和必要的比较基准一起出现。“较上月 +12.5%”比孤立的“+12.5%”更容易判断。相同口径的数值使用一致精度与格式，需要逐行比较时右对齐并使用等宽数字。

    图表按问题选择：趋势用折线，类别比较用条形，精确查找用表格。弱化网格和装饰，保持数据系列与图例对应；用长度编码数量的条形图保留零基线，其他尺度选择也应清楚呈现。必要的单位、图例与刻度应保留。

    Tremor 的 Tooltip 将名称和数值分列，并对数值使用等宽数字；AreaChart 允许明确控制轴线、刻度、数值格式和缺失数据的连接方式。先确定比较任务，再选择这些表现方式。[^chart]

23. **在响应式布局中保留任务优先级。**

    根据可用宽度调整列数、控件组合和信息顺序。页面标题、当前上下文和主要操作应始终容易找到。宽度不足时，把次要内容移到后续位置或可展开区域；需要横向比较的表格可以保留横向滚动。

    让组件根据自身容器宽度调整表现。shadcn 的 React、Vue 与 Svelte 指标卡都采用容器查询组织列数和数值字号。可复用的是内容在不同空间中保持主次的规则。[^responsive]

24. **让焦点流向与视觉流向一致。**

    打开弹窗时，把焦点放到合适的标题、字段或操作上；关闭时，将焦点送回触发位置或合理的下一步。键盘顺序应跟随页面阅读顺序，焦点样式保持清楚。

    Radix 的模态 Dialog 管理焦点范围，并在关闭后恢复触发器焦点；Ark UI 提供初始焦点与关闭后焦点的配置。设计弹窗和浮层时，把进入、操作、退出作为一个完整过程。[^focus]

25. **用一套共同尺度吸收不同组件的长处。**

    确定自己的字体角色、间距、控件高度、圆角、颜色职责和动效节奏，再把借用的组件调整到这套尺度中。相同任务的控件保持相同的视觉语言。

    shadcn 的 Nova 与 Maia 同时调整按钮形状、输入框高度、卡片圆角和内部间距，体现了成组协调的价值。品牌个性可以集中在少量稳定特征上，并贯穿整个界面。[^styles]

26. **用真实内容和完整操作检验设计。**

    起稿先放入真实或具有代表性的内容，检查长标题、换行、缺失图片、极端数值、空列表和错误提示。随后在窄屏、宽屏、深色模式、键盘操作及减少动态效果的条件下，走完主要任务。

    评审按内容取舍、布局主次、排版尺度、颜色与状态、动效与细节的顺序进行。遇到视觉杂乱，优先修正信息组织和注意力分配。交付标准是主次明确、阅读顺畅、操作可预期，并且在不同内容和状态下持续成立。

[^bento]: [Magic UI 的 Bento Grid 与 Card](https://github.com/magicuidesign/magicui/blob/efe76fc5755eca1142dd4f74c1d6f0ace2887e3c/apps/www/registry/magicui/bento-grid.tsx#L22)。
[^table]: [Tremor 的表格间距与分隔](https://github.com/tremorlabs/tremor/blob/ca4d588f47820ff3d514d37fa4ee08a4222dec11/src/components/Table/Table.tsx#L57)。
[^type]: [coss ui 收录的 Cal Sans 字体指南](https://github.com/origin-space/originui/blob/3d8ca28e7d90123e9e0f44665944dc240b026ccb/packages/ui/src/fonts/font-guide.md#L19)。
[^mantine]: [Mantine 的字体与间距尺度](https://github.com/mantinedev/mantine/blob/1d8c524fac27bc6ede5441cdff79abceb9e95b5c/packages/@mantine/core/src/core/MantineProvider/default-theme.ts#L31)。
[^colors]: [Chakra UI 的语义颜色](https://github.com/chakra-ui/chakra-ui/blob/960ae222ace1df8de835dc3c62d698f1b58b6786/packages/react/src/theme/semantic-tokens/colors.ts#L3)；[daisyUI 的颜色配对与形状变量](https://github.com/saadeghi/daisyui/blob/bf3bac3a397b543e55641ecb2d60a2ed961f09ec/packages/daisyui/src/themes/light.css#L1)。
[^surface]: [coss ui 的卡片表面处理](https://github.com/origin-space/originui/blob/3d8ca28e7d90123e9e0f44665944dc240b026ccb/apps/ui/registry/default/ui/card.tsx#L8)。
[^button]: [coss ui 的按钮尺度与触摸命中范围](https://github.com/origin-space/originui/blob/3d8ca28e7d90123e9e0f44665944dc240b026ccb/apps/ui/registry/default/ui/button.tsx#L10)。
[^hero-button]: [HeroUI 的按钮反馈](https://github.com/heroui-inc/heroui/blob/70a11531fedfb39b6a0748ca49766266108362ae/packages/styles/components/button.css#L4)。
[^field]: [coss ui 的字段名称、说明与错误](https://github.com/origin-space/originui/blob/3d8ca28e7d90123e9e0f44665944dc240b026ccb/apps/ui/registry/default/ui/field.tsx#L7)。
[^listbox]: [Headless UI 的活动项与选中项](https://github.com/tailwindlabs/headlessui/blob/eea57cf46fd6767ed1059012f7073b88eb159fba/playgrounds/react/page-examples/listbox/listbox-with-pure-tailwind.tsx#L54)。
[^dark]: [HeroUI 的浅色与深色主题](https://github.com/heroui-inc/heroui/blob/70a11531fedfb39b6a0748ca49766266108362ae/packages/styles/themes/default/variables.css#L192)。
[^continuity]: [Base UI 的 Popover 变换原点](https://github.com/mui/base-ui/blob/cc9075a414c93577a10b3085dbc5f122ea2fe564/docs/src/app/%28docs%29/react/components/popover/demos/_index.module.css#L7)；[Motion Primitives 的活动背景](https://github.com/ibelick/motion-primitives/blob/120f64f6ca60348e251f929e9c81f11ccbe45eda/components/core/animated-background.tsx#L70)与[展开对话框](https://github.com/ibelick/motion-primitives/blob/120f64f6ca60348e251f929e9c81f11ccbe45eda/components/core/morphing-dialog.tsx#L116)。
[^blur]: [Magic UI 的 Blur Fade](https://github.com/magicuidesign/magicui/blob/efe76fc5755eca1142dd4f74c1d6f0ace2887e3c/apps/www/registry/magicui/blur-fade.tsx#L34)。
[^reduced]: [React Spectrum 的加载动画偏好处理](https://github.com/adobe/react-spectrum/blob/0752308bb18ca03e55c06892bf8dbf81760c7f78/packages/@react-spectrum/s2/src/Skeleton.tsx#L32)；[Mantine 的过渡配置](https://github.com/mantinedev/mantine/blob/1d8c524fac27bc6ede5441cdff79abceb9e95b5c/packages/@mantine/core/src/components/Transition/use-transition.ts#L39)。
[^loading]: [React Spectrum 的骨架内容结构](https://github.com/adobe/react-spectrum/blob/0752308bb18ca03e55c06892bf8dbf81760c7f78/packages/@react-spectrum/s2/src/Skeleton.tsx#L137)；[coss ui 的按钮加载占位](https://github.com/origin-space/originui/blob/3d8ca28e7d90123e9e0f44665944dc240b026ccb/apps/ui/registry/default/ui/button.tsx#L71)。
[^chart]: [Tremor 的 Tooltip 排版](https://github.com/tremorlabs/tremor/blob/ca4d588f47820ff3d514d37fa4ee08a4222dec11/src/components/AreaChart/AreaChart.tsx#L385)与[坐标轴配置](https://github.com/tremorlabs/tremor/blob/ca4d588f47820ff3d514d37fa4ee08a4222dec11/src/components/AreaChart/AreaChart.tsx#L712)。
[^responsive]: [React 指标卡](https://github.com/shadcn-ui/ui/blob/96da9cc7f1aa10580a3741664e2a77c721206c00/apps/v4/registry/new-york-v4/blocks/dashboard-01/components/section-cards.tsx#L13)；[Vue 指标卡](https://github.com/unovue/shadcn-vue/blob/de1f76cbb4b319ea26b0dea175dc00c18fce3bd0/apps/v4/components/examples/dashboard/components/SectionCards.vue#L15)；[Svelte 指标卡](https://github.com/huntabyte/shadcn-svelte/blob/6149e14107a9de3530a3083de2f1b7623b3c5d1f/docs/src/routes/%28app%29/%28layout%29/examples/dashboard/components/section-cards.svelte#L8)。
[^focus]: [Radix 的模态焦点管理](https://github.com/radix-ui/primitives/blob/eb3a2b7091293e27df8f9ba906632d8daa3d81a3/packages/react/dialog/src/dialog.tsx#L336)；Ark UI 的[初始焦点](https://github.com/chakra-ui/ark/blob/c7af88a51b9dc32e5903a75b3d49b4deaa36e8dc/packages/react/src/components/dialog/examples/initial-focus.tsx#L9)与[关闭后焦点](https://github.com/chakra-ui/ark/blob/c7af88a51b9dc32e5903a75b3d49b4deaa36e8dc/packages/react/src/components/dialog/examples/final-focus.tsx#L8)。
[^styles]: [shadcn Nova 的组件尺度](https://github.com/shadcn-ui/ui/blob/96da9cc7f1aa10580a3741664e2a77c721206c00/apps/v4/registry/styles/style-nova.css#L149)；[shadcn Maia 的组件尺度](https://github.com/shadcn-ui/ui/blob/96da9cc7f1aa10580a3741664e2a77c721206c00/apps/v4/registry/styles/style-maia.css#L149)。

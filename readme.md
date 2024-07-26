readme.md直接显示在首页，用来放cocoslua笔记了

修改文件不需要重启游戏：
```lua
function RedBagListLayer:ctor()
    startTestLuaFile("ui.redbag.RedBagListLayer")
end
-- src是根目录 把参数改成该文件对应的路径就可以
```

```lua
-- 加上描边
text:enableOutline(color,size)
--去掉描边或阴影
text:disableEffect(cc.LabelEffect.OUTLINE)
text:disableEffect(cc.LabelEffect.SHADOW)
--设置可见与不可见
image:setVisible(true)
image:setVisible(false)
--创建图片
local img = ccui.ImageView:create()
-- 或者
local img = extend(ccui.ImageView:create()) --(自己封装的extend)
img:loadTexture("file.png")
-- 设置图片圆角(没试过)
img:setTextureRect(cc.rect(10, 10, 10, 10))
```

调用对象方法时，可以用.或:调用例如方法名是func
```lua
self.func(x,y) --1.
self:func() --2.
方法1调用时参数表所见即所得，被调用方法体内self为空
方法2调用时，会在第一个参数添加self，self即为调用者的self
```
改变图片大小
```lua
widget:setScale9Enabled(true)
bgImage:setCapInsets(cc.rect(10, 10, 10, 10))

-- 修改图片尺寸
image:setContentSize(cc.size(x,y))
-- 需要先允许九宫格拉伸 修改尺寸才有效 也就是这样
image:setScale9Enabled(true)
image:setContentSize(cc.size(x,y))
--允许九宫格拉伸之后可以设置九宫格拉伸参数
image:setCapInsets(cc.rect(10, 10, 10, 10)) 


node:ignoreContentAdaptWithSize()
-- 使setContentSize()无效 从UI工程里读到的大小是多少就是多少
node:ignoreContentAdaptWithSize(false)-- loadText()替换图片时会改变图片大小，使该对象大小不变
node:ignoreContentAdaptWithSize(true)--  loadText()替换图片时会根据图片改变对象大小
```
按钮是否可以点击
```lua
btn:setEnabled(true)
btn:setEnabled(false)
```
设置图片z轴
```lua
select:setZOrder(num)
-- z轴数值小的被数值大的遮挡
```

对象不可点击时置灰
```lua
helper.GrayManager:setGray(self.fail_bg, true)
```

颜色格式转换
```lua
colorToccc3Type("#ffffff")
```
获得节点尺寸信息
```lua
getSize():
-- 这个方法返回的是节点在父节点坐标系中的实际大小。
-- 这个大小包括了节点的缩放、旋转等属性的影响。
-- 换句话说,就是节点在场景中实际占用的空间大小。
getContentSize():
-- 这个方法返回的是节点自身内容的大小。
-- 这个大小不受节点的缩放、旋转等属性的影响。
-- 它代表了节点原始的、未经任何变换的大小。

-- .width 和 .height可以获得宽高
x:getSize().width
x:getContentSIze().height
```


设置锚点 设置大小
```lua
x:setAnchorPoint(cc.p(0,0))
x:setContentSize(cc.size(114,514))
```
获得坐标
```lua
local x,y = node:getPosition()
```

setColor() 和 setTextColor:
```txt
setColor会和之前已有的颜色混合
setTextColor会覆盖之前的颜色
```
滑动效果：
```lua
--列表容器 / 滚动容器
--listview / scrollview

-- listview
local listview = ccui.ListView:create()
listview:setPosition(cc.p(panel_x, panel_y))
listview:setContentSize(cc.size(panel_w, panel_h))
listview:setDirection(ccui.ListViewDirection.horizontal) --水平方向
listview:setItemsMargin(114514) -- 设置元素间隔
listview:pushBackCustomItem(layout)

-- scrollview
local scroll = extend(ccui.ScrollView:create())
scroll:setAnchorPoint(cc.p(0, 0))
scroll:setPosition(cc.p(0, 0))
scroll:setDirection(ccui.ScrollViewDir.horizontal) --横向
scroll:setDirection(ccui.ScrollViewDir.vertical)   --纵向
scroll:setContentSize(cc.p(114,514))
scroll:setBounceEnabled(false)
scroll:setInnerContainerSize(cc.size(114,514)) -- 设置可拖动区域大小
-- 当可拖动区域大小大于ContentSize时, 对象就可以被拖动了
scroll:addChild(item) --item的位置在滑动方向上不能为负 否则不可见
```

创建按钮参考:
``` lua
CommonTabNode.lua
createCommonTabBtn()
-- 工作环境有效
```
获得屏幕实际大小
```lua
local winSize = cc.Director:getInstance():getWinSize()
local platform_scale = getPlatformScale(true)
winSize / platform_scale --获得屏幕实际大小
```

弹窗太大，把dataToUI的4，5，6个参数改成nil,nil,true
```lua
dataToUI(1,2,3,nil,nil,true)
```

弹窗动画
```lua
local move = cc.MoveTo:create(time,cc.p(0,105 * item.scale))
local scaleAct = cc.ScaleTo:create(time,0.01)
local fadeOut = cc.FadeOut:create(time) -- 淡出 在消失时会慢慢变淡
local spawn = cc.Spawn:create(move,scaleAct,fadeOut) --三个动作同时进行{移动 缩小 淡出}
node:runAction(spawn)
```

将接收到的点击效果传给父节点
```lua
bg:setSwallowTouches(false) --不会吞掉触摸效果
-- 常用场景:scrollview上有背景 背景上有按钮  对背景使用
-- 使用clone()时不会克隆这个属性
```

colorText
```lua
local newText = createColorText("<color:#ffdf5e>some word</color> <color:#ffffff>some word</color>",fontSize,ContentSize,baseColor)
-- baseColor不会影响前面的<color>标签
function createColorText(str, fontSize, contentSize, baseColor, outlinecolor, outlinesize,fontname)
    ...
end
```

创建文字获得大小
```lua
local text = ccui.Text:create()
text:setString(msg.m_szMessage)
text:setFontName(DEFAULT_FONT)
text:setFontSize(22)
local size = text:getContentSize()
```

进度条
```lua
local bar = ccui.LoadingBar:create("ui_main/HeartSystem/BigHeart.png")
bar:setRotation(-90) --旋转90度
bar:setPercent(curExp / maxExp * 100)
```

创建角色
```lua
armature = createHeroArmature(ppdata.Heros:getHero(iCardID))
```

按钮回调函数
```lua
tab:setCallback(handler(self, function), nil, true) --有回弹效果
tab:setCallback(handler(self, function), true, true) --无回弹效果
```

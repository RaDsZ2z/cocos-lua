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

local img = extend(ccui.ImageView:create()) --(自己封装的extend)
img:loadTexture("file.png")
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
widget:setScale9Enabled(true)
image:setContentSize(cc.size(x,y))
-- 使setContentSize()无效 从UI工程里读到的大小是多少就是多少
-- 替换图片的时候会改变图片大小，使该对象大小不变
node:ignoreContentAdaptWithSize(true)
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
x:setAnchroPoint(cc.p(0,0))
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
listview:setItemsMargin(3.00) -- 设置元素间隔
listview:pushBackCustomItem(layout)

-- scrollview
local scroll = extend(ccui.ScrollView:create())
scroll:setAnchorPoint(cc.p(0, 0))
scroll:setPosition(cc.p(0, 0))
scroll:setDirection(ccui.ScrollViewDir.horizontal)
scroll:setContentSize(winSize)
scroll:setBounceEnabled(false)
scroll:setInnerContainerSize(cc.size(innerWidth, winSize.height)) -- 设置元素大小
scroll:pushBackCustomItem(item)
```

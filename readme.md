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
-- 使setContentSize()无效
node:ignoreContentAdaptWithSize(true)
```

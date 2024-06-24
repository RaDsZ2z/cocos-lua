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

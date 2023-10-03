# IJeiUtils

## Import

```csharp
import mods.randomtweaker.jei.IJeiUtils;
```

## Static ZenMethod

| 方法名| 返回值类型| 方法作用 |
| :------ | ------ | ------ |
| createBackground(int width, int height)| IJeiBackground | 创建背景(贴图为默认) |
| createBackground(int u, int v, int width, int height, String resourceName)| IJeiBackground | 创建背景(贴图通过resourceName路径指定) |
| createLiquidSlot(int x, int y, int width, int height, int capacityMb, boolean showCapacity,boolean isInput, @Optional(valueBoolean = true) boolean hasBase)| IJeiSlotLiquid | 创建流体槽位(参数见下讲解) |
| createLiquidSlot(int x, int y, boolean isInput, @Optional(valueBoolean = true) boolean hasBase)| IJeiSlotLiquid | 同上 |
| createLiquidSlot(String slotName, int x, int y, int width, int height, int capacityMb, boolean showCapacity,boolean isInput, @Optional(valueBoolean = true) boolean hasBase)| IJeiSlotLiquid | 同上 |
| createLiquidSlot(String slotName, int x, int y, boolean isInput, @Optional(valueBoolean = true) boolean hasBase)| IJeiSlotLiquid | slotName为指定槽位的id，x与y控制槽位的方位，width槽位宽度，height槽位长度，isInput 为是否是输入流体, hasBase 为是否渲染默认的流体槽 (需对比宽高)，流体槽必须要根据固定的宽高创建 (eg：16 * 16, 43 * 16, 16 * 34)，其余不知，可自行探索|
| createItemSlot(int x, int y, boolean isInput, @Optional(valueBoolean = true) boolean hasBase)| IJeiSlotItem | 创建物品槽位(参数见下讲解) |
| createItemSlot(String slotName, int x, int y, boolean isInput, @Optional(valueBoolean = true) boolean hasBase)| IJeiSlotItem | slotName为指定槽位的id，x与y控制槽位的方位，width槽位宽度，height槽位长度，isInput 为是否是输入流体, hasBase 为是否渲染默认的流体槽 (需对比宽高)，流体槽必须要根据固定的宽高创建 (eg：16 * 16, 43 * 16, 16 * 34)，其余不知，可自行探索 |
| createItemInputElement(int x, int y)| IJeiElements | 创建物品输入元素 |
| createItemInputElement(String elementName, int x, int y)| IJeiElements | 创建物品输入元素，elementName为元素的id |
| createItemOutputElement(int x, int y)| IJeiElements | 创建物品输出元素 |
| createItemOutputElement(String elementName, int x, int y)| IJeiElements | 创建物品输出元素，elementName为元素的id |
| createLiquidElement(int x, int y, int width, int height)| IJeiElements | 创建流体元素 |
| createLiquidElement(String elementName, int x, int y, int width, int height)| IJeiElements | 创建流体元素，elementName为元素的id |
| createFontInfoElement(String info, int x, int y, int color, @Optional int width, @Optional int height)| IJeiElements | 创建文字元素 |
| createFontInfoElement(String elementName, String info, int x, int y, int color, @Optional int width, @Optional int height)| IJeiElements | 创建文字元素，elementName为元素的id |
| createArrowElement(int x, int y, int direction)| IJeiElements | 创建箭头元素，direction 参数为四个箭头, 可填 0, 1, 2, 3 |
| createArrowElement(String elementName, int x, int y, int direction)| IJeiElements | 创建箭头元素，direction 参数为四个箭头, 可填 0, 1, 2, 3，elementName为元素的id |
| createImageElement(String elementName, int x, int y, int width, int height, int u, int v,String texture, int textureWidth, int,textureHeight)| IJeiElements | 创建图片元素，texture 的格式为 modid:path，elementName为元素的id |
| createJeiManaBarElement(int x, int y, int mana, @Optional int mode)| IJeiElements | 创建魔力条元素，mana 为植物魔法魔力值，mode为1时填显示的魔力上限会缩小并显示缩小的倍数，不为1时上限为魔力池上限 |
# IJeiUtils

## Import

```csharp
import mods.randomtweaker.jei.IJeiUtils;
```

## Static ZenMethod

| 方法名| 返回值类型| 方法作用 |
| :------ | ------ | ------ |
| createBackground(width as int, height as int)| IJeiBackground | 创建背景(贴图为默认) |
| createBackground(u as int, v as int, width as int, height as int, resourceName as string)| IJeiBackground | 创建背景(贴图通过resourceName路径指定) |
| createLiquidSlot(x as int, y as int, width as int, height as int, capacityMb as int, showCapacity as bool,isInput as bool,hasBase as bool(此参数可不写默认为true))| IJeiSlotLiquid | 创建流体槽位(参数见下讲解) |
| createLiquidSlot(x as int, y as int, isInput as bool, hasBase as bool(此参数可不写默认为true))| IJeiSlotLiquid | 同上 |
| createLiquidSlot(String slotName, x as int, y as int, width as int, height as int, capacityMb as int, showCapacity as bool,isInput as bool, hasBase as bool(此参数可不写默认为true))| IJeiSlotLiquid | 同上 |
| createLiquidSlot(String slotName, x as int, y as int, isInput as bool, hasBase as bool(此参数可不写默认为true))| IJeiSlotLiquid | slotName为指定槽位的id，x与y控制槽位的方位，width槽位宽度，height槽位长度，isInput 为是否是输入流体, hasBase 为是否渲染默认的流体槽 (需对比宽高)，流体槽必须要根据固定的宽高创建 (eg：16 * 16, 43 * 16, 16 * 34)，其余不知，可自行探索|
| createItemSlot(x as int, y as int, isInput as bool, hasBase as bool(此参数可不写默认为true))| IJeiSlotItem | 创建物品槽位(参数见下讲解) |
| createItemSlot(String slotName, x as int, y as int, isInput as bool, hasBase as bool(此参数可不写默认为true))| IJeiSlotItem | slotName为指定槽位的id，x与y控制槽位的方位，width槽位宽度，height槽位长度，isInput 为是否是输入流体, hasBase 为是否渲染默认的流体槽 (需对比宽高)，流体槽必须要根据固定的宽高创建 (eg：16 * 16, 43 * 16, 16 * 34)，其余不知，可自行探索 |
| createItemInputElement(x as int, y as int)| IJeiElements | 创建物品输入元素 |
| createItemInputElement(elementName as string, x as int, y as int)| IJeiElements | 创建物品输入元素，elementName为元素的id |
| createItemOutputElement(x as int, y as int)| IJeiElements | 创建物品输出元素 |
| createItemOutputElement(elementName as string, x as int, y as int)| IJeiElements | 创建物品输出元素，elementName为元素的id |
| createLiquidElement(x as int, y as int, width as int, height as int)| IJeiElements | 创建流体元素 |
| createLiquidElement(elementName as string, x as int, y as int, width as int, height as int)| IJeiElements | 创建流体元素，elementName为元素的id |
| createFontInfoElement(info as string, x as int, y as int, color as int, width as int(可为空), height as int(可为空))| IJeiElements | 创建文字元素 |
| createFontInfoElement(elementName as string, info as string, x as int, y as int, color as int, width as int(可为空), height as int(可为空))| IJeiElements | 创建文字元素，elementName为元素的id |
| createArrowElement(x as int, y as int, direction as int)| IJeiElements | 创建箭头元素，direction 参数为四个箭头, 可填 0, 1, 2, 3 |
| createArrowElement(elementName as string, x as int, y as int, direction as int)| IJeiElements | 创建箭头元素，direction 参数为四个箭头, 可填 0, 1, 2, 3，elementName为元素的id |
| createImageElement(elementName as string, x as int, y as int, width as int, height as int, u as int, v as int,texture as string,  textureWidth as int, textureHeight as int)| IJeiElements | 创建图片元素，texture 的格式为 modid:path，elementName为元素的id |
| createJeiManaBarElement(x as int, y as int, mana as int, mode as int(可为空))| IJeiElements | 创建魔力条元素，mana 为植物魔法魔力值，mode为1时填显示的魔力上限会缩小并显示缩小的倍数，不为1时上限为魔力池上限 |
# IJeiPanel

## Import

```csharp
import mods.randomtweaker.jei.IJeiPanel;
```

## Static ZenMethod

| 方法名| 返回值类型| 方法作用 |
| :------ | ------ | ------ |
| setModid(modid as string)| IJeiPanel | 设置显示的模组id |
| setIcon(icon as IItemStack)| IJeiPanel | 设置界面的显示 |
| addSlot(slot as IJeiSlot)| IJeiPanel | 增加槽位 |
| setSlots(slots as IJeiSlot[])| IJeiPanel | 设置一堆槽位 |
| onTooltip(tooltip as IJeiTooltip)| IJeiPanel | 为指定的地方添加新的提示 (不会覆盖 Item 和 Fluid) |
| addElement(elements as IJeiElement)| IJeiPanel | 增加界面的元素 |
| setElements(elements as IJeiElement[])| IJeiPanel | 设置界面的元素 |
| addRecipeCatalyst(stack as IItemStack)| IJeiPanel | 增加配方的元素(按 R 或者按 U 键，JEI 能显示合成或者作用的物品) |
| setRecipeCatalysts(stacks as IItemStack[])| IJeiPanel | 设置配方的元素(按 R 或者按 U 键，JEI 能显示合成或者作用的物品) |
| setBackground(background as IJeiBackground)| IJeiPanel | 设置界面的背景 |
| getJeiSlots()| IJeiSlot[] | 获取界面的槽位 |
| getJeiSlot(slotName as string)| IJeiSlot | 根据槽位id获取槽位 |
| getJeiElements()| IJeiElement[] | 获取界面的元素 |
| getJeiElement(elementName as string)| IJeiElement | 根据槽的id获取界面的元素 |
| register()| 无 | 注册jei界面 |
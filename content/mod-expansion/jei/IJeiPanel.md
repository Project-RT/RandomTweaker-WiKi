# IJeiPanel

## Import

```csharp
import mods.randomtweaker.jei.IJeiPanel;
```

## Static ZenMethod

| 方法名| 返回值类型| 方法作用 |
| :------ | ------ | ------ |
| setModid(String modid)| IJeiPanel | 设置显示的模组id |
| setIcon(IItemStack icon)| IJeiPanel | 设置界面的显示 |
| addSlot(IJeiSlot slot)| IJeiPanel | 增加槽位 |
| setSlots(IJeiSlot[] slots)| IJeiPanel | 设置一堆槽位 |
| onTooltip(IJeiTooltip tooltip)| IJeiPanel | 为指定的地方添加新的提示 (不会覆盖 Item 和 Fluid) |
| addElement(IJeiElement elements)| IJeiPanel | 增加界面的元素 |
| setElements(IJeiElement[] elements)| IJeiPanel | 设置界面的元素 |
| addRecipeCatalyst(IItemStack stack)| IJeiPanel | 增加配方的元素 |
| setRecipeCatalysts(IItemStack[] stacks)| IJeiPanel | 设置配方的元素 |
| setBackground(IJeiBackground background)| IJeiPanel | 设置界面的背景 |
| getJeiSlots()| IJeiSlot[] | 获取界面的槽位 |
| getJeiSlot(String slotName)| IJeiSlot | 根据槽位id获取槽位 |
| getJeiElements()| IJeiElement[] | 获取界面的元素 |
| getJeiElement(String elementName)| IJeiElement | 根据槽的id获取界面的元素 |
| register()| 无 | 注册jei界面 |
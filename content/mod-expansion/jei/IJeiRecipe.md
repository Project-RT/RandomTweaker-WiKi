# IJeiRecipe

## Import

```csharp
import mods.randomtweaker.jei.IJeiRecipe;
```

## Static ZenMethod

| 方法名| 返回值类型| 方法作用 |
| :------ | ------ | ------ |
| addInput(IIngredient input)| IJeiRecipe | 增加输入 |
| setInputs(IIngredient[] inputs)| IJeiRecipe | 设置一堆输入 |
| addOutput(IIngredient output)| IJeiRecipe | 增加输出 |
| setOutputs(IIngredient[] outputs)| IJeiRecipe | 设置一堆输出 |
| setElements(IJeiElement[] elements)| IJeiRecipe | 设置一堆元素(独属于这个配方的) |
| addElement(IJeiElement element)| IJeiRecipe | 增加元素(独属于这个配方的) |
| onJEITooltip(IJeiTooltip tooltip)| IJeiRecipe | 为指定的地方添加新的提示 (不会覆盖 Item 和 Fluid)|
| build()| 无 | 注册jei配方 |
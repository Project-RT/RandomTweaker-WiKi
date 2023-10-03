# IJeiRecipe

## Import

```csharp
import mods.randomtweaker.jei.IJeiRecipe;
```

## Static ZenMethod

| 方法名| 返回值类型| 方法作用 |
| :------ | ------ | ------ |
| addInput(input as IIngredient)| IJeiRecipe | 增加输入 |
| setInputs(inputs as IIngredient[])| IJeiRecipe | 设置一堆输入 |
| addOutput(output as IIngredient)| IJeiRecipe | 增加输出 |
| setOutputs(outputs as IIngredient[])| IJeiRecipe | 设置一堆输出 |
| setElements(elements as IJeiElement[])| IJeiRecipe | 设置一堆元素(独属于这个配方的) |
| addElement(element as IJeiElement)| IJeiRecipe | 增加元素(独属于这个配方的) |
| onJEITooltip(tooltip as IJeiTooltip)| IJeiRecipe | 为指定的地方添加新的提示 (不会覆盖 Item 和 Fluid)|
| build()| 无 | 注册jei配方 |
# Attunement Altar

此类为 `CrT` 提供了添加共鸣祭坛配方的功能

## import

```csharp
import mods.randomtweaker.astralsorcery.AttunementAltar;
```

## Static ZenMethod

| 方法名 | 参数解释 |
| :------ | ------ |
| addRecipe(input as IIngredient, output as IItemStack, constellation as string) | `input` 为输入物品, `output` 为输出物品, `constellation` 为指定共鸣的星座名称,  |
| addRecipe(input as IIngredient, output as IItemStack) | 上同, 但无需指定共鸣某个星座 |

## Example

```csharp
import mods.randomtweaker.astralsorcery.AttunementAltar;

// 添加后自行查看 JEI
// 这个名称可以通过 /as constellation playerName 再按个 tab 查看
// 或者查看 mcmod 里的资料的英文名称, 需要全小写
// 共鸣祭坛会优先匹配有星座的配方
AttunementAltar.addRecipe(<minecraft:stick>, <minecraft:dirt>, "astralsorcery.constellation.discidia");
AttunementAltar.addRecipe(<minecraft:dirt>, <minecraft:stick>);
```

# IInputPattern

为解决类似无尽合成需要填写大量物品尖括号的问题而诞生的工具类

## Import

```csharp
import mods.randomtweaker.utils.IInputPattern;
```

## Global Function

此类注册了两个全局函数供 `zs` 使用

全局函数意味着你可以直接调用这些函数

### inputPattern

`pattern` 参数可填类似 `"ABC", "EFG"` 或 `["ABC", "EFG"]`

此方法会返回自身, 也就是 `IInputPattern` 类实例

```csharp
// 实际上 zs 并不支持 as string...

inputPattern(pattern as string...);
```

### inputPatternGet

`pattern` 参数可填类似 `["ABC", "EFG"]`

此方法会返回 IIngredient[][]

```csharp
inputPatternGet(pattern as string[], mapping as IIngredient[string])
```

## ZenMethod

| 方法名 | 返回值类型 | 方法及返回值描述 |
| :-------- | -------- | -------- |
| create(pattern as string[]) | IInputPattern | 创建一个 IInputPattern 对象并指定 `pattern` |
| with(character as string, ingredient as IIngredient) | IInputPattern | 指定 `pattern` 中某单个字符代表的物品或矿辞 |
| transform(mapping as IIngredient[string]) | IInputPattern | 上同, 只不过可以一次性指定多个单个字符代表的物品或矿辞 |
| get() | IIngredient[][] | 返回由 `pattern` 及其字符代表的物品或矿辞组成的 IIngredient 二维数组 |
| getWithShapeless() | IIngredient[] | 上同, 只不过返回的是二维数组中的第一个元素 |

## Example

```csharp
import mods.randomtweaker.utils.IInputPattern;

// 下面介绍两种创建 IInputPattern 实例的方法

//第一种
var inputPattern1 as IInputPattern = IInputPattern.create
([
    "ABA",
    "BAB",
    "ABA"
]);

//第二种
var inputPattern2 as IInputPattern = inputPattern(
    "AB",
    "BA"
);

//下面介绍 with 方法和 transform 方法的用法

// with 的用法
// 这就是火药的合成
inputPattern1.with("A", <minecraft:gunpowder>) // 填了个具体物品 (火药)
.with("B", <ore:sand>); // 填了沙子矿辞

// transform 的用法
// 这就是闪长岩的合成
inputPattern2.transform({
    "A" : <minecraft:cobblestone>,
    "B" : <minecraft:quartz>
});

// 最后, pattern 和其内字符的含义已定义完毕, 该添加合成了

recipes.addShaped(<minecraft:tnt>, inputPattern1.get());

recipes.addShaped(<minecraft:stone:3> * 2, inputPattern2.get());

//-----------------------------------------------------------

// 还有一种一步到位的方式--inputPatternGet
// 这是荧石的合成
recipes.addShaped(<minecraft:glowstone>, inputPatternGet([
    "AA",
    "AA"
], {
    "A" : <minecraft:glowstone_dust>
}));

// 接下来为无序合成
// 这是苔石的合成
// 两种方式
recipes.addShapeless("recipe1", <minecraft:mossy_cobblestone>, inputPatternGet([
    "AB"
], {
    "A" : <minecraft:cobblestone>,
    "B" : <minecraft:vine>
})[0]);

recipes.addShapeless("recipe2", <minecraft:mossy_cobblestone>, inputPattern("AB")
.transform({ // 这里其实也可以用 with 方法指定 A 字符和 B 字符代表的东西
    "A" : <minecraft:cobblestone>,
    "B" : <minecraft:vine>
}).getWithShapeless());
```

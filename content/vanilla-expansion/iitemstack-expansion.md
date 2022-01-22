# IItemStack Expansion

此类为 [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack) 的扩展类

这意味着 `IItemStack` 类实例可以直接使用此类的方法

## Import

你完全没必要导这个包, 除非你想用类名调用扩展类方法

```csharp
import mods.randomtweaker.vanilla.IItemStack;
```

## Static ZenMethod

| 方法名 | 返回值类型 | 方法作用 |
| :------ | ------ | ------ |
| getTagSize() | int | 返回物品的 `NBT` 中有多少个 `key` |

## Example

```csharp
// 实际上你永远都不需要这个导包, 除非犯病了
// 因为跟 CrT 自带的 IItemStack 类的类名重合所以要用 as 关键字重定向类名
import mods.randomtweaker.vanilla.IItemStack as IItemStackExpansion;
import crafttweaker.item.IItemStack;

var stone as IItemStack = <minecraft:stone>; // 石头
var cobbleStone as IItemStack = <minecraft:cobblestone>; // 圆石

// 两种使用扩展类的方法的方式
// 第一种, 用扩展类类名调用, 一般来说, 你不应该用这种方式, 应该使用第二种方式
// 使用这种方式调用的方法, 需要在括号内填入 IItemStack 类实例作为实参
// 这里重定向了类名所以用 IItemStackExpansion 调用
print(IItemStackExpansion.getTagSize(stone)); // 会输出 0, 因为没有 nbt
print(IItemStackExpansion.getTagSize(cobbleStone)); // 同上


// 第二种, IItemStack 类实例直接调用方法
print(stone.getTagSize()); // 会输出 0, 因为没有 nbt
print(cobbleStone.getTagSize()); // 同上

// 现在让我们修改 stone 变量和 cobbleStone 变量存储的物品
stone = <minecraft:stone>.withTag({"key1" : "value1" as string}); // 还是石头物品, 但是带 nbt
cobbleStone = <minecraft:cobblestone>.withTag({"key2" : "value2" as string, "key3" : "value3" as string}); // 还是圆石物品, 但是带 nbt

// 现在再 pirnt 一次 getTagSize 方法的结果
print(stone.getTagSize()); // 会输出 1, 因为只有 key1 这一个 key
print(cobbleStone.getTagSize()); // 会输出 2, 因为 key2 和 key3 共两个 key

// 还有一种情况
// 带空 nbt 的情况
var plank as IItemStack = <minecraft:planks>.withTag({}); // 橡木木板, 但是带空 nbt

// 这个时候 print 一下 getTagSize 方法的结果, 会发生什么呢
print(plank.getTagSize()); // 会输出 0, 因为 nbt 内没有任何内容
```

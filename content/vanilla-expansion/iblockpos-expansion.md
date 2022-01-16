# IBlockPos Expansion

此类为 [IBlockPos](https://docs.blamejared.com/1.12/en/Vanilla/World/IBlockPos) 的扩展类

这也意味着 `IBlockPos` 类实例可以直接使用此类的方法

## Import

你完全没必要导这个包, 除非你想用类名调用扩展类方法

```csharp
import mods.randomtweaker.vanilla.IBlockPos;
```

## Static ZenMethod

| 方法名 | 返回值类型 | 方法作用 |
| :------ | ------ | ------ |
| getAllInBox(from as IBlockPos, to as IBlockPos) | IBlockPos[] | 返回 `from` 参数到 `to` 参数范围内所有的 `IBlockPos` 对象的集合 |
| add(x as double, y as double, z as double) | IBlockPos | 返回坐标偏移 `xyz` 参数后的新坐标 |
| add(x as int, y as int, z as int) | IBlockPos | 同上 |
| up(@Optional n as int) | IBlockPos | 返回坐标向上偏移 `n` 个方块距离后的新坐标, 其中 `n` 默认为 `1` (可不填 `n` 参数) |
| down(@Optional n as int) | IBlockPos | 返回坐标向下偏移 `n` 个方块距离后的新坐标, `n` 参数含义同上 |
| north(@Optional n as int) | IBlockPos | 返回坐标向北偏移 `n` 个方块距离后的新坐标, `n` 参数含义同上 |
| south(@Optional n as int) | IBlockPos | 返回坐标向南偏移 `n` 个方块距离后的新坐标, `n` 参数含义同上 |
| west(@Optional n as int) | IBlockPos | 返回坐标向西偏移 `n` 个方块距离后的新坐标, `n` 参数含义同上 |
| east(@Optional n as int) | IBlockPos | 返回坐标向东偏移 `n` 个方块距离后的新坐标, `n` 参数含义同上 |

## Example

```csharp
import crafttweaker.world.IBlockPos;

// 在这里就不介绍用扩展类类名调用方法的方式了, 详情请看 IItemStack Expansion 的内容
// 首先先创建两个 IBlockPos 对象作为示例

var posOne as IBlockPos = IBlockPos.create(0, 0, 0);
var posTwo as IBlockPos = IBlockPos.create(1, 1, 1);

// getAllInBox 方法的用法
// 此方法只能由类名调用, 用对象调用会报错
// posOne.getAllInBox(posTwo); 会报 No such member in crafttweaker.world.IBlockPos: getAllInBox

// 只能这么调用 getAllInBox 方法
var posCollection as IBlockPos[] = IBlockPos.getAllInBox(posOne, posTwo);
// 接下来打印集合内的成员

for pos in posCollection {
    print("坐标 : " ~ pos.x ~ "," ~ pos.y ~ "," ~ pos.z);
}

/* 结果 :
坐标 : 0,0,0
坐标 : 1,0,0
坐标 : 0,1,0
坐标 : 1,1,0
坐标 : 0,0,1
坐标 : 1,0,1
坐标 : 0,1,1
坐标 : 1,1,1
*/

// 接下来是 add 方法
// 有两个 add 方法, 一个接受整型 (int) 参数, 一个接受双精度浮点数 (double)

var posOneAdded as IBlockPos = posOne.add(1, 1, 1); //调用接受整型的 add 方法
var posTwoAdded as IBlockPos = posTwo.add(2.5D, 2.5D, 2.5D); //调用接受双精度浮点数的 add 方法

// print 一下 add 后的结果
print("PosOne Add 后的结果 : " ~ posOneAdded.x ~ "," ~ posOneAdded.y ~ "," ~ posOneAdded.z); // 会打印 PosOne Add 后的结果 : 1,1,1
print("PosTwo Add 后的结果 : " ~ posTwoAdded.x ~ "," ~ posTwoAdded.y ~ "," ~ posTwoAdded.z); // 会打印 PosTwo Add 后的结果 : 3,3,3

// 等一下, 为什么第二个 print 的结果也是整数坐标?
// 这是因为 IBlockPos 存储的是整型数据, 所以最后拿到的 xyz 都是整数
// 查看源码后, 我们得知接受双精度浮点数的 add 方法是这么 add 的
// 拿 posTwoAdded 举例子
// 首先 1 + 2.5 得到 3.5, 然后 3.5 向下取整得到 3
// 所以坐标就变成了 3,3,3

// 在这里, add 或以下方法都是创建新的 IBlockPos 对象, 而不是对原先的对象进行修改
// 所以不要干这种蠢事 : 
// posOne.add(2, 2, 2); // 这是创建新的 IBlockPos 对象
// print("" ~ posOne.x ~ "," ~ posOne.y ~ "," ~ posOne.z); // 会打印 0,0,0 而不是 2,2,2

//-----------------------------------------------

// 以下是上表其余的方法

// up
// 向 y 轴正半轴偏移
print(posOne.up().y); // 不填参数默认偏移 1 格, 在这里会打印 1
print(posOne.up(3).y); // 在这里会打印 3

// down
// 向 y 轴负半轴偏移
print(posOne.down().y); // 不填参数默认偏移 1 格, 在这里会打印 -1
print(posOne.down(3).y); // 在这里会打印 -3

// north
// 向 z 轴负半轴偏移
print(posOne.north().z); // 不填参数默认偏移 1 格, 在这里会打印 -1
print(posOne.north(3).z); // 在这里会打印 -3

// south
// 向 z 轴正半轴偏移
print(posOne.south().z); // 不填参数默认偏移 1 格, 在这里会打印 1
print(posOne.south(3).z); // 在这里会打印 3

// west
// 向 x 轴负半轴偏移
print(posOne.west().x); // 不填参数默认偏移 1 格, 在这里会打印 -1
print(posOne.west(3).x); // 在这里会打印 -3

// east
// 向 x 轴正半轴偏移
print(posOne.east().x); // 不填参数默认偏移 1 格, 在这里会打印 1
print(posOne.east(3).x); // 在这里会打印 3
```

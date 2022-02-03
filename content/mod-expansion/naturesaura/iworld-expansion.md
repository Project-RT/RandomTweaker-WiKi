# IWorld Expansion

此类为 [IWorld](https://docs.blamejared.com/1.12/en/Vanilla/World/IWorld) 类的扩展类, 这意味着 `IWorld` 类实例可以直接使用此类的方法

## Import

你完全没必要导包, 除非你想用类名调用扩展类方法

```csharp
import mods.randomtweaker.naturesaura.IWorld;
```

## Static ZenMethod

| 方法名 | 返回值类型 | 方法描述 |
| :------ | ------ | ------ |
| getAuraChunk(pos as IBlockPos) | [IAuraChunk](iaurachunk.md) | 返回 `pos` 所在的灵气区块 |
| getHighestSpot(pos as IBlockPos, radius as int, defaultSpot as IBlockPos) | IBlockPos | 返回以 `pos` 为中心, `radius` 为半径的范围内灵气量最高的坐标, 如果最高灵气量小于 0 则返回 `defaultSpot` 的值 |
| getLowestSpot(pos as IBlockPos, radius as int, defaultSpot as IBlockPos) | IBlockPos |上同, 但最低灵气量大于 0 时才返回 `defaultSpot` 的值 |
| getSpotAmountInArea(pos as IBlockPos, radius as int) | int | 返回以 `pos` 为中心, `radius` 为半径的范围内的灵气点总和 |
| getAuraInArea(pos as IBlockPos, radius as int) | int | 返回以 `pos` 为中心, `radius` 为半径的范围内的灵气总和 |
| triangulateAuraInArea(pos as IBlockPos, radius as int) | int | 上同, 但每个灵气点的灵气量都会乘于与 `pos` 的距离的百分比 (百分比 : `1 - (pos 到灵气点的距离 / radius`)) |

## Example

```csharp
//以下内容涉及事件, 不会事件请先学习
import crafttweaker.world.IBlockPos;
import crafttweaker.event.PlayerRightClickItemEvent; // 玩家右键物品事件
import mods.randomtweaker.naturesaura.IAuraChunk;

events.onPlayerRightClickItem(function(event as PlayerRightClickItemEvent) {
    var player as IPlayer = event.player; // 获取触发事件的玩家
    var world as IWorld = event.world; // 获取触发事件的玩家所在的世界

    if(!world.remote && <minecraft:stick>.matches(event.item)) { // 先确保在服务端执行代码, 再判断手上物品是否为木棍
        // event.position 返回触发事件的坐标, 在这里触发事件的是玩家, 所以坐标自然是玩家的坐标
        // 获取玩家所在的灵气区块
        // 更多关于 IAuraChunk 的信息, 请看对应章节
        var auraChunk as IAuraChunk = world.getAuraChunk(event.position);

        // 获取玩家 4 格范围内灵气量最高的坐标, 如果找不到就返回玩家坐标
        var highestPos = world.getHighestSpot(event.position, 4, event.position);

        // 获取玩家 4 格范围内灵气量最低的坐标, 如果找不到就返回玩家坐标
        var lowestPos = world.getLowestSpot(event.position, 4, event.position);

        // 默认值为 0
        // 找寻玩家 4 格内的灵气点
        var spotAmount as int = world.getSpotAmountInArea(event.position, 4);
        print(spotAmount); // Example 这里打印的是 0, 因为使用情况不一, 所以每个人打印的结果也会不同, 这个结果仅供参考


        // 以下两个的默认值都为 1000000, 但第一个值的类型是 int, 第二个是 float
        // 玩家 4 格内的灵气量
        var auraTotal as int = world.getAuraInArea(event.position, 4);
        print(auraTotal); // 打印 : 1000000, 上同, 不解释

        var triangulateAura as int = world.triangulateAuraInArea(event.position, 4);
        print(triangulateAura); // 打印 : 1000000, 这个方法请自行测试
    }
});
```

# IAuraChunk

## Import

```csharp
import mods.randomtweaker.naturesaura.IAuraChunk;
```

## Static ZenMethod

| 方法名 | 返回值类型 | 方法描述 |
| :------ | ------ | ------ |
| drainAura(pos as IBlockPos, amount as int, aimForZero as bool, simulate as bool) | int | 消耗给定 pos 的灵气数量, 返回消耗的灵气 (`aimForZero` 为 `true` 时如果灵气被消耗至负数则返回值为消耗前的灵气量) |
| drainAura(pos as IBlockPos, amount as int) | int | 同上只不过后两个参数是 `false` |
| storeAura(pos as IBlockPos, amount as int, aimForZero as bool, simulate as bool) | int | 增加给定 pos 的灵气数量, 返回增加的灵气 (`aimForZero` 为 `true` 时如果灵气被增加至正数则返回值为增加前的灵气量) |
| storeAura(pos as IBlockPos, amount as int) | int | 同上只不过后两个参数为 `false` |
| getDrainSpot(pos as IBlockPos) | int | 返回 `pos` 的灵气量 |

## Example

```csharp
// 以下内容涉及事件, 不会事件请先学习事件
import crafttweaker.world.IWorld;
import crafttweaker.world.IBlockPos;
import crafttweaker.event.PlayerRightClickItemEvent; // 玩家右键物品事件
import mods.randomtweaker.naturesaura.IAuraChunk;

events.onPlayerRightClickItem(function(event as PlayerRightClickItemEvent) {
    var world as IWorld = event.world; // 获取触发事件的玩家所在的世界
    var pos as IBlockPos = event.position; // 获取玩家坐标

    if(!world.remote && <minecraft:stick>.matches(event.item)) { // 先确保在服务端执行代码, 再判断手上物品是否为木棍
        // event.position 返回触发事件的坐标, 在这里触发事件的是玩家, 所以坐标自然是玩家的坐标
        // 获取玩家所在的灵气区块
        var auraChunk as IAuraChunk = world.getAuraChunk(event.position);

        // 消耗 1w 灵气量于玩家坐标上
        auraChunk.drainAura(pos, 10000);

        // 添加 1w 灵气量于玩家坐标上
        auraChunk.storeAura(pos, 10000);

        // 获取玩家坐标的灵气量
        var amount as int = auraChunk.getDrainSpot(pos);
        print(amount); // 打印 0
    }
});
```

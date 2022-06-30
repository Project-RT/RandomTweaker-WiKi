# DynamicSpawnTable

此类决定具体存放的生成表, 需要在调用 `ICocoon.registerSpawn()` 时传入方法逻辑

## Import

```csharp
import mods.randomtweaker.botania.DynamicSpawnTable;
```

## 参数解析

返回一个生成表的名称

- `stack` as IItemStack 玩家右键或者随想之茧接触到的物品
- `player` as IPlayer 如果为玩家右键触发则不为 `null`, 反之
- `tile` as ICocoonTileEntity 随想之茧本身的一些数据

## Example

```csharp
function(stack, player, tile) {
    // 在此处你可以写任意逻辑决定返回哪些生成表
    return "你注册过的生成表的名称";
}
```

# Attunement Start Event

当共鸣开始时触发 (顺带一提, 这个事件是用来整活的!!)

这个事件实现了 [IEntityEvent](https://docs.blamejared.com/1.12/en/Vanilla/Events/Events/IEntityEvent), 所以 `IEntityEvent` 事件的可用 `Getter` 此事件也可使用

## Import

```csharp
import mods.randomtweaker.astralsorcery.AttunementStartEvent;
```

## ZenGetter

| Getter | 返回值类型 | Getter 描述 |
| :------ | ------ | ------ |
| world | IWorld | 返回共鸣祭坛所处世界 |
| constellation | string | 返回共鸣的星座 |
| entity (此为 `IEntityEvent` 的 `Getter`) | IEntity | 返回与共鸣祭坛共鸣的实体 (有可能是物品实体也有可能是生物) |

## ZenMethod

| 方法名 | 返回值类型 | 方法描述 |
| :------ | ------ | ------ |
| getWorld() | IWorld | 与 `world` Getter 一致 |
| getConstellation() | string | 与 `constellation` Getter 一致 |

## Example

```csharp
import crafttweaker.data.IData;
import crafttweaker.world.IWorld;
import crafttweaker.entity.IEntity;
import crafttweaker.item.IItemStack;
import crafttweaker.entity.IEntityItem;
import mods.randomtweaker.astralsorcery.AttunementStartEvent; // 共鸣祭坛开始共鸣事件

// 这个事件据目前定位来说, 只是为了整活
events.onAttunementStart(function(event as AttunementStartEvent) {
    var world as IWorld = event.world; // 获取共鸣祭坛所在的世界
    var entity as IEntity = event.entity; // 获取共鸣的实体
    var constellation as string = event.constellation; // 获取共鸣的星座

    // 保证实体为物品实体 (既然是物品实体, 那不是配方加上去的就是水晶石吧, 如果还有欢迎补充), 并判断共鸣的星座是否为非攻座
    if(!world.remote && entity instanceof IEntityItem && constellation.contains("discidia")) {
        var entityItem as IEntityItem = entity; // 强制转型为物品实体
        var item as IItemStack = entityItem.item; // 获取物品实体里的 "物品"

        // 判断是否为水晶石
        if(<astralsorcery:itemrockcrystalsimple>.matches(item)) {
            var nbt as IData = item.tag; // 拿到物品的 nbt

            // 判断非 null, 可能有些多余, 毕竟正常情况的水晶石都带这个 nbt
            if(!isNull(nbt.astralsorcery) && !isNull(nbt.astralsorcery.crystalProperties)) {
                nbt = nbt.astralsorcery.crystalProperties; // 不解释, 请看下一章里 Example 的解释

                // 经典判断非 null, 判断水晶石尺度是否大于等于 200
                if(!isNull(nbt.size) && nbt.size.asInt() >= 200) {
                    // 生成一个爆炸, 参数解释在 CrT 官方文档上有说明
                    world.performExplosion(null, entity.x, entity.y, entity.z, 1, false, false);
                }
            }
        }
    }
});
```

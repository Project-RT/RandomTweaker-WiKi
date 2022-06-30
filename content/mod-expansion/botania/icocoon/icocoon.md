# ICocoon

此类为随想之茧提供了自定义的生成生物的接口

## Import

```csharp
import mods.randomtweaker.botania.ICocoon;
```

## Static ZenMethod

| 方法名 | 返回值类型 | 方法描述 |
| :------ | ------ | ------ |
| getInstanceByStack(stack as IItemStack) | ICocoon | 通过生成表中的物品获取生成表 |

## ZenMethod

| 方法名 | 返回值类型 | 方法描述 |
| :------ | ------ | ------ |
| registerSpawn(name as string, stack as IItemStack, spawnTable as [double]IEntityDefinition, @Optional dynamicSpawnTab as DynamicSpawnTable) | ICocoon | 注册一个自定义的生成表 |
| getName() | string | 返回表的唯一名称 |

## Example

```csharp
// 首先是导包
import mods.randomtweaker.botania.ICocoon;

// 注册一个生成表
// test 即为生成表的名称
ICocoon.registerSpawn("test", <minecraft:iron_ingot>, {
    // 注意! 冒号后面的数字总和不能超过 1
    <entity:minecraft:wither_skeleton> : 1.0
}, function(stack, player, tile) {
    // 保证在服务端执行以下代码, 并排除非玩家右键情况
    if(!tile.world.remote && !isNull(player)) {
        // 更新随想之茧的 NBT 数据
        tile.updateData({test1 : "test1" as string});
        // 你也可以在此返回别的生成表的名称, 例如
        return "test1";
    }

    // 返回自身名称
    return "test";
});

// 注册第二个生成表
// 你也可以不填最后一个参数, 那是高级运用的轮子
ICocoon.registerSpawn("test1", <minecraft:coal:1>, {
    <entity:minecraft:zombie> : 0.5,
    <entity:minecraft:skeleton> : 0.5
});
```

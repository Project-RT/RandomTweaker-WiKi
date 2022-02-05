# Attunement Recipe Complete Event

当配方完成时被触发

此事件实现了 [IEventCancelable](https://docs.blamejared.com/1.12/en/Vanilla/Events/Events/IEventCancelable), 意味着 `IEventCancelable` 类可用方法在此事件中一样有效, 故可被取消, 取消后配方不输出物品

这个事件实现了 [IEntityEvent](https://docs.blamejared.com/1.12/en/Vanilla/Events/Events/IEntityEvent), 所以 `IEntityEvent` 事件的可用 `Getter` 此事件也可使用

## Import

```csharp
import mods.randomtweaker.astralsorcery.AttunementRecipeCompleteEvent;
```

## ZenGetter

| Getter | 返回值类型 | Getter 描述 |
| :------ | ------ | ------ |
| input | IItemStack | 返回在共鸣祭坛上触发配方的物品 |
| output | IItemStack | 返回配方输出的物品 |
| world | IWorld | 返回共鸣祭坛所在的世界 |
| constellation | string | 返回共鸣的星座 |
| entity (此为 `IEntityEvent` 的 `Getter`) | IEntity | 返回与共鸣祭坛共鸣的实体 |
| itemEntity | IEntityItem | 返回与共鸣祭坛共鸣的物品实体 |

## ZenSetter

| Setter | 传入值类型 | Setter 描述 |
| :------ | ------ | ------ |
| output | IItemStack | 设置配方输出的物品 |

## ZenMethod

| 方法名 | 返回值类型 | 方法描述 |
| :------ | ------ | ------ |
| getInput() | IItemStack | 与 `input` Getter 一致 |
| getOutput() | IItemStack | 与 `output` Getter 一致 |
| setOutput(output as IItemStack) | void | 与 `output` Setter 一致 |
| getWorld() | IWorld | 与 `world` Getter 一致 |
| getItemEntity() | IEntityItem | 与 `itemEntity` Getter 一致 |
| getConstellation() | string | 与 `constellation` Getter 一致 |
| getAdditionalOutput() | List\<IItemStack> (可当 [IItemStack] 处理) | 获取额外输出的物品 |
| addAdditionalOutput(additionalOutput as IItemStack) | void | 添加额外输出的物品 |

## Example

```csharp
import crafttweaker.data.IData;
import crafttweaker.world.IWorld;
import crafttweaker.item.IItemStack;
import crafttweaker.entity.IEntityItem;

import mods.randomtweaker.astralsorcery.AttunementAltar;
import mods.randomtweaker.astralsorcery.AttunementRecipeCompleteEvent; // 共鸣祭坛合成配方结束事件

// 注册配方
AttunementAltar.addRecipe(<minecraft:stick>.withAmount(2), <minecraft:dirt>, "astralsorcery.constellation.discidia"); // 指定共鸣非攻座
AttunementAltar.addRecipe(<minecraft:stick>, <minecraft:log>); // 注意这个没有填最后一个参数, 意味着无需指定共鸣某个星座

events.onAttunementRecipeComplete(function(event as AttunementRecipeCompleteEvent) {
    var world as IWorld = event.world; // 获取共鸣祭坛所在的世界
    var inputItem as IEntityItem = event.itemEntity; // 获取共鸣的物品实体, 此时可以拿 inputItem 的 nbt 做进一步操作

    if(!world.remote && <minecraft:stick>.matches(inputItem.item)) {// 先确保在服务端执行代码, 再判断共鸣的物品实体是否为木棍
        var output as IItemStack = event.output; // 获取到输出物品
        var constellation as string = event.constellation; // 获取共鸣的星座


        // 判断泥土是不是配方该输出的物品, 星座是否为非攻座, 这样第二个注册的配方就一定会被排除在外
        if(<minecraft:dirt>.matches(output) && constellation == "astralsorcery.constellation.discidia") {
            // 重设配方输出为 10 个木板
            event.setOutput(<minecraft:planks>.withAmount(10));

            // 添加额外的输出, 64 个石头
            event.addAdditionalOutput(<minecraft:stone>.withAmount(64));

            var nbt as IData = inputItem.nbt; // 拿到 nbt

            // 判断 nbt 里是否存在 ForgeData 这个 key, 如果不加判断, 可能会抛出错误, 比如经典的 NPE
            if(!isNull(nbt.ForgeData)) {
                nbt = nbt.ForgeData; // 重定向 nbt 的域到 ForgeData, 重定向后 nbt 变量指向 inputItem.nbt.ForgeData

                var special as IData = nbt.memberGet("special"); // 假设 inputItem 的 nbt 里有这个 key 和对应的 value

                // 排除 special 是 null 的情况, 后把 special 转成 bool 类型 (1 是 true, 0 是 false)
                if(!isNull(special) && special.asBool()) { 
                    // 如果有这个 key 且 value 为 1 (也就是 true)
                    // 就把输出更改为 64 个钻石块
                    // 一定要把另外一个 setOutput 方法放在前面, 要是在此行后面会被重设成 10 个木板
                    event.setOutput(<minecraft:diamond_block>.withAmount(64)); 
                }
            }

            // 取消事件, 取消过后上述代码都不再有效, 取消后会返还输入物品
            //event.cancel();
        }
    }
});
```

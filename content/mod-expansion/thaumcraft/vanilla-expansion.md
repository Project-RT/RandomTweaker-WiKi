# Vanilla Expansion

为 [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack) 类和 [IEntity](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntity) 类提供了扩展方法

这意味着 `IItemStack` 类实例和 `IEntity` 类实例可以使用这些方法

## Import

你完全没必要导包, 除非你想用类名调用扩展类方法

### IItemStack Expansion

```csharp
import mods.randomtweaker.thaumcraft.IItemStack;
```

### IEntity Expansion

```csharp
import mods.randomtweaker.thaumcraft.IEntity;
```

## Static ZenMethod

### IItemStack ZenMethod

| 方法名 | 返回值类型 | 方法描述 |
| :------ | ------ | ------ |
| getAspects() | string[] | 获取一个物品所具有的源质名称 |

### IEntity ZenMethod

| 方法名 | 返回值类型 | 方法描述 |
| :------ | ------ | ------ |
| getAspects() | string[] | 获取一个实体所具有的源质名称 |

## Example

```csharp
import crafttweaker.event.PlayerInteractEntityEvent; // 玩家与实体互动事件

// 这里先介绍获取物品源质名称的方法

for aspect in <minecraft:cobblestone>.getAspects() {
    print(aspect);
}

// 理论上, 这里在游戏启动时应该会打印圆石具有的源质名称
// 即打印 terra 和 perditio
// 但实际上, 什么都不会打印, 这是为什么?
// 在这里给出解释, 因为源质的注册在 PostInitialization 阶段, 此时 CrT 早已加载了脚本, 故 getAspects() 返回一个空数组
// 出于这个原因, 两个方法的使用场景就受到了限制
// 限制在 PostInitialization 阶段后这些方法才会返回一个内部元素不为空的数组
// 所以休想在游戏的生命周期事件内干什么好事

// 接下来为获取实体具有的源质名称的方法
// 涉及事件, 不会就去学(doge)

events.onPlayerInteractEntity(function(event as PlayerInteractEntityEvent) {
    if(!event.world.remote) { // 确保在服务端执行下列代码
        for aspect in event.target.getAspects() { // for 循环
            print(aspect);
            // 在只装有原版神秘的情况, 并且互动的实体是苦力怕, 那将打印
            // herba 和 ignis
            // 在这里, 因为这个事件是玩家与实体互动时触发的, 所以一定会在 PostInitialization 阶段后触发
            // 故返回一个内部元素不为空的数组
        }
    }
});
```

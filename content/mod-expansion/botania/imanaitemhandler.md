# IManaItemHandler

此类暴露了植魔的一些方法, 使得你可以向玩家需求魔力, 向玩家输出魔力等等

## Import

```csharp
import mods.randomtweaker.botania.IManaItemHandler;
```

## Static ZenMethod

| 方法名 | 返回值类型 | 方法描述 |
| :------ | ------ | ------ |
| getManaItems(player as IPlayer) | IItemStack[] | 返回玩家**背包**中可以容纳魔力的物品 |
| getManaBaubles(player as IPlayer) | IItemStack[int] | 返回玩家**饰品栏**中的**魔力物品**而不是魔力饰品, 其中 int 的值为物品所在的饰品格 |
| requestMana(stack as IItemStack, player as IPlayer, manaToGet as int, remove as bool) | int | `stack` 为提取魔力的物品, `player` 为被提取魔力的玩家, `manaToGet` 为提取需要的的魔力数量, `remove` 为是否不为模拟提取魔力, 返回实际减少的魔力数量 |
| requestManaExact(stack as IItemStack, player as IPlayer, manaToGet as int, remove as bool) | bool | 参数含义上同, 只有当魔力数量大于 `manaToGet` 才返回 `true` |
| requestManaForTool(stack as IItemStack, player as IPlayer, manaToGet as int, remove as bool) | int | 参数含义上同, 但会考虑魔力减免, 返回本应减少的魔力数量 |
| requestManaExactForTool(stack as IItemStack, player as IPlayer, manaToGet as int, remove as bool) | bool | 参数含义上同, 考虑魔力减免, 返回提取是否成功 |
| dispatchMana(stack as IItemStack, player as IPlayer, manaToSend as int, add as bool) | int | `stack` 为发送魔力的物品, `player` 为接收魔力的玩家, `manaToSend` 为发送的魔力, `add` 为是否真的发送, 返回实际发送的魔力数量 |
| dispatchManaExact(stack as IItemStack, player as IPlayer, manaToSend as int, add as bool) | bool | 参数含义上同, 只有当可容纳魔力数量大于等于 `manaToSend` 才返回 `true` |
| getFullDiscountForTools(player as IPlayer, tool as IItemStack) | float | 返回玩家的魔力减免, 会受 `tool` 参数的影响 |

## Example

```csharp
import crafttweaker.world.IWorld;
import crafttweaker.player.IPlayer;
import crafttweaker.item.IItemStack;
import crafttweaker.event.PlayerRightClickItemEvent; // 玩家右键物品事件
import mods.randomtweaker.botania.IManaItemHandler; // 想使用就必须导包

// 在这里默认环境里装有植物魔法 Mod (没装的给我说 Example 有问题我当场...)
events.onPlayerRightClickItem(function(event as PlayerRightClickItemEvent) {
    var player as IPlayer = event.player; // 获取触发事件的玩家
    var world as IWorld = event.world; // 获取触发事件的玩家所在的世界

    // 在 Example 里, 玩家饰品栏里有魔力之戒, 快捷栏第二格有魔力石板, 都是满魔力
    if(!world.remote && <minecraft:stick>.matches(event.item)) { // 先确保在服务端执行代码, 再判断手上物品是否为木棍
        // 先介绍 getFullDiscountForTools 方法
        // 此方法是获取玩家的魔力减免数值
        // 最后一个参数一般来说填的是正在提取魔力的物品 (题外话 : 在植魔原本的代码里没看到最后一个参数有什么运用)
        // 当然也可以填 null
        var discount as float = IManaItemHandler.getFullDiscountForTools(player, <minecraft:stick>);
        print(discount); // 没有穿上有魔力减免的装备为 0
        // 这里我穿了全套的泰拉杠套装, 打印 0.2

        // 获取玩家背包里的魔力容器 (更具体一点为实现了 IManaItem 类的物品)
        var manaItemInInventory as IItemStack[] = IManaItemHandler.getManaItems(player);

        for item in manaItemInInventory {
            print(item.commandString);
            // 打印 <botania:manatablet>.withTag({mana: 500000})
        }

        // 获取玩家饰品栏里的魔力物品
        var manaItemInBaubleInventory as IItemStack[int] = IManaItemHandler.getManaBaubles(player);

        for slot, item in manaItemInBaubleInventory {
            print("Slot : " + slot + ", item : " + item.commandString);
            // 打印 Slot : 1, item : <botania:manaring>.withTag({mana: 500000, playerHashcode: 90})
            // 注意这里的 Slot : 1, slot 是从 0 开始数的, 所以第二个格的 slot 是 1
        }

        // requestMana 方法
        // 这个方法会优先提取 manaToGet 值的数量, 不足就提取剩余魔力
        // 一般而言, stack 参数填的都是提取或者发送魔力的物品, 在代码中则为跳过该物品, 不进行判断
        // 以免发生自己扣自己魔力, 自己给自己魔力这种神奇操作
        // 假设我们右键一次木棍 (魔法棒), 最低消耗 80 魔力最高 100 魔力, 然后在玩家面前两格生成一只羊
        // 注意最后填的为 false, 意味着这是模拟提取魔力
        if(IManaItemHandler.requestMana(<minecraft:stick>, player, 100, false) >= 80) {
            // 注意这里填的为 true, 意味真实提取魔力
            // 代码运行到这你会发现背包中的魔力石板的魔力减少了 100
            // 对, 这个方法是优先检查背包里有无符合的魔力物品, 没有再去饰品栏里找
            // 以下操纵魔力的方法都是这个规则
            IManaItemHandler.requestMana(<minecraft:stick>, player, 100, true);

            // player.horizontalFacing 获取到玩家方向, getOffset 方法为坐标偏移方法
            // spawnEntity 为方便生成一个不需要自定义数据的实体的方法, 不需要先 create 个实体再 setPosition
            <entity:minecraft:sheep>.spawnEntity(world, event.position.getOffset(player.horizontalFacing, 2));
        }
        
        // requestManaExact 方法更为严格
        // 提取魔力的魔力容器里的魔力没有大于 manaToGet 的值就直接跳过, 如果背包和饰品栏一个符合条件的魔力容器都没有则返回 false
        // 返回 false 意味着提取失败, 不会扣除玩家身上的魔力
        // 最后的值一样填 false, 想知道玩家是否符合条件的时候都应该填 false
        // 以免误扣除玩家的魔力 (玩家 : 我...)
        // 精确扣除玩家 1w 魔力, 后发送一句话
        if(IManaItemHandler.requestManaExact(<minecraft:stick>, player, 10000, false)) {
            IManaItemHandler.requestManaExact(<minecraft:stick>, player, 10000, true);
            player.sendChat("你被骗了!");
        }

        // requestManaForTool 方法
        // 此方法会考虑魔力减免, 所以如果想要一个物品或者其他什么的消耗魔力考虑魔力减免
        // 就使用此方法
        // 上述例子中都有判断魔力足不足够, 其实不判断也行 (doge)
        // 不判断的话方法最好不用 Exact 的, 原因可以自己思考一下
        // 如果穿戴了全套泰拉套, 那就会减免 20% 的魔力, 也就是只需要 800 魔力了
        var requsetAmount as int = IManaItemHandler.requestManaForTool(<minecraft:stick>, player, 1000, true);
        print(requsetAmount); // 打印 1000, 如果魔力不足 1000, 则会打印 (剩余魔力 / (1 - 魔力减免百分比化小数))

        // requestManaExactForTool 方法与就是 requestManaExact 方法考虑魔力减免的版本
        IManaItemHandler.requestManaExactForTool(<minecraft:stick>, player, 10000, true);

        // dispatchMana 方法与 requestMana 类似
        // 当可容纳的魔力数量不足 manaToSend 的值时, 就会返回实际发送的魔力
        print(IManaItemHandler.dispatchMana(<minecraft:stick>, player, 10000, true));
        // 打印了 10000 代表了身上有剩余可容纳魔力大于 10000 的魔力容器 (这不废话吗, 上面的代码都消耗不止 1w 魔力)

        // dispatchManaExact 跟 requestManaExact 类似
        // 返回 false 意味着发送魔力失败
        print(IManaItemHandler.dispatchManaExact(<minecraft:stick>, player, 10000, true));
        // 只要有容量大于等于 1w 的魔力容器就会打印 true, 否则 false
    }
});
```

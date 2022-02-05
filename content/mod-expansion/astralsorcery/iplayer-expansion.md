# IPlayer Expansion

此类为 [IPlayer](https://docs.blamejared.com/1.12/en/Vanilla/Players/IPlayer) 类的扩展类, 这意味着 `IPlayer` 类实例可以直接使用此类的方法

此扩展类为 `CrT` 提供了一系列操作玩家星能力, 共鸣星座的方法

## Import

你完全没必要导这个包, 除非你想用类名调用扩展类方法

```csharp
import mods.randomtweaker.astralsorcery.IPlayer;
```

## Static ZenMethod

| 方法名 | 返回值类型 | 方法描述 |
| :------ | ------ | ------ |
| getPerkPercentToNextLevel() | float | 返回升级星能力等级所需经验与超出现等级经验的百分比 |
| getPerkLevel() | int | 返回当前星能力等级 |
| getPerkExp() | double | 返回当前星能力总经验 |
| getAttunedConstellation | string | 获取玩家共鸣星座名称 |
| getKnownConstellations() | List\<String> (可当成 [string] 处理) | 获取玩家已连线的星座名称 |
| getSeenConstellations() | List\<String> | 获取玩家已知星座名称 |
| modifyPerkExp(double exp) | bool | 添加玩家星能力经验 (如有共鸣星座则返回 `true`, 否则返回 `false`, `exp` 最大为 `(下一级等级容纳经验 - 当前等级容纳经验) * 0.08`) |
| setPerkExp(double exp) | bool | 上同, 只不过由添加变为设置 |

## Example

```csharp
// 以下内容涉及事件, 不会事件优先学习事件
import crafttweaker.world.IWorld;
import crafttweaker.player.IPlayer;
import crafttweaker.event.PlayerRightClickItemEvent; // 玩家右键物品事件

events.onPlayerRightClickItem(function(event as PlayerRightClickItemEvent) {
    var player as IPlayer = event.player; // 获取触发事件的玩家
    var world as IWorld = event.world; // 获取触发事件的玩家所在的世界

    if(!world.remote && <minecraft:stick>.matches(event.item)) { // 先确保在服务端执行代码, 再判断手上物品是否为木棍
        // 假设玩家刚共鸣的星座为非攻座
        // 实际上, 参数会在内部进行向下取整
        // 设置玩家星能力的经验为 158
        // 此方法仅在 !world.remote 环境下可使用
        player.setPerkExp(158);

        // 这个的结果其实跟拿着星芒宝典打开星能力章节后左上角 HUD 显示的数值一致
        var percent as float = player.getPerkPercentToNextLevel();
        print(percent); // 打印 0.0, 因为刚好升到第二级

        var level as int = player.getPerkLevel();
        print(level); // 打印 2, 因为升到了 2 级

        var exp as double = player.getPerkExp();
        print(exp); // 打印 158, 因为刚才 set 成了 158

        var constellation as string = player.getAttunedConstellation();
        print(constellation); // 打印 astralsorcery.constellation.discidia, 因为共鸣的星座为非攻座

        // 在这里, 我还解锁了解离座, 但未连线
        // 必须这样指定类型, 否则会报错
        // 获取已经连线的星座
        var knownConstellation as [string] = player.getKnownConstellations();
        
        for c in knownConstellation {
            print(c);
            // 打印 astralsorcery.constellation.discidia
        }

        // 指定类型原因如上
        var seenConstellation as [string] = player.getSeenConstellations();

        for c in seenConstellation {
            print(c);
            // 打印 astralsorcery.constellation.discidia
            // 和 astralsorcery.constellation.evorsio // 这个是解离座
        }
        
        // 在示例脚本里, 如果要验证此方法作用, 请把 setPerkExp 方法那行注释
        // 参数有最大限制, 所以填超大数值等级直接起飞的想法是不切实际的
        // 此方法仅在 !world.remote 环境下可使用
        player.modifyPerkExp(13); // 13 为 2 级到 3 级最大可填数值, 再大会被强制修改为 13
    }
});
```

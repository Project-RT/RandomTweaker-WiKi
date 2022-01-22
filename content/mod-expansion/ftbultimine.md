# FTB Ultimine

同样的, 此功能需要在配置文件中把 `B:AllowCrTControl` 改为 `true` 才可使用

此类为 [IPlayer](https://docs.blamejared.com/1.12/en/Vanilla/Players/IPlayer) 类的扩展类, 这意味着 `IPlayer` 类实例可以直接使用此类的方法

此功能为 `CrT` 提供了操纵连锁的接口, 现在 `CrT` 可以决定玩家能否连锁

## Import

你完全没必要导这个包, 除非你想用类名调用扩展类方法

```csharp
import mods.randomtweaker.ftbultimine.IPlayer;
```

## Static ZenMethod

| 方法名 | 方法作用 |
| :----- | ----- |
| setAllowFTBUltimine(flag as bool) | 决定玩家能否连锁 |

## Example

```csharp
// 以下内容涉及事件, 不会事件慎入或查看 https://youyi580.gitbook.io/zentutorial/advanced/event-overview 的内容初步了解事件
import crafttweaker.event.BlockBreakEvent; // 方块破坏事件

events.onBlockBreak(function(event as BlockBreakEvent) {
    if(!event.world.remote) { // 判断是否在服务端内
        event.player.setAllowFTBUltimine(false); // 阻止玩家连锁

        // 还有一个值得注意的是, 调用此方法后, 效果是永久的, 除非再次调用并传入 true, 否则该玩家永远无法连锁
    }
});
```

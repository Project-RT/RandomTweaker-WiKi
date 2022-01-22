# Dream Journl

同样的, 需要在配置文件把 `B:DreamJournal` 改为 `true` 才可启用此功能

此类为 [IPlayer](https://docs.blamejared.com/1.12/en/Vanilla/Players/IPlayer) 类的扩展类, 这意味着 `IPlayer` 类实例可以直接使用此类的方法

此类为修改异梦来源方式提供了接口

## Import

你完全没必要导这个包, 除非你想用类名调用扩展类方法

```csharp
import mods.randomtweaker.thaumcraft.IPlayer;
```

## Static ZenMethod

| 方法名| 方法作用 |
| :----- | ----- |
| giverDreamJournl() | 给予玩家一本异梦并发送一条本地化消息 |

## Example

```csharp
// 以下内容涉及事件, 不会事件慎入或查看 https://youyi580.gitbook.io/zentutorial/advanced/event-overview 的内容初步了解事件
import crafttweaker.event.PlayerRightClickItemEvent; // 玩家右键物品事件

events.onPlayerRightClickItem(function(event as PlayerRightClickItemEvent) {
    if(!event.world.remote && <minecraft:stick>.matches(event.item)) { // 判断是否在服务端并确认右键的物品是否为木棍
        event.player.giverDreamJournl();
        // 获取异梦并发送本地化信息, 本地化 key 为 got.dream
    }
});
```

如果你安装了 `RL` 并在 `oresources` 文件内准备好了 `zh_cn.lang` (`RL` 用法自行搜索)

在 `lang` 文件添加这一行

```lang
got.dream=自定义内容!
```

那么发送的消息不再是 `你从异梦中醒来。你快速记下了转瞬即逝的记忆` 而是 `自定义内容!`

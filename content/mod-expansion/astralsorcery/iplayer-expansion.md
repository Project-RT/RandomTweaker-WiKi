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
| getPerkExp() | int | 返回当前星能力总经验 |
| getAttunedConstellation | string | 获取玩家共鸣星座名称 |
| getKnownConstellations() | List\<String> (在 `zs` 里可看成 string[]) | 获取玩家已知星座名称 |
| getSeenConstellations() | List\<String> | 获取玩家当晚可观测星座名称 |
| modifyPerkExp(double exp) | bool | 修改玩家星能力经验 (如果有共鸣星座则返回 `true`, 否则返回 `false`) |
| setPerkExp(double exp) | bool | 上同, 只不过由修改变为设置 |

## Example

```csharp
// 以下内容涉及事件, 不会事件优先学习事件


```

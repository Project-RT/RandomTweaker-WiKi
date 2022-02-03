# Attunement Start Event

当共鸣开始时触发

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
| entity (此为 `IEntityEvent` 的 `Getter`) | IEntity | 与共鸣祭坛共鸣的实体 |

## ZenMethod

| 方法名 | 返回值类型 | 方法描述 |
| :------ | ------ | ------ |
| getWorld() | IWorld | 与 `world` Getter 一致 |
| getConstellation() | string | 与 `constellation` Getter 一致 |

## Example

```csharp

```

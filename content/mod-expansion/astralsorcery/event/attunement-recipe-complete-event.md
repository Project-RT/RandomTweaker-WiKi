# Attunement Recipe Complete Event

当配方完成时被触发

此事件实现了 [IEventCancelable](https://docs.blamejared.com/1.12/en/Vanilla/Events/Events/IEventCancelable), 意味着 `IEventCancelable` 类可用方法在此事件中一样有效, 故可被取消, 取消后配方不输出物品

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
| getConstellation() | string | 与 `constellation` Getter 一致 |
| getAdditionalOutput() | List\<IItemStack> (可当 IItemStack[] 处理) | 获取额外输出的物品 |
| addAdditionalOutput(additionalOutput as IItemStack) | void | 添加额外输出的物品 |

## Example

```csharp

```

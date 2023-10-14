# ISubTileEntityGenerating

因为 ISubTileEntityGenerating 类继承 SubTileEntity 类所以 SubTileEntity 所有可用的功能 ISubTileEntityGenerating 类都能用

## Import

```csharp
import mods.randomtweaker.cote.ISubTileEntityGenerating;
```

## ZenProperty

请看 SubTileEntity

| 字段 | 类型 | 描述 |
| :------ | ------ | ------ |
| PassiveFlower | bool | 是否为被动产魔花 | 
| valueForPassiveGeneration | int | 每 Tick 被动产出多少魔力 (受 canGeneratePassively 函数影响, 此函数返回 true 时主动产魔花就根据这个字段的值被动产魔, 无需在 onUpdate 函数写产魔轮子) | 
| delayBetweenPassiveGeneration | int | 每 Tick 被动产魔后的冷却时间 | 
| shouldSyncPassiveGeneration | bool | 被动产魔时是否同步 TileEntity | 

## Example

```csharp
#loader contenttweaker
import mods.contenttweaker.VanillaFactory;
import mods.randomtweaker.cote.ISubTileGenerating;

var subTileGenerating as ISubTileGenerating = VanillaFactory.createSubTileGenerating("test", 0xFFFFFF);
subTileGenerating.register();
```
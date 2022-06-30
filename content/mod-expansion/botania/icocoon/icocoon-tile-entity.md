# ICocoonTileEntity

此类为随想之茧扩展出来的接口, 为高级运用提供方法

## Import

```csharp
import mods.randomtweaker.botania.ICocoonTileEntity;
```

## ZenGetter

| Getter | 返回值类型 | 描述 |
| :------ | ------ | ------ |
| world | IWorld | 获取随想之茧所在世界 |
| pos | IBlockPos | 获取随想之茧方块坐标 |
| data | IData | 获取随想之茧的 `NBT` 数据 |

## ZenMethod

| 方法名 | 返回值类型 | 方法描述 |
| :------ | ------ | ------ |
| getIWorld() | IWorld | 与 `world Getter` 一致 |
| getIBlockPos() | IBlockPos | 与 `pos Getter` 一致 |
| getData() | IData | 与 `data Getter` 一致 |
| updateData(data as IData) | void | 更新随想之茧的 `NBT` 数据 |

## Example

请移步 [ICocoon#Example](icocoon#example)

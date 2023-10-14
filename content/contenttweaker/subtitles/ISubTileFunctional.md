# ISubTileFunctional

因为 ISubTileFunctional 类继承 SubTileEntity 类所以 SubTileEntity 所有可用的功能 ISubTileFunctional 类都能用

如果有小功能花, 记得在 resources/contenttweaker/textures/blocks 目录下存放一张单独的贴图给小功能花 (贴图名 : unlocalizedName +_chibi.png)

## Import

```csharp
import mods.randomtweaker.cote.ISubTileEntityFunctional;
```

## ZenProperty

请看 SubTileEntity

| 字段 | 类型 | 描述 |
| :------ | ------ | ------ |
| hasMini | bool | 是否创建小型功能花 |
| miniRange | int | 小型功能花的工作范围 |

## Example

```csharp
#loader contenttweaker
import mods.contenttweaker.VanillaFactory;
import mods.randomtweaker.cote.ISubTileFunctional;

var subTileFunctional as ISubTileFunctional = VanillaFactory.createSubTileFunctional("test_1", 0xFFFFFF);
subTileFunctional.register();
```
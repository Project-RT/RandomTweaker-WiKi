# SubTileEntity

同时安装了 BoT 和 CoT 时可以使 CoT 可以自定义产魔或者功能花

CrT 获取不到这个类, 只能获取到它的子类

记得在 resources/contenttweaker/textures/blocks 目录下存放自定义花的贴图 (贴图名 : unlocalizedName.png)

这个类主要让代码方便维护

想创建产魔花请看 ISubTileGenerating

想创建功能花请看 ISubTileFunctional

## Import

```csharp
import mods.randomtweaker.cote.SubTileEntity;
```
## ZenProperty

| 字段 | 类型 | 描述 |
| :------- | ------- | ------- |
|unlocalizedName | string | 注册名 | 
|range | int | 自定义花的工作范围 | 
|color | int | 自定义花的魔力条颜色 | 
|maxMana | int | 最大魔力容量 | 
|acceptsRedstone | bool | 是否接受红石信号 | 
|overgrowthAffected | bool | 是否受蕴魔土的影响 | 

## 本地化

tile.botania:flower.自定义花的名字.name = 本地化自定义花的名字

tile.botania:flower.自定义花的名字.reference = 本地化自定义花的 tooltip

## Example

```csharp
import mods.contenttweaker.VanillaFactory;
import mods.randomtweaker.cote.ISubTileEntityGenerating;
import mods.randomtweaker.cote.ISubTileEntityFunctional;

//产魔花
var test_flower0 as ISubTileEntityGenerating = VanillaFactory.createSubTileGenerating("test_flower0", 0xFFFFFF);
test_flower0.maxMana = 2000;
test_flower0.onUpdate = function(subtile, world, pos) {
    if(!world.remote) {
        if(isNull(subtile.data.time))
            subtile.updateCustomData({time : 0});

        if(!isNull(subtile.data.time)) {
            subtile.updateCustomData({time : subtile.data.time.asInt() + 1});
            if(subtile.data.time.asInt() == 100){
                server.commandManager.executeCommand(server, "dididididididididi~~~");
            }
        }
    }
};
test_flower0.register();

//功能花
var test_flower1 as ISubTileFunctional = VanillaFactory.createSubTileFunctional("test_flower1", 0x000000);
test_flower1.maxMana = 100086;
test_flower1.onUpdate = function(subtile, world, pos) {
    if(!world.remote) {
        if(isNull(subtile.data.time))
            subtile.updateCustomData({time : 0});

        if(!isNull(subtile.data.time)) {
            subtile.updateCustomData({time : subtile.data.time.asInt() + 1});
            if(subtile.data.time.asInt() == 100){
                server.commandManager.executeCommand(server, "dididididididididi~~~");
            }
        }
    }
};
test_flower1.register();
```
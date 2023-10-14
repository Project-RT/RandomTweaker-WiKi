# Function

自定义花能用的函数

## onBlockAdded
当自定义花被添加到世界上时调用

导包

```csharp
import mods.randomtweaker.cote.BlockAdded;
```

world as IWorld 自定义花所在世界

pos as IBlockPos 自定义花所在坐标

state as IBlockState 自定义花的方块状态

```csharp
subTileEntityObj.onBlockAdded = function(world, pos, state) {

};
```
## canSelect
森林法杖是否可以选择此自定义花并绑定到方块上

需要返回一个 bool

导包
```csharp
import mods.randomtweaker.cote.CanSelect;
```
player as ICTPlayer 玩家

wand as IItemStack 玩家手持的法杖

pos as IBlockPos 自定义花的坐标

side as IFacing 自定义花面对你的方向

```csharp
subTileEntityObj.canSelect = function(player, wand, pos, side) {
    return true;
};
```
## onBlockPlaceBy
当自定义花被一个实体放置在世界时调用

导包
```csharp
import mods.randomtweaker.cote.BlockPlacedBy;
```
world as IWorld 自定义花所在世界

pos as IBlockPos 自定义花的坐标

state as IBlockState 自定义花的方块状态

entity as IEntityLivingBase 放置自定义花的实体

stack as IItemStack 手上的物品 ( 也就是你放下的那朵自定义花)

```csharp
subTileEntityObj.onBlockPlaceBy = function(world, pos, state, entity, stack) {

};
```
## onUpdate
每 Tick 都会调用

导包
```csharp
import mods.randomtweaker.cote.Update;
```
subtile as SubTileEntityInGame 自定义花的 TileEntity

world as IWorld 自定义花所在的世界

pos as IBlockPos 自定义花的坐标

```csharp
subTileEntityObj.onUpdate = function(subtile, world, pos) {

};
```
## onBlockHarvested
当自定义花被挖掘完时调用

导包
```csharp
import mods.randomtweaker.cote.BlockHarvested;
```
world as IWorld 自定义花所在的世界

pos as IBlockPos 自定义花的坐标

state as IBlockState 自定义花的方块状态

player as ICTPlayer 挖掘自定义花的玩家

```csharp
subTileEntityObj.onBlockHarvested = function(world, pos, state, player) {

};
```
## onBlockActivated
当玩家右键自定义花时调用

需要返回一个 bool

导包
```csharp
import mods.randomtweaker.cote.BlockActivated;
```
world as IWorld 自定义花所在的世界

pos as IBlockPos 自定义花的坐标

state as IBlockState 自定义花的方块状态

player as ICTPlayer 右键自定义花的玩家

hand as Hand 右键自定义花的玩家的手

side as IFacing 玩家的方向

hitX as float 玩家跟自定义花的相对坐标

hitY as float 玩家跟自定义花的相对坐标

hitZ as float 玩家跟自定义花的相对坐标

```csharp
subTileEntityObj.onBlockActivated = function(world, pos, state, player, hand, side, hitX, hitY, hitZ) {
    if(<botania:twigwand>.matches(player.getHeldItem(hand))) {
        return false;
    }
    return true;
};
```
## canGeneratePassively
自定义花是否被动产能 (仅 ISubTileGenerating 类具有此函数)

导包
```csharp
import mods.randomtweaker.cote.CanGeneratePassively;
```
pos as IBlockPos 自定义花的坐标

world as IWorld 自定义花所在的世界

```csharp
subTileGeneratingObj.canGeneratePassively = function(pos, world) {

};
```
## populateDropStackNBTs
决定挖掘完自定义花的掉落物 (仅 ISubTileGenerating) 类具有此函数

导包
```csharp
import mods.randomtweaker.cote.PopulateDropStackNBTs;
```

drops as IItemStack[] 掉落物列表

```csharp
subTileGeneratingObj.populateDropStackNBTs = function(drops) {

};
```
# IPotion

使用cot来自定义药水效果

## Import

```csharp
import mods.randomtweaker.cote.IPotion;
```

## ZenProperty

| 字段 | 类型 | 描述 |
| :------- | ------- | ------- |
| instant | bool | 药水效果是即刻生效的还是持续生效的 (true 为即刻, false 为持续) |
| badEffectIn | bool | 药水效果是否为不好的效果 |
| beneficial | bool | 药水效果是否对玩家有益, 有益的药水会放在第一格 |
| shouldRender | bool | 药水效果是否在背包栏渲染 |
| shouldRenderHUD | bool | 药水效果是否在 HUD (在右上角) 渲染 |


## Function

| Function |  函数描述 |
| :------- |  ------- |
| isReady |  决定当前 Tick 是否触发 performEffect 函数 |
| performEffect |  此函数每 Tick 都会调用 |
| affectEntity |  此函数仅 Potion 的 instant 为 true 时触发 |

## VanillaFactory

```csharp
    var potion as IPotion = VanillaFactory.createPotion(unlocalizedName as string, liquidColorIn as int);
    /*
    unlocalizedName为注册名，不可重复! 类型为string(不要傻傻的填 unlocalizedName)
    liquidColorIn为药水颜色，例如0xF7D575
    贴图位置 : contenttweaker:textures/gui/unlocalizedName.png
    */
```

## Example

```csharp
#loader contenttweaker
 
import mods.contenttweaker.VanillaFactory;
import mods.randomtweaker.cote.IPotion;
import mods.contenttweaker.Player;
 
var potion as IPotion = VanillaFactory.createPotion("lhhd", 0xF7D575);
//贴图位置 : contenttweaker:textures/gui/(此处填药水注册id，事例中就该填lhhd).png
potion.shouldRender = false;
potion.shouldRenderHUD = false;
potion.badEffectIn = false;
potion.isReady = function(duration, amplifier) {
    if (duration % 20 == 0) {
        /*
        意思为20t触发一次(20t为一秒)
        也可以:
        return duration % 20 == 0
        */
        return true;
    }
        return false;
};
potion.performEffect = function(living, amplifier) {
    if(!living.world.remote && living instanceof Player) {
        var player as Player = living;
        player.sendChat("didiidid~~~");
    }
};
/*
living 类型为 IEntityLivingBase 意为具有此药水效果的生命实体
amplifier为药水等级(int)，药水等级最低为0
*/
potion.register();
```

# Custom JEI

## Import

```csharp
import mods.jei.JEI;
```

## Static ZenMethod

| 方法名| 返回值类型| 方法作用 |
| :------ | ------ | ------ |
| createJei(uid as string, title as string)| IJeiPanel | 创建jei界面 |
| createJeiRecipe(uid as string)| IJeiRecipe | 创建jei配方 |


## Example

JEI界面的创建与配方的添加

```csharp

import mods.jei.JEI;
import mods.randomtweaker.jei.IJeiPanel;
import mods.randomtweaker.jei.IJeiUtils;
import mods.randomtweaker.jei.IJeiRecipe;


//创建jei界面
var keyJEI as IJeiPanel = JEI.createJei("test_jei", "key");
//很明显uid不能重复(也不能与现有的重复)
keyJEI.setModid("www");
//设置显示的模组id
keyJEI.setBackground(IJeiUtils.createBackground(150, 50));
//设置一个界面的大小
keyJEI.addRecipeCatalyst(<minecraft:stone:3>);
keyJEI.addRecipeCatalyst(<minecraft:stone:1>);
//jei界面左边的显示
//比如对着熔炉按u会跳转到熔炉烧炼的界面
//对上面添加的物品按u也会跳转到这个界面
keyJEI.addSlot(IJeiUtils.createItemSlot(16, 18, true));
keyJEI.addSlot(IJeiUtils.createItemSlot(80, 18, false));
//增加物品格子(当然也可以增加流体)
keyJEI.addElement(IJeiUtils.createFontInfoElement("font", 50, 50,  0x000000));
keyJEI.addElement(IJeiUtils.createFontInfoElement("fontInfo", 100, 18, 0x52575B));
//增加描述
keyJEI.register();
//注册

//创建jei配方
var test_recipe as IJeiRecipe = JEI.createJeiRecipe("test_jei");
//这个uid就是你要将这个配方添加到的界面的uid
test_recipe.addInput(<minecraft:apple>);
//增加输入
test_recipe.addOutput(<minecraft:golden_apple:1>);
//增加输出
test_recipe.build();
//注册
```
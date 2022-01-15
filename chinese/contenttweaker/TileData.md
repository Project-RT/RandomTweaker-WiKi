# TileData

此类主要用于管理自定义植魔花内部的 `NBT` 数据

## Import

如果你想要声明变量或数组为此类型, 务必导包

```zenscript
import mods.randomtweaker.utils.ITileData;
```

## ZenGetter

| Getter | 返回值类型 | 返回值描述 |
| :------- | ------- | ------- |
| data | IData | 返回存储的数据 |

## ZenSetter

| Setter | Setter 值类型 | Setter 功能描述 |
| :--------- | --------- | --------- |
| data | IData | 更改存储的数据 |

## Example

```zenscript
//TileDataObj 在这里代表 TileData 类实例

TileDataObj.data = {"test" : "testValue" as string};
TileDataObj.data = {"testTwo" : {"testThree" : "testValue"}};

print(TileDataObj.data.asString());
// 会输出
/* {
    test:testValue,
    testTwo : {
        testThree:testValue
    }
} */
```

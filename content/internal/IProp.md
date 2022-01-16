# IProp

此功能需在配置文件中将 `B:Prop` 修改为 `true` 才可使用

此功能为 `CraftTweaker` 提供了一种全局 (可跨存档) 的数据存储方式, 由键值 (key-value) 对应存储, 其保存的位置位于 `.minecraft/rt.properties`

## Import

如果你想使用此功能, 务必导包

```csharp
import mods.randomtweaker.file.IProp;
```

## Static ZenMethod

| 方法名 | 返回值类型 | 方法作用 |
| :---------- | :---------- | :---------- |
| write(key as string, value as string) | `void` | 将 `value` 写入文件并以 `key` 为其键 |
| read(key as string) | `string` | 返回通过 `key` 拿到的 `value` |
| getAllKeys() | `string[]` | 返回文件中所有的 `key` |

## Example

```csharp
import mods.randomtweaker.file.IProp;

IProp.write("test", "testValue");
print(IProp.read("test")); // 会打印 testValue
print(IProp.getAllKeys()[0]); // 会打印 test

// 即使下次启动游戏时上述代码被删除了, rt.properties 的内容也不会被改变
```

此时你的 `rt.properties` 应该是这样的

```csharp
test=testValue
```

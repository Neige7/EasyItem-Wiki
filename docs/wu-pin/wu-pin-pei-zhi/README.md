# 物品配置

## 路径

所有物品配置文件应存放于`plugins/EasyItem/Items`文件夹

重复 ID 的物品仍然会被加载，但可能互相覆盖

最后哪个物品活下来。。。随缘了属于是

## 配置

详见[默认配置](kai-shi/mo-ren-pei-zhi.md)

## 编写你的物品

### /ei save是万物起源

遇事不决，/ei save。如果不行，就/ei cover。这是最简单最便捷的快速生成物品配置的方法

[物品保存指令](zhi-ling/wu-pin-bao-cun?id=save)

[物品覆盖指令](zhi-ling/wu-pin-bao-cun?id=cover)

### ID

所有物品都应该有一个ID，如下格式：

```
物品ID:
  # 具体的配置项, 以物品材质为例
  material: STONE
```

### 材质

即，物品是石头还是木头还是钻石剑

```
物品1:
  # 这个物品是石头
  material: STONE
物品2:
  # 这个物品是钻石
  material: DIAMOND
```

ID都有哪些，见下方链接

https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Material.html

如果你看着 ID 不知道它对应什么物品。。。

一般来讲，你可以在游戏中同时按下 F3+H，启用高级显示框，这样物品下方就会出现对应的ID。

![](_images/%E9%AB%98%E7%BA%A7%E6%8F%90%E7%A4%BA%E6%A1%86.png)

如上图所示，`minecraft:stone` 对应 `STONE`

对于 mod 物品，前缀不能省略。

比如一个名称为`mod:test`的物品，对应的 ID 应为 `MOD_TEST`

但是啊但是，你有没有看上面啊？

/ei save是万物起源。别搁这儿看ID了，保存一下什么都有了，看个锤子看。

### 物品名

具体配置如下

```
有名字的铁剑:
  material: IRON_SWORD
  name: 我有名字
```

### 非法物品名

该配置项在生成物品时将覆盖name项，具体配置如下

```
有名字的铁剑:
  material: IRON_SWORD
  illegalName: '{"italic":false,"color":"white","text":"玉米饼"}'
```

?> 众所周知，高版本的name和lore在nbt里其实是以一段json的形式存在的。
<br />本来这没什么，他这么做，你接受就好了。
<br />但他妈的总有一些傻逼插件能给你整出点活儿。
<br />比如上面那个就是某MMOItems干的，上面那一段非法物品名的合法形式应该是：
<br />{"extra":[{"bold":false,"italic":false,"underlined":false,"strikethrough":false,"obfuscated":false,"color":"white","text":"玉米饼"}],"text":""}
<br />这导致EasyItem无法以更可读的形式无损保存物品，只能将它原版的傻逼德行记录下来。
<br />但是这无伤大雅，如果你准备修改它，那你也就不需要让他与原先的物品完全一致了。
<br />直接使用name配置项吧。

### 物品Lore

具体配置如下

```
有Lore的铁剑:
  material: IRON_SWORD
  lore:
  - 我有lore
  - 我真有lore
  - 信我
```

你可以通过换行符`\n`换行, 在一行中书写多行lore

值得一提的是, 在yaml语法中, 双引号包裹的`"\n"`才代表换行符

单引号包裹的`'\n'`只代表一段形似`\n`的字符

例:

```
有Lore的铁剑:
  material: IRON_SWORD
  lore:
  - "我有lore\n我真有lore\n信我"
```

### 非法Lore

该配置项在生成物品时将覆盖lore项，具体配置如下

```
有Lore的铁剑:
  material: IRON_SWORD
  illegalLore:
  - '{"italic":false,"extra":[{"strikethrough":true,"color":"dark_gray","text":"------"},{"color":"gray","text":"[
    "},{"bold":true,"color":"aqua","text":"通用 "},{"color":"gray","text":"]"},{"strikethrough":true,"color":"dark_gray","text":"------"}],"text":""}'
```

?> 众所周知，高版本的name和lore在nbt里其实是以一段json的形式存在的。
<br />本来这没什么，他这么做，你接受就好了。
<br />但他妈的总有一些傻逼插件能给你整出点活儿。
<br />比如上面那个就是某MMOItems干的，上面那一段非法Lore的合法形式应该是：
<br />{"extra":[{"bold":false,"italic":false,"underlined":false,"strikethrough":true,"obfuscated":false,"color":"dark_gray","text":"------"},{"italic":false,"strikethrough":false,"color":"gray","text":"[                     [20:56:46 INFO]:     "},{"bold":true,"italic":false,"color":"aqua","text":"通用 "},{"bold":false,"italic":false,"color":"gray","text":"]"},{"italic":false,"strikethrough":true,"color":"dark_gray","text":"------"}],"text":""}
<br />这导致EasyItem无法以更可读的形式无损保存物品，只能将它原版的傻逼德行记录下来。
<br />但是这无伤大雅，如果你准备修改它，那你也就不需要让他与原先的物品完全一致了。
<br />直接使用lore配置项吧。

### 子ID/损伤值

在 1.12.2 及以下的版本中，某些物品存在“子ID”。

比如 WOOL 是白色羊毛，而子ID为 1 的 WOOL 是橙色羊毛。

![](_images/%E5%AD%90ID.png)

对应配置方法如下

```
白色羊毛:
  material: WOOL
橙色羊毛:
  material: WOOL
  # 子ID为1
  damage: 1
```

而对于有耐久的物品，damage对应损伤值，即，物品消耗了几点耐久。

```
铁剑:
  material: IRON_SWORD
用了一下的铁剑:
  material: IRON_SWORD
  # 消耗了1点耐久
  damage: 1
```

### CustomModelData

对于 1.14+ 的服务器，物品有了一个新的属性，CustomModelData。

一般人们用它搭配材质包制作自定义材质物品。

对应配置方法如下

```
铁剑:
  material: IRON_SWORD
  # CustomModelData 为 1
  custommodeldata: 1
```

### 附魔

附魔名称列表，应前往以下链接查看

https://hub.spigotmc.org/javadocs/spigot/org/bukkit/enchantments/Enchantment.html

具体配置方法如下

```
有附魔的铁剑:
  material: IRON_SWORD
  enchantments:
    # 锋利5
    DAMAGE_ALL: 5
```

啥？你说全是英文你根本看不懂哪个对哪个？

/ei save干什么用的

### 无法破坏

具体配置如下

```
无法破坏的铁剑:
  material: IRON_SWORD
  unbreakable: true
```

### 隐藏属性

有的物品明明无法破坏，物品信息里却看不到。

有的物品明明有附魔，物品信息里却看不到。

具体配置方法如下

```
啥都看不到的铁剑:
  material: IRON_SWORD
  hideflags:
  # 隐藏物品属性
  - HIDE_ATTRIBUTES
  # 隐藏物品可破坏方块
  - HIDE_DESTROYS
  # 隐藏物品染料颜色
  - HIDE_DYE
  # 隐藏物品附魔
  - HIDE_ENCHANTS
  # 隐藏物品可放置方块
  - HIDE_PLACED_ON
  # 隐藏物品药水效果
  - HIDE_POTION_EFFECTS
  # 隐藏物品无法破坏
  - HIDE_UNBREAKABLE
```

### 物品颜色

药水和皮革护甲可以拥有自定义颜色，具体配置方法如下

```
有颜色的皮革头盔1:
  material: LEATHER_HELMET
  color: 'ABCDEF'
有颜色的皮革头盔2:
  material: LEATHER_HELMET
  color: 666666
```

如上所示，你可以用十进制和十六进制两种方式配置物品颜色。

如果你想要以十进制表示颜色，那么color必须配置一个数字（不被引号包裹）

如果你想要以十六进制表示颜色，那么color必须是一个字符串（被引号包裹）

比如，`color: '666666'` 表示的是十六进制，等价于 `color: 6710886`

### 自定义NBT

许多插件会向物品中插入一些自定义NBT，用来记录某些信息。

NeigeItems也允许你这样做。

你可以通过插入自定义NBT，兼容一些基于NBT的插件，比如

```
超猛镐子:
  material: IRON_PICKAXE
  nbt:
    MMOITEMS_ATTACK_DAMAGE: (Double) 1000000
```

如果你装了MMOItems，那这个镐子现在应该有100万攻击力了。

你可能注意到，1000000前面有一个`(Double) `。

这个前缀代表，生成这条NBT的时候，会以 Double 类型生成（写的时候不要忘记括号后面的空格）。

如果你不写的话，生成时这条NBT很有可能就变成了Int类型或者Long类型。

这种用于转换类型的前缀应该应用于数值类型的NBT

具体有以下类型可以选择

```
# Byte 类型的 1
(Byte) 1
# Short 类型的 1
(Short) 1
# Int 类型的 1
(Int) 1
# Long 类型的 1
(Long) 1
# Float 类型的 1
(Float) 1
# Double 类型的 1
(Double) 1
```

使用类型转换前缀，一定要加空格

但是啊但是，别搁这儿看了，你直接/ei save一下，自动就都出来了。

### 模板继承

你可以让一个配置继承其他配置的部分或全部内容

具体内容请查看[模板继承](wu-pin/wu-pin-pei-zhi/mo-ban-ji-cheng.md)

### 节点

私有节点应直接配置与物品下方，比如

```
测试铁剑:
  material: IRON_SWORD
  name: <test>
  sections:
    test: 测试内容
```

有关私有节点的各个类型，具体请查看[私有节点](jie-dian/si-you-jie-dian.md)

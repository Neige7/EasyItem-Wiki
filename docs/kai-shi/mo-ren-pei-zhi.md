# 默认配置

## config.yml

```
Main:
  MMItemsPath: MMItems.yml
  Debug: false
Messages:
  invalidPlayer: §e[EI] §6玩家不在线或不存在
  successInfo: §e[EI] §6成功给予 §f{player} §a{amount} §6个 §f{name}
  givenInfo: §e[EI] §6你得到了 §a{amount} §6个 §f{name}
  dropSuccessInfo: §e[EI] §6成功在 §a{world} §6的 §a{x},{y},{z} §6掉落了 §a{amount} §6个 §f{name}
  unknownItem: §e[EI] §6找不到ID为 §a{itemID} §6的物品
  existedKey: §e[EI] §6已存在ID为 §a{itemID} §6的物品
  onlyPlayer: §e[EI] §6该指令仅可玩家使用
  successSaveInfo: §e[EI] §6成功将 §f{name} §6以ID §a{itemID} §6保存至 §a{path}
  mmImportSuccessInfo: §e[EI] §6成功将所有MM物品保存至 §a{path}
  airItem: §e[EI] §6请不要试图保存空气, 谢谢合作
  invalidAmount: §e[EI] §6无效数字
  invalidWorld: §e[EI] §6无效世界
  invalidLocation: §e[EI] §6无效坐标
  insufficientPermissions: §e[EI] §6权限不足
  reloadedMessage: §e[EI] §6重载完毕
  invalidNBT: §6[EI] §cNBT加载失败, 请勿在列表型NBT中混用键值对, 数字及字符串
  invalidItem: '§6[EI] §c物品加载失败, 物品可能缺损数据, 物品ID: §6{itemID}'
  failureInfo: '§e[EI] §6物品给予失败, 可能原因: 物品未配置材质/玩家已下线'
  invalidMaterial: '§e[EI] §6物品 {itemID} 使用了未知的材质 {material}'
  clickGiveMessage: §e点击获取该物品
Help:
  prefix: |-
    §6====================§eEasyItems§6====================
    §6==================[]为必填, ()为选填==================
  suffix: §6================<< §e{prev} §f{current}§e/§f{total} §e{next} §6>>================
  amount: 10
  format: "{command} §7> {description}"
  prev: 上一页
  next: 下一页
  commands:
    list:
      command: §e/ei §flist (页码)
      description: 查看所有EI物品
    get:
      command: §e/ei §fget [物品ID] (数量)
      description: 根据ID获取EI物品
    give:
      command: §e/ei §fgive [玩家ID] [物品ID] (数量)
      description: 根据ID给予EI物品
    giveAll:
      command: §e/ei §fgiveAll [物品ID] (数量)
      description: 根据ID给予所有人EI物品
    drop:
      command: §e/ei §fdrop [物品ID] [数量] [世界名] [X坐标] [Y坐标] [Z坐标]
      description: 于指定位置掉落EI物品
    save:
      command: §e/ei §fsave [物品ID] (保存路径)
      description: 将手中物品以对应ID保存至对应路径
    cover:
      command: §e/ei §fcover [物品ID] (保存路径)
      description: 将手中物品以对应ID覆盖至对应路径
    mm load:
      command: §e/ei §fmm load [物品ID] (保存路径)
      description: 将对应ID的MM物品保存为EI物品
    mm cover:
      command: §e/ei §fmm cover [物品ID] (保存路径)
      description: 将对应ID的MM物品覆盖为EI物品
    mm loadAll:
      command: §e/ei §fmm loadAll (保存路径)
      description: 将全部MM物品转化为EI物品
    reload:
      command: §e/ei §freload
      description: 重新加载EI物品
    help:
      command: §e/ei §fhelp
      description: 查看帮助信息
ItemList:
  Prefix: §6===========§eEasyItems§6===========
  Suffix: §6======<< §e{prev} §f{current}§e/§f{total} §e{next} §6>>======
  ItemAmount: 10
  ItemFormat: §6{index}. §a{ID} §6- §f{name}
  Prev: 上一页
  Next: 下一页
```

## Items/ExampleItem.yml

```
ExampleItem:
  # 物品材质
  material: LEATHER_HELMET
  # 物品CustomModelData(适用于1.14+)
  custommodeldata: 1
  # 物品损伤值
  damage: 1
  # 物品名
  name: §6一件皮革甲
  # 物品Lore
  lore:
  - '简单节点测试: <easyTest>'
  - '快速计算测试: <calcTest>'
  - '文本中小于号请添加反斜杠, 防止错误识别'
  - '形如: \<\<\<\>\>\>'
  - "换行符测试\n换行符测试"
  # 物品附魔
  enchantments:
    ARROW_DAMAGE: 1
    ARROW_KNOCKBACK: 1
  # 物品隐藏标识
  hideflags:
  - HIDE_ATTRIBUTES
  - HIDE_DESTROYS
  # 物品颜色(适用于药水/皮革装备)
  color: 65535
  # 物品NBT
  nbt:
    # 可以在NBT中编辑物品的原版属性
    AttributeModifiers:
    - Amount: 10
      AttributeName: minecraft:generic.max_health
      Operation: 0
      UUID:
      - 0
      - 31453
      - 0
      - 59664
      Name: generic.maxHealth
  # 物品私有节点
  sections:
    easyTest: 简单节点测试
    calcTest:
      type: fastcalc
      formula: 1+2+3
      min: 1
      max: 100
      fixed: 3

GradientTest:
  material: STONE
  lore:
    - <test1>
    - <test2>
  sections:
    test1: <gradient::000000_FFFFFF_1_---------->
    test2:
      type: gradient
      colorStart: 000000
      colorEnd: FFFFFF
      step: 1
      text: ----------

# 一个测试模板
template1:
  material: IRON_SWORD
  lore:
  - "&e攻击伤害: &f<damage>"
  nbt:
    MMOITEMS_ATTACK_DAMAGE: (Double) <damage>
# 一个测试模板
template2:
  material: DIAMOND_SWORD

# 一个全局继承测试, 它继承了"template1"的所有内容
TemplateItem1:
  inherit: template1
  name: §f物品继承测试
  sections:
    damage: 100
# 一个部分继承测试, 它继承了"template1"的lore, 以及"template2"的material
TemplateItem2:
  inherit: 
    lore: template1
    material: template2
  name: §f物品继承测试
  sections:
    damage: 100
# 一个顺序继承测试, 它将按顺序进行节点继承. 先继承"template1"的所有内容，再继承"template2"的所有内容
TemplateItem3:
  inherit:
  - template1
  - template2
  name: §f物品继承测试
  sections:
    damage: 100

# join节点测试
JoinTest1:
  material: STONE
  lore:
    # 结果: 1, 2, 3, 4, 5
    - 'join节点: <test>'
  sections:
    test:
      type: join
      # 待操作的列表
      list:
        - 1
        - 2
        - 3
        - 4
        - 5
JoinTest2:
  material: STONE
  lore:
    # 结果: 1-2-3-4-5
    - 'join节点: <test>'
  sections:
    test:
      type: join
      list:
        - 1
        - 2
        - 3
        - 4
        - 5
      # 分隔符(默认为", )
      separator: "-"
JoinTest3:
  material: STONE
  lore:
    # 结果: <1, 2, 3, 4, 5>
    - 'join节点: <test>'
  sections:
    test:
      type: join
      list:
        - 1
        - 2
        - 3
        - 4
        - 5
      # 前缀
      prefix: "<"
      # 后缀
      postfix: ">"
JoinTest4:
  material: STONE
  lore:
    # 结果: 1, 2, 3
    - 'join节点: <test>'
  sections:
    test:
      type: join
      list:
        - 1
        - 2
        - 3
        - 4
        - 5
      # 限制长度
      limit: 3
JoinTest5:
  material: STONE
  lore:
    # 结果: 1, 2, 3, ...
    - 'join节点: <test>'
  sections:
    test:
      type: join
      list:
        - 1
        - 2
        - 3
        - 4
        - 5
      limit: 3
      # 超过长度的部分用该符号代替
      truncated: "..."
JoinTest6:
  material: STONE
  lore:
    # 等同于:
    # - 第一行
    # - 第二行
    # - 第三行
    #
    # 这个节点应该单独占据一行
    # 不要在这行写其他文本(比如'join节点: <test>')
    # 具体请自行测试
    - '<test>'
  sections:
    test:
      type: join
      list:
        - 第一行
        - 第二行
        - 第三行
      # 像下面这样写分隔符、前缀和后缀
      # 即可达到调用多行lore的效果
      separator: "\\n"
      prefix: '"'
      postfix: '"'

RepeatTest1:
  material: STONE
  lore:
    # 等同于:
    # - 文本
    # - 文本
    # - 文本
    # 这个节点应该单独占据一行
    # 不要在这行写其他文本(比如'repeat节点: <test>')
    # 具体请自行测试
    - '<test>'
  sections:
    test:
      type: repeat
      content: 文本
      repeat: 3
      # 像下面这样写分隔符、前缀和后缀
      # 即可达到调用多行lore的效果
      separator: "\\n"
      prefix: '"'
      postfix: '"'
RepeatTest2:
  material: STONE
  lore:
    # 4行"&4&l<红宝石槽>"
    - '<repeat>'
  sections:
    repeat:
      type: repeat
      content: '&4&l<红宝石槽>'
      repeat: 4
      # 像下面这样写分隔符、前缀和后缀
      # 即可达到调用多行lore的效果
      separator: "\\n"
      prefix: '"'
      postfix: '"'
RepeatTest3:
  material: STONE
  lore:
    # "§4§l<★>-§4§l<★>-§4§l<★>"
    - '<repeat>'
  sections:
    repeat:
      type: repeat
      content: '§4§l<★>'
      repeat: 3
      separator: "-"
RepeatTest4:
  material: STONE
  lore:
    # 形似&4||||||||||&f||||||||||
    - 'repeat节点: &4<repeat1>&f<repeat2>'
  sections:
    repeat1:
      type: repeat
      content: "|"
      repeat: 10
    repeat2:
      type: repeat
      content: "|"
      repeat: 10
```

## Items/RPGExample.yml

```
RPGSwordTemplate:
  material: <材质>
  name: <前缀>大剑
  lore:
  - §e----属性----
  - <属性>
  - §e----宝石----
  - <宝石>
  unbreakable: true
  hideflags:
  - HIDE_ATTRIBUTES
  - HIDE_UNBREAKABLE
  sections:
    材质: IRON_SWORD
    宝石:
      type: repeat
      content: §7可镶嵌 <宝石类型>
      repeat: <宝石数量>
      separator: "\\n"
      prefix: '"'
      postfix: '"'
    宝石类型: §4§l红宝石
    宝石数量: 4

RPGSword1:
  inherit: RPGSwordTemplate
  sections:
    前缀: §a§l霍格沃茨
    属性:
      type: join
      list:
      - '§f攻击力: 100'
      - '§f暴击率: 10%'
      - '§f暴击伤害: 100%'
      separator: "\\n"
      prefix: '"'
      postfix: '"'
    宝石类型: §b§l蓝宝石
    宝石数量: 2

RPGSword2:
  inherit: RPGSwordTemplate
  sections:
    前缀: §b§l莱因哈特
    属性:
      type: join
      list:
      - '§f攻击力: 200'
      - '§f暴击率: 20%'
      - '§f暴击伤害: 200%'
      separator: "\\n"
      prefix: '"'
      postfix: '"'
    宝石类型: §a§l绿宝石
    宝石数量: 3
```
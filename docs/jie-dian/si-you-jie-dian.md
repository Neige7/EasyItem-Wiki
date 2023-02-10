# 私有节点

> 节点配置内全面支持节点调用

## 私有节点配置

查看：[私有节点配置](wu-pin/wu-pin-pei-zhi/README.md?id=节点)，形如

```
测试铁剑:
  material: IRON_SWORD
  name: <test>
  sections:
    test: 测试内容
```

## 快速计算节点

```
节点ID:
  type: fastcalc
  formula: 1+2+3
  min: 1
  max: 100
  fixed: 3
```

* `formula` 待计算公式，支持代入节点
* `min` 结果的最小值
* `max` 结果的最大值
* `fixed` 小数保留位数

## Join节点

```
节点ID:
  type: join
  list:
    - 第一行
    - 第二行
    - 第三行
    - 第四行
  separator: "-"
  prefix: '<'
  postfix: '>'
  limit: 3
  truncated: "..."
```

简介: 将list中的多段文本连接成一段文本

* `list` 待操作的列表
* `separator` 分隔符 (默认为", ")
* `prefix` 前缀 (默认无前缀)
* `postfix` 后缀 (默认无后缀)
* `limit` 限制列表长度
* `truncated` 超过长度的部分用该符号代替 (默认直接吞掉超过长度的部分)

示例中的节点将返回:

```
<第一行-第二行-第三行-...>
```

由于该节点功能较其他节点更加复杂,  因此我为它编写了多个示例配置帮助理解, 如下:

```
# 帮助理解list
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
# 帮助理解separator
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
# 帮助理解prefix及postfix
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
# 帮助理解limit
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
# 帮助理解truncated
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
# 利用join节点插入多行lore
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
```

## Repeat节点

```
节点ID:
  type: repeat
  content: '待重复文本'
  separator: "-"
  prefix: '<'
  postfix: '>'
  repeat: 3
```

简介: 将content的文本重复多次, 生成一整段文本

* `content` 待重复文本
* `separator` 分隔符 (默认无分隔符)
* `prefix` 前缀 (默认无前缀)
* `postfix` 后缀 (默认无后缀)
* `repeat` 重复次数

示例中的节点将返回:

```
<待重复文本-待重复文本-待重复文本>
```

由于该节点功能较其他节点更加复杂,  因此我为它编写了多个示例配置帮助理解, 如下:

```
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

## 渐变色节点

```
节点ID:
  type: gradient
  colorStart: "000000"
  colorEnd: "FFFFFF"
  step: 1
  text: 哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈
```

* `colorStart` 起始颜色
* `colorEnd` 结尾颜色
* `step` 每几个字符变一次颜色(默认为1, 可省略)
* `text` 文本内容

## 简单节点

```
节点ID: 值
```

如上所示，你直接添加节点的值。

比如：

```
test: test
```

调用`<test>`将返回`test`

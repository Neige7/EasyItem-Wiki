# 多彩掉落

> 相关配置支持解析即时声明变量

在MM怪物的配置中添加

掉落物可以像无主之地一样喷射到空中，具体配置方法如下

```
NeigeItems:
  FancyDrop:
    offset:
      x: 横向偏移
      y: 纵向偏移
    angle:
      type: 旋转方式
```

横向偏移表示物品向四周弹射的力度

纵向偏移表示物品向空中弹射的力度

旋转方式决定物品的弹射角度，是一个个绕一圈弹出去，还是随机弹出去

下面我写几个MM怪物配置实例：

```
test1:
  Type: ZOMBIE
  Health: 1
  NeigeItems:
    FancyDrop:
      offset:
        x: 0.1
        y: 1
      angle:
        # 转一圈弹出去
        type: round
```

```
test1:
  Type: ZOMBIE
  Health: 1
  NeigeItems:
    FancyDrop:
      offset:
        # 随机偏移值
        x: 0-0.1
        # 随机偏移值
        y: 1-1.5
      angle:
        # 随机角度弹出去
        type: random
```

![](_images/%E5%A4%9A%E5%BD%A9%E6%8E%89%E8%90%BD.gif)

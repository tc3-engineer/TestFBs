# TwinCAT 3 REFERENCE TO 用法说明

## 1. REFERENCE TO 是什么？

`REFERENCE TO` 可以理解为一个变量的“别名”或“引用”。

```iecst
VAR
    nDataA  : DINT := 100;
    refData : REFERENCE TO DINT;
END_VAR
```

绑定：

```iecst
refData REF= nDataA;
```

写入：

```iecst
refData := 999;
```

实际修改的是 `nDataA`。

## 2. REF= 和 := 的区别

`REF=` 用于绑定引用：

```iecst
refData REF= nDataA;
```

`:=` 用于普通赋值：

```iecst
refData := 999;
```

如果 `refData` 已经指向 `nDataA`，那么这句等价于：

```iecst
nDataA := 999;
```

## 3. FB_init 传参时为什么可以写 :=？

如果输入参数本身是：

```iecst
refAxisIn : REFERENCE TO FB_AxisUnit;
```

外部实例化时可以这样传：

```iecst
fbHomeSeq : FB_StationLoad_HomeSeq(
    refAxisIn := fbAxisLift
);
```

内部真正保存引用时，仍然建议写：

```iecst
THIS^.refAxis REF= refAxisIn;
```

一句话：

```text
:= 是参数传递；
REF= 是成员引用绑定。
```

## 4. 为什么要检查 __ISVALIDREF()？

引用可能没有绑定，所以使用前建议：

```iecst
IF __ISVALIDREF(refData) THEN
    refData := refData + 1;
END_IF
```

正式项目中，Sequence、Axis、Cylinder、Param 这种引用注入，建议在运行入口处统一检查。

## 5. 推荐架构

```text
FB_StationLoad
│
├── fbAxisLift       真实轴对象
├── fbCylClamp       真实气缸对象
├── stParam          真实参数
│
├── fbHomeSeq        保存引用
├── fbAutoSeq        保存引用
└── fbManualSeq      保存引用
```

站拥有对象，序列保存引用。

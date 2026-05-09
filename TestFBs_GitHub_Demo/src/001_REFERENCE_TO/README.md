# 001_REFERENCE_TO - TwinCAT 3 REFERENCE TO 验证例程

本例程用于验证 TwinCAT 3 中 `REFERENCE TO` 的核心用法。

## 文件说明

```text
MAIN.TcPOU
    直接验证 REFERENCE TO DINT 的基础用法；
    同时调用 FB_RefCounter 验证 FB 内部保存引用。

FB_RefCounter.TcPOU
    一个引用计数器 Demo；
    通过 Bind() 方法绑定外部 DINT；
    通过 AddValue() 方法修改外部变量；
    通过 GetValue() 方法读取当前引用值。
```

## 基础验证流程

Watch：

```text
nDataA
nDataB
refData
xRefValid
nReadValue
xBindA
xBindB
xAdd
xSet999
```

测试：

```text
1. 置位 xBindA：refData 绑定 nDataA。
2. 置位 xAdd：nDataA 从 100 变为 101。
3. 置位 xSet999：nDataA 变为 999。
4. 置位 xBindB：refData 重新绑定 nDataB。
5. 再置位 xAdd：nDataB 从 500 变为 501。
```

## FB 引用验证流程

Watch：

```text
nCounterA
nCounterB
xBindCounterA
xBindCounterB
xAdd10
nCurrentValue
xResult
```

测试：

```text
1. 置位 xBindCounterA。
2. 置位 xAdd10。
3. nCounterA 从 10 变为 20。
4. 置位 xBindCounterB。
5. 置位 xAdd10。
6. nCounterB 从 100 变为 110。
```

## 核心理解

```iecst
refData REF= nDataA;
refData := 999;
```

含义：

```text
refData 指向 nDataA；
对 refData 写入 999；
实际被修改的是 nDataA。
```

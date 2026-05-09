# TestFBs - TwinCAT 3 功能验证演示库

这是一个用于沉淀 TwinCAT 3 / Structured Text 常见语法、FB 写法、OOP 用法的小型演示库。

当前已包含：

- `001_REFERENCE_TO`：验证 `REFERENCE TO`、`REF=`、`__ISVALIDREF()`、FB 内部保存外部变量引用的用法。

## 如何导入 TwinCAT 3

1. 打开 TwinCAT 3 PLC 工程。
2. 在 PLC 工程的 `POUs` 上右键。
3. 选择 `Add -> Existing Item...`
4. 导入对应目录下的 `.TcPOU` 文件。
5. 如果工程中已有同名 `MAIN`，请先改名，避免冲突。
6. 编译、下载、在线 Watch 变量。

## 当前 Demo：001_REFERENCE_TO

验证点：

```text
1. REFERENCE TO 是引用/别名，不是值复制。
2. REF= 是引用绑定。
3. refData := 999 会修改被引用的原变量。
4. __ISVALIDREF() 可以判断引用是否有效。
5. FB 内部可以保存外部变量引用。
```

推荐 Watch：

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
nCounterA
nCounterB
xBindCounterA
xBindCounterB
xAdd10
nCurrentValue
xResult
```

## 命名说明

- `FB_`：Function Block
- `ST_`：Structure
- `GVL_`：Global Variable List
- `n`：整数变量
- `x`：布尔变量
- `fb`：功能块实例
- `ref`：引用变量

注释采用中英文结合，方便现场工程师阅读和维护。

## License

本仓库使用 MIT License。

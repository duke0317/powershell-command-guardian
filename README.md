# PowerShell Command Guardian

面向 AI Agent 的 PowerShell 命令审查 Skill。检查并修复 Windows PowerShell 5.1 与 PowerShell 7+ 命令中的兼容性、编码、路径、引号、错误传播及高风险操作问题。

## 能力

- 区分 Windows PowerShell 5.1 与 PowerShell 7+
- 检查版本专属语法与参数
- 检查控制台、管道、文件编码差异
- 识别 Windows、WSL、Git Bash、容器路径语义
- 保留条件执行、退出码、stdout/stderr 等行为
- 标记删除、覆盖、提权、注册表、服务等高风险操作
- 将 Shell 命令转换为 PowerShell，同时避免机械字符串替换

## 安装

### skills.sh CLI

```bash
npx skills add duke0317/powershell-command-guardian
```

### 手动安装

下载 [SKILL.md](./SKILL.md)，放入目标 Agent 支持的 Skill 目录。不同 Agent 的目录和加载方式可能不同，请以对应产品文档为准。

## 使用示例

```text
使用 powershell-command-guardian 检查下面命令能否在 PowerShell 5.1 运行：

Invoke-WebRequest https://example.com/data.json -OutFile C:/Temp/data.json
```

```text
把下面 WSL 命令转换为 Windows PowerShell 5.1，同时保留条件执行语义：

test -d /mnt/d/data/cache && echo ready
```

Skill 会输出具体问题、修正命令及必要假设；原命令有效时不会为了样式而重写。

## 设计原则

- 保留命令原始意图与执行语义
- 不把 `/` 无条件替换成 `\`
- 不把 Unix 命令机械映射成同名 Cmdlet
- 不把控制台编码误当成文件编码
- 不宣称未经目标环境测试的命令绝对安全
- 不擅自增加 `-Force`、递归、提权或关闭确认

## 限制

这是面向 Agent 的审查规则，不是 PowerShell 执行沙箱，也不能替代目标环境测试。执行删除、覆盖、权限、系统配置或远程操作前，必须人工确认目标与影响范围。

## 许可证

[Apache License 2.0](./LICENSE)

# 脚本教程指南 (Shell 示例)

## 快速清理日志文件

您可以使用以下简单的 Shell 脚本来自动清除大于 100MB 且超过 30 天的日志文件：

```bash
#!/bin/bash
find /var/log/ -type f -name "*.log" -size +100M -mtime +30 -exec rm {} \;
echo "Log cleanup finished."
```


## CMD how to find the disk by name:

```cmd

@REM 找到 SHIJIANZHE 盘符 , 即 备份目的地 盘符
for /F "tokens=2" %%i in ('"wmic volume get label,name | findstr SHIJIANZHE"') do set var_mybakdisk=%%i
echo var_mybakdisk:"%var_mybakdisk%"

```

注意： cmd 的 wmic 功能在Windows 11 版本 24H2 中被移除 ， 实际需要先用 管理员运行 cmd 然后开启：
开启命令：
```cmd
DISM /Online /Add-Capability /CapabilityName:WMIC~~~~
```

参见：https://learn.microsoft.com/zh-cn/answers/questions/2359404/wmic
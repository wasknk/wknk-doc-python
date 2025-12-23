# asyncio


## asyncio.Semaphore
Backpressure
## 



##  Simple example , local network ping scanner (system: WINDOWS)
```
import asyncio
import platform


async def ping_ip(ip):
    """
    异步 ping 单个 IP 地址
    """
    # 根据操作系统选择 ping 参数
    # -c 1: 发送一个包; -W 1: 等待 1 秒 (Linux/macOS)
    # -n 1: 发送一个包; -w 1000: 等待 1000 毫秒 (Windows)
    param = "-n" if platform.system().lower() == "windows" else "-c"
    wait_param = "-w" if platform.system().lower() == "windows" else "-W"
    wait_time = "1000" if platform.system().lower() == "windows" else "1"

    command = ["ping", param, "1", wait_param, wait_time, ip]

    # 使用异步子进程运行系统 ping 命令
    proc = await asyncio.create_subprocess_exec(
        *command, stdout=asyncio.subprocess.PIPE, stderr=asyncio.subprocess.PIPE
    )

    stdout, stderr = await proc.communicate()

    if proc.returncode == 0:
        return f"[+] {ip} is UP"
    return None


async def main(network_prefix):
    """
    并发扫描整个网段 (1-254)
    """
    print(f"开始扫描网段: {network_prefix}.0/24 ...\n")

    # 创建 1-254 的所有 IP 扫描任务
    tasks = [ping_ip(f"{network_prefix}.{i}") for i in range(1, 255)]

    # 使用 asyncio.gather 并发执行
    results = await asyncio.gather(*tasks)

    # 打印活跃的 IP
    active_hosts = [res for res in results if res]
    for host in active_hosts:
        print(host)

    print(f"\n扫描完成，发现 {len(active_hosts)} 个活跃主机。")


if __name__ == "__main__":
    # 请根据你实际的内网网段修改，例如 '192.168.1' 或 Docker 网段 '172.18.0'
    target_network = "192.168.1"
    asyncio.run(main(target_network))
```
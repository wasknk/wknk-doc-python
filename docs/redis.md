# redis 




## Redis with Python Example (FastAPI + BackgroundTasks)

```
import json
import asyncio
import redis
from fastapi import FastAPI, BackgroundTasks

app = FastAPI()

# 连接本地 Redis
# 建议在实际项目中从环境变量读取配置
r = redis.Redis(host='localhost', port=6379, db=0, decode_responses=True)

# --- 模拟量化脚本 ---
async def run_backtest_task(task_id: str, params: dict):
    """
    模拟一个耗时的量化回测脚本
    """
    # 1. 更新进度到 Redis
    r.set(f"status:{task_id}", "running")
    
    # 2. 模拟计算逻辑
    await asyncio.sleep(5)  # 模拟耗时 5 秒
    result = {
        "strategy": params.get("name"),
        "return_rate": "15.5%",
        "max_drawdown": "5.2%",
        "timestamp": "2025-12-28"
    }
    
    # 3. 将结果以 JSON 形式存入 Redis，设置过期时间为 1 小时 (3600秒)
    r.set(f"result:{task_id}", json.dumps(result), ex=3600)
    r.set(f"status:{task_id}", "completed")

# --- API 路由 ---

@app.post("/start-backtest/{task_id}")
async def start_backtest(task_id: str, background_tasks: BackgroundTasks):
    # 定义一些策略参数
    params = {"name": "MovingAverage_Cross"}
    
    # 将任务丢入后台执行，不阻塞 API 响应
    background_tasks.add_task(run_backtest_task, task_id, params)
    
    return {"message": "Backtest started", "task_id": task_id}

@app.get("/get-result/{task_id}")
async def get_result(task_id: str):
    # 从 Redis 获取状态和结果
    status = r.get(f"status:{task_id}")
    
    if status == "completed":
        result_json = r.get(f"result:{task_id}")
        return {"status": status, "data": json.loads(result_json)}
    
    return {"status": status or "not_found", "data": None}
```
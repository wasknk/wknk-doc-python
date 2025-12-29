# pytest 


```
.
├── app/
│   ├── main.py
│   ├── api/
│   │   ├── v1/
│   │   │   ├── endpoints/
│   │   │   │   ├── users.py
│   │   │   │   └── quant.py
│   ├── core/
│   │   └── config.py
│   ├── crud/           # 数据库增删改查逻辑
│   ├── models/         # SQLAlchemy 模型
│   └── schemas/        # Pydantic 模型
├── tests/
│   ├── __init__.py
│   ├── conftest.py     # Pytest 核心配置文件（非常关键）
│   ├── api/            # 对应 app/api/
│   │   ├── v1/
│   │   │   ├── test_users.py
│   │   │   └── test_quant.py
│   └── unit/           # 单元测试，针对纯逻辑函数
│       └── test_calculations.py
├── alembic/
├── pytest.ini          # Pytest 配置文件
└── .env.test           # 测试环境专用环境变量
```
# async-smsactivate

[![PyPI Version](https://img.shields.io/pypi/v/async-smsactivate.svg)](https://pypi.org/project/async-smsactivate/)
[![Python Version](https://img.shields.io/pypi/pyversions/async-smsactivate.svg)](https://python.org)
[![License](https://img.shields.io/pypi/l/async-smsactivate.svg)](LICENSE)

**async-smsactivate** 是 [sms-activate.org](https://sms-activate.org) 官方 SDK 的**异步增强版本**，在原同步实现基础上基于
`aiohttp` 和类型注释构建，支持高并发场景下的短信接码服务调用，接口与原 SDK 完全兼容。

## 🌟 核心特性

- **全异步支持**：基于 `aiohttp` 实现异步 API，显著提升并发性能。
- **类型安全**：完整的类型注释（Type Hints），增强代码可读性和 IDE 提示。
- **无缝兼容**：入参和返回格式与原 SDK 一致，无需修改业务逻辑即可迁移。
- **错误处理**：继承原 SDK 的错误码映射和响应解析逻辑，确保稳定性。

## 📦 安装方法

```bash
pip install async-smsactivate
```

## 🚀 使用示例

```python
import asyncio
from async_smsactivate import AsyncSMSActivateAPI


async def example_usage():
    # 初始化异步客户端（需替换为你的 API Key）
    api = AsyncSMSActivateAPI(api_key="YOUR_API_KEY_HERE")

    # 1. 获取账户余额
    balance = await api.getBalance()
    print("Balance:", balance)

    # 2. 获取指定服务和国家的号码（示例：WhatsApp 俄罗斯号码）
    number_response = await api.getNumber(
        service="whatsapp",  # 服务名称
        country="ru"  # 国家代码
    )
    print("Number Response:", number_response)

    # 3. 关闭异步会话（释放资源）
    await api.close()


if __name__ == "__main__":
    asyncio.run(example_usage())
```

## 📖 接口说明

### 初始化

```python
from async_smsactivate import AsyncSMSActivateAPI

api = AsyncSMSActivateAPI(api_key="你的 API Key")  # 必需参数
```

### 主要方法

所有接口与原 SDK 一致，支持以下核心功能（完整列表见 官方文档）：

| 功能	         | 方法名	                              | 说明           |
|-------------|-----------------------------------|--------------|
| 账户余额	       | getBalance()	                     | 查询账户余额       |
| 获取号码	       | getNumber()	                      | 购买指定服务和国家的号码 |
| 号码状态		      | getStatus(activation_id)	         | 查询号码激活状态     |
| 更新状态		      | setStatus(activation_id, status)	 | 更新号码状态       |
| 租赁服务		      | getRentNumber()	                  | 租赁号码相关操作     |
| 价格与国家		     | getPrices(), getCountries()	      | 查询价格和支持的国家列表 |

## ⚠️ 注意事项
1. 异步运行：所有方法需在异步事件循环中调用（如通过 asyncio.run()）。

2. 会话关闭：使用完毕务必调用 api.close()，避免网络连接泄漏。

3. 错误处理：返回值包含 error 字段时表示请求失败，可通过 get_error() 获取错误信息。

## 🤝 贡献与反馈
欢迎通过以下方式参与项目：

1. 提交 Issue：在 问题页面 反馈 Bug 或功能建议。
2. 提交代码：Fork 仓库后创建分支，提交 Pull Request 并描述变更。
## 📜 许可证
本项目采用 MIT 许可证，详见 LICENSE 文件。
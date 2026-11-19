# API 参考

这一页用于展示接口文档应该怎样写。**以下接口、数据和响应均为教学示例，不存在真实的后端服务，也不能直接请求 GitHub Pages 获得这些响应。**

## 示例接口：查询文档列表

| 项目 | 说明 |
| --- | --- |
| 方法 | `GET` |
| 路径 | `/api/docs` |
| 功能 | 获取文档目录列表 |
| 认证 | 示例不要求认证 |
| 返回格式 | JSON |
| 是否真实可用 | 否，仅供文档演示 |

### 请求示意

```http
GET /api/docs HTTP/1.1
Accept: application/json
```

### 成功响应示意

```json
{
  "code": 200,
  "message": "ok",
  "items": [
    {
      "id": 1,
      "title": "使用指南",
      "slug": "guide"
    },
    {
      "id": 2,
      "title": "关于项目",
      "slug": "about"
    }
  ]
}
```

### 字段含义

| 字段 | 类型 | 描述 |
| --- | --- | --- |
| `code` | integer | 示例状态码 |
| `message` | string | 简短的状态说明 |
| `items` | array | 文档条目集合 |
| `items[].id` | integer | 文档编号 |
| `items[].title` | string | 文档标题 |
| `items[].slug` | string | 文档短标识 |

## 示例接口：按编号查询文档

假设某个真实后端提供 `/api/docs/{id}` 路径，则可以按下列形式写出接口规范：

```http
GET /api/docs/1 HTTP/1.1
Accept: application/json
```

示例响应：

```json
{
  "code": 200,
  "item": {
    "id": 1,
    "title": "使用指南",
    "summary": "本地构建和自动发布步骤"
  }
}
```

## 为什么静态文档也能写 API 说明？

API 文档本质上是**关于接口的文字与格式化示例**。它可以被放在静态网站中阅读；而真正处理 HTTP 请求、查询数据库并返回动态 JSON 的后端，需要另行开发和部署。

想了解项目的实际自动发布流程，请返回 [使用指南](guide.md) 或 [关于项目](about.md)。

# NGA 论坛用户 IP 属地统计

爬取 NGA 论坛"网事杂谈"版面近期帖子中回复用户的 IP 属地，统计各地区人数，并整理成可直接导入 ECharts 的数据格式。

## 流程

`nga_ip_data.ipynb` 按以下步骤执行：

1. **版面页**：抓取版面前 `limit` 页（默认 5 页）的帖子 ID，去重
2. **主题页**：遍历帖子，获取所有回复用户的 uid；超过 100 页的帖子跳过
3. **用户页**：调用用户信息接口获取 `ipLoc`（IP 属地），结果追加写入 `area.txt`
4. **结果处理**：分类计数、排序，输出 ECharts 需要的 `{value, name}` 列表

笔记本中保留了中断后续爬的代码（已注释）。

## 环境

- Python 3 + Jupyter Notebook
- `requests`、`lxml`、`numpy`
- 接口说明参考 [NGA-API-Documents](https://github.com/wolfcon/NGA-API-Documents)

## 使用

1. 在浏览器中登录 NGA，从开发者工具的 Network 面板复制 Cookie，填入 `headers['Cookie']`
2. 按顺序运行笔记本单元格

## 注意

请求之间已设置延时（版面 / 主题页 1 s，用户页 0.1 s）。请勿调大页数或缩短延时，避免对论坛服务器造成负担。

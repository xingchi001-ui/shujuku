# 礼服设计视觉知识库

本目录包含从用户上传的 PDF 资料中，使用 MiniMax-M3 进行非 OCR、逐本逐页视觉理解后生成的知识库文件。

## 文件

- `segments_846.jsonl`：846 条成功视觉分析记录，包含书籍、页码、视觉摘要、结构化设计维度和来源信息。
- `show_gown_studio_846pages.db`：由上述 846 条记录导入的 SQLite 数据库，表名为 `dress_knowledge`。
- `failed_pages.jsonl`：仍未成功分析的 1 页记录，不在数据库中伪造内容。
- `full_analysis.log`：逐页分析日志。

## 当前覆盖范围

- 总页数：847
- 成功视觉分析：846 页
- 未成功页面：1 页
- 未成功页面：`《新婚礼服100例》第107页`

## 视觉理解约束

分析采用视觉理解，不使用 OCR。无法从图像确认的面料成分、克重、内层支撑、闭合方式和真实穿着效果，会保留在 `uncertainty` 或 `risk` 字段中。

## 数据库导入

```bash
python3 import_dress_data.py segments_846.jsonl --db show_gown_studio_846pages.db --replace
```

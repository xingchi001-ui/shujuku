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

## 2026-11-07 新增《婚纱礼服100款》纸样基础层

新增 `segments_hunshasheji100.jsonl` 共 217 页，使用 MiniMax-M3 逐页视觉理解，未做 OCR。记录在原有廓形、面料、工艺、动态等字段之外，增加纸样基础字段：纸样分割线、纸样省道、纸样拼片、纸样层级、立体裁剪线索、放量线索、面料结构关系、纸样工艺顺序、纸样验证项目、纸样风险。

`show_gown_studio.db` 已更新为合并数据库：`dress_knowledge=1063`、`model_styling_knowledge=1036`、`pattern_knowledge=217`。纸样字段只记录画面可见证据；看不见的尺寸、量体、内层支撑和真实省量会明确标记为不可判断，不能直接替代打版师量体和胚布验证。

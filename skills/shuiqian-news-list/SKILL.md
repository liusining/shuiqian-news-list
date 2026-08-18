---
name: shuiqian-news-list
description: 拉取《睡前消息》每日新闻列表。当用户想看今天、昨天或历史某天的睡前消息、睡前新闻、马督工新闻列表时使用。
---

# 睡前消息每日新闻列表

获取《睡前消息》栏目每天发布的新闻列表（当天或历史任意一天），输出为带原文链接的可读清单。

## 数据接口

- 主地址：`https://shuiqian-news.sining.ai/daily/YYYY-MM-DD.json`
- 备用地址：`https://raw.githubusercontent.com/liusining/shuiqian-news-list/main/data/daily/YYYY-MM-DD.json`
- 日期索引：`https://shuiqian-news.sining.ai/index.json`（字段：`latest` 最新可用日期、`dates` 全部可用日期、`lastUpdated` 最后更新时间）

先请求主地址；网络失败或返回非 200/404 的错误时切换备用地址。两个地址内容一致。

## 步骤

1. **解析日期**：把用户的说法（今天、昨天、前天、上周三、2023年3月15日……）解析为 `YYYY-MM-DD`。一律以东八区（Asia/Shanghai）的当前日期为基准，不要用 UTC。
2. **请求数据**：按上面的地址获取 JSON。
3. **404 处理**（按顺序判断）：
   - 目标日期在未来 → 告知日期在未来，无法查询。
   - 目标日期是今天 → 当天列表一般在晚上 21:00–24:00 之间发布。改取 `index.json`，回答「今天的还没发布，最新一期是 {latest}」，并询问是否要看最新一期。
   - 其他情况（历史缺档）→ 回答「没有当天的新闻，找不到了」。不要推荐附近日期，不要编造内容。
4. **排版输出**：见下节。

## JSON 字段

- `date` 日期；`description` 当日主题（可为 null）；`article_url` 公众号原文链接（可为 null）
- `items[]`：`no` 序号、`title` 标题、`body` 正文（Markdown，可能含加粗）、`source_url` 该条新闻的原文链接（可为 null）

## 排版建议

把 JSON 重排为人类可读的清单，**每条新闻必须包含标题、正文、原文链接三部分**：

```markdown
## 睡前消息每日新闻 {date}（{description}）

### {no}. {title}

{body}

🔗 {source_url}

（……逐条列出……）

——内容来自《睡前消息》编辑部（[公众号原文]({article_url})）
```

- 条数多时也不要自行删减条目；用户只要概览时，可先给标题清单，再按需展开正文。
- `body` 中的加粗原样保留；`source_url` 为 null 时省略链接行；`description`、`article_url` 为 null 时省略对应部分。
- 输出中的所有链接必须来自 JSON，禁止虚构、改写或补全链接。

## 错误与边界

- 两个地址都失败：明确告知网络失败，不要凭记忆补内容。
- 数据起点为 2022-11-20，更早的日期直接说明超出数据范围。

# 睡前消息每日新闻列表

《睡前消息》栏目每天晚上发布一期新闻列表。本仓库把它整理成按天存放的 JSON 数据，并提供一个 AI agent skill（适用于 Claude Code 等），随时查询当天或历史某天的新闻列表。

## 安装 skill

```bash
npx skills add liusining/shuiqian-news-list
```

或克隆本仓库后执行 `npx skills add ./skills --all`。

装好后直接对 agent 说「今天的睡前消息」「2023年3月15日的睡前新闻」即可。

## 数据接口

| 用途 | 地址 |
|---|---|
| 某天的新闻列表 | `https://shuiqian-news.sining.ai/daily/YYYY-MM-DD.json` |
| 备用地址 | `https://raw.githubusercontent.com/liusining/shuiqian-news-list/main/data/daily/YYYY-MM-DD.json` |
| 日期索引 | `https://shuiqian-news.sining.ai/index.json` |

每日一个 JSON 文件，字段：`date`、`description`（当日主题）、`article_url`（公众号原文链接）、`items[]`（每条新闻的 `no`、`title`、`body`、`source_url`）。缺失日期返回 404。

## 数据范围

- **2022-11-20 ~ 2023-11-03**：历史数据，来自社区归档项目 [bedtimenews archive](https://github.com/bedtimenews/bedtimenews-archive-contents)。
- **2023-11-04 ~ 2026-08-17**：缺档，无数据。
- **2026-08-18 起**：每日更新。

## 版权声明

新闻列表内容版权归《睡前消息》编辑部所有。本仓库仅做非商业目的的格式整理与聚合，每条新闻均附原文链接；如权利人提出要求，将立即删除相关内容。

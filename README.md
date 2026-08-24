# 睡前消息每日新闻列表

《睡前消息》栏目每天晚上发布一期新闻列表。本仓库把它整理成按天存放的 JSON 数据，每日更新。

## 使用 skill

配套的 AI agent skill（适用于 Claude Code 等，可随时查询当天或历史某天的新闻列表）在独立仓库 [shuiqian-news-skill](https://github.com/liusining/shuiqian-news-skill)：

```bash
npx skills add liusining/shuiqian-news-skill
```

装好后直接对 agent 说「今天的睡前消息」「2023年3月15日的睡前新闻」即可。

## 数据接口

| 用途 | 地址 |
|---|---|
| 某天的新闻列表 | `https://shuiqian-news.sining.ai/daily/YYYY-MM-DD.json` |
| 备用地址 | `https://raw.githubusercontent.com/liusining/shuiqian-news-list/main/data/daily/YYYY-MM-DD.json` |
| 日期索引 | `https://shuiqian-news.sining.ai/index.json` |

每日一个 JSON 文件，字段：`date`、`description`（当日主题）、`article_url`（本期原文链接）、`items[]`（每条新闻的 `no`、`title`、`body`、`source_url`）。缺失日期返回 404。

## 数据范围

- **2019-01-10 ~ 2022-11-19**：历史数据，整理自《睡前消息》官方微博公开发布的内容。
- **2022-11-20 ~ 2023-11-03**：历史数据，来自社区归档项目 [bedtimenews archive](https://github.com/bedtimenews/bedtimenews-archive-contents)。
- **2023-11-04 ~ 2026-08-17**：历史数据，大部分整理自官方微博公开内容。
- **2026-08-18 起**：每日更新。

各时期均有少量日期缺档（停更或原文已不可得），对应日期接口返回 404。

## 版权声明

新闻列表内容版权归《睡前消息》编辑部所有。本仓库仅做非商业目的的格式整理与聚合，每条新闻均附原文链接；如权利人提出要求，将立即删除相关内容。

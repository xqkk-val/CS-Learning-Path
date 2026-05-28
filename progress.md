# 学习进度总览

## 本周统计
| 日期  | 学习内容 | 笔记  | 状态  |
| --- | ---- | --- | --- |
|     |      |     |     |

## 累计统计
- 总笔记数：
- 完成目标数：


## 📊 笔记统计

```dataview
TABLE file.ctime AS "创建日期"
FROM "notes/cpp/file-io"
SORT file.name ASC
```

## 📋 任务完成情况

```dataview
TASK
FROM "goals"
WHERE !completed
GROUP BY file.name
```
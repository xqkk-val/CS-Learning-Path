# 学习进度总览

> 更新时间：`= date(today)`

## 📊 笔记清单

```dataview
TABLE file.ctime AS "创建日期", 标签
FROM "notes/cpp/file-io"
SORT file.name ASC
```

## 📋 待完成任务

```dataview
TASK
FROM "goals"
WHERE !completed
```

## 📈 学习统计

- 笔记总数：`= length(rows)` 
- 已完成任务：查看看板「✅ 已完成」列
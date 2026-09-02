# agent-task-progress

用于记录定时 Agent 任务的进展与运行状态。

## 存储约定

每个任务必须在 `tasks/` 下拥有一个独立目录；不得把不同任务的状态文件混放在同一目录中。

目录名使用稳定、可读的任务标识，例如：

```text
tasks/
  daily-backup/
    status.md
    history.jsonl
  dependency-audit/
    status.md
    history.jsonl
```

- `status.md`：该任务当前状态、最近一次运行结果与下一步。
- `history.jsonl`：按时间追加的运行记录，便于自动化读取。
- 任务目录内可增加该任务专用的日志或产物，但不能存放其他任务的数据。

新建任务时先创建 `tasks/<task-id>/`，再将它的所有状态文件写入该目录。

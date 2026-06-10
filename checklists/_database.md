---
notion-bases: true
schema:
  - id: status
    name: 状态
    type: select
    visible: true
    width: 100
    options:
      - value: pending
        color: '#e8a138'
      - value: in_progress
        color: '#4bb563'
      - value: done
        color: '#888888'
  - id: tags
    name: 标签
    type: multiselect
    visible: true
    width: 200
  - id: created
    name: 创建
    type: date
    visible: true
    width: 110
  - id: updated
    name: 更新
    type: date
    visible: true
    width: 110
views:
  - id: default
    type: table
    filters: []
    sorts:
      - columnId: updated
        direction: desc
    hiddenColumns: []
    columnWidths: {}
  - id: board-status
    name: 按状态
    type: board
    filters: []
    sorts: []
    hiddenColumns: []
    columnWidths: {}
    groupByColumnId: status
---

# 行动追踪

> 待校验、备忘、待办清单。

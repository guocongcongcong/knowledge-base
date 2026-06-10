---
notion-bases: true
schema:
  - id: type
    name: 类型
    type: select
    visible: true
    width: 100
    options:
      - value: query
      - value: comparison
  - id: tags
    name: 标签
    type: multiselect
    visible: true
    width: 180
  - id: confidence
    name: 可信度
    type: select
    visible: true
    width: 100
    options:
      - value: high
        color: '#4bb563'
      - value: medium
        color: '#e8a138'
      - value: low
        color: '#e25555'
  - id: contested
    name: 争议
    type: checkbox
    visible: true
    width: 70
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
  - id: sources
    name: 来源
    type: text
    visible: false
    width: 200
views:
  - id: default
    type: table
    filters: []
    sorts:
      - columnId: updated
        direction: desc
    hiddenColumns:
      - sources
    columnWidths: {}
  - id: board-confidence
    name: 按可信度
    type: board
    filters: []
    sorts: []
    hiddenColumns:
      - sources
    columnWidths: {}
    groupByColumnId: confidence
---

# 查询与研究

> 调研对比、推演分析、学习路线。

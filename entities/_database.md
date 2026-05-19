---
notion-bases: true
schema:
  - id: status
    name: 状态
    type: status
    visible: true
    width: 100
    options:
      - value: active
        color: '#4bb563'
      - value: paused
        color: '#e8a138'
      - value: archived
        color: '#868686'
  - id: tags
    name: 标签
    type: multiselect
    visible: true
    width: 180
  - id: repo
    name: 仓库
    type: url
    visible: true
    width: 200
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
    name: 看板
    type: board
    filters: []
    sorts: []
    hiddenColumns: []
    columnWidths: {}
    groupByColumnId: status
---

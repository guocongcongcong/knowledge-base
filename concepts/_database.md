---
notion-bases: true
schema:
  - id: tags
    name: 标签
    type: multiselect
    visible: true
    width: 180
    options:
      - value: ai-tools
      - value: claude-code
      - value: skills
      - value: programming
      - value: obsidian
      - value: knowledge-base
      - value: memory
      - value: token-efficiency
      - value: visualization
      - value: workflow
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
  - id: contradictions
    name: 矛盾页
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
      - contradictions
    columnWidths: {}
  - id: board-confidence
    name: 按可信度
    type: board
    filters: []
    sorts:
      - columnId: updated
        direction: desc
    hiddenColumns:
      - sources
      - contradictions
    columnWidths: {}
    groupByColumnId: confidence
  - id: gallery-view
    name: 画廊
    type: gallery
    filters: []
    sorts:
      - columnId: updated
        direction: desc
    hiddenColumns:
      - sources
      - contradictions
    columnWidths: {}
    galleryCardSize: medium
---

---
summary: "設計文件範本"
read_when:
  - 建立新的設計文件
  - 學習設計文件格式
---

# [功能名稱] 設計文件

## Goals

- [列出這次要達成的目標]
- [要解決什麼問題？]
- [成功的定義是什麼？]

## Non-goals

- [這次明確不做什麼]
- [避免 AI 過度設計]
- [避免範圍蔓延]

## Decisions (locked)

這些已經決定了，不要改：

- **[決策 1]:** [原因]
- **[決策 2]:** [原因]
- **[決策 3]:** [原因]

## Key concepts

### [概念 1]

[定義]

### [概念 2]

[定義]

### [概念 3]

[定義]

## Config surface

### 設定項

- `config.key.one` — [說明]
- `config.key.two` — [說明]

### 環境變數

- `ENV_VAR_ONE` — [說明]
- `ENV_VAR_TWO` — [說明]

## Implementation phases

### Phase 1: [名稱]

- [任務 1]
- [任務 2]
- [任務 3]

### Phase 2: [名稱]

- [任務 1]
- [任務 2]

### Phase 3: [名稱]

- [任務 1]
- [任務 2]

## Data structures

```json
{
  "example": {
    "field1": "string",
    "field2": 123,
    "field3": true
  }
}
```

## Testing plan

- **Unit tests:** [要測什麼]
- **Integration tests:** [要測什麼]
- **E2E tests:** [要測什麼]

## Open risks

- [風險 1]：[緩解方式]
- [風險 2]：[緩解方式]

## Related docs

- [相關文件 1](link)
- [相關文件 2](link)

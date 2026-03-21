# CTOR API Contract v0.2  
Расширенный API‑контракт для UI, Engine, ИИ‑ботов и игровых платформ CTOR

Версия: **v0.2**  
Статус: **расширенный контракт**  
Совместим с: **v0.1**

---

# 1. Назначение документа

Этот документ расширяет минимальный API‑контракт CTOR (v0.1), добавляя:

- тайминг ходов  
- обработку ошибок  
- расширенные типы ходов  
- расширенные события  
- метаданные матча  
- поддержку разных игровых режимов  
- расширенный протокол для ботов  

Документ служит **официальным стандартом** для всех модулей CTOR:

- CTOR-UI  
- CTOR-Engine  
- CTOR-AI-AI  
- CTOR-H-AI  
- CTOR-H-H  
- CTOR-TEAM-TEAM  

---

# 2. Новые сущности API

v0.2 добавляет:

1. **TimingInfo** — тайминг игрока или бота  
2. **Error** — ошибка выполнения хода  
3. **MatchMeta** — метаданные матча  
4. **ExtendedMoveType** — расширенные типы ходов  
5. **ExtendedEvent** — расширенные события  

---

# 3. Расширенный GameState

```json
{
  "board": [],
  "current_player": "PLAYER_1",
  "turn": 0,
  "legal_moves": [],
  "score": {},
  "status": "RUNNING",
  "timing": {
    "PLAYER_1": { "time_left_ms": 30000 },
    "PLAYER_2": { "time_left_ms": 28000 }
  },
  "meta": {
    "mode": "AI-AI",
    "match_id": "MATCH_001",
    "move_time_limit_ms": 2000
  }
}
```

### Новые поля:

| Поле | Тип | Описание |
|------|-----|----------|
| timing | объект | Тайминг игроков |
| meta | объект | Метаданные матча |

---

# 4. TimingInfo

```json
{
  "PLAYER_1": {
    "time_left_ms": 30000
  }
}
```

### Поля:

| Поле | Тип | Описание |
|------|-----|----------|
| time_left_ms | число | Оставшееся время игрока |

---

# 5. MatchMeta

```json
{
  "mode": "TEAM-TEAM",
  "match_id": "MATCH_001",
  "move_time_limit_ms": 2000
}
```

### Поля:

| Поле | Тип | Описание |
|------|-----|----------|
| mode | строка | H-H, H-AI, AI-AI, TEAM-TEAM |
| match_id | строка | Уникальный ID матча |
| move_time_limit_ms | число | Лимит времени на ход |

---

# 6. Расширенный формат Move

```json
{
  "player_id": "PLAYER_1",
  "move_type": "PLACE",
  "coordinates": [2, 3],
  "metadata": {
    "confidence": 0.82,
    "agent_version": "0.3"
  }
}
```

### Новые поля:

| Поле | Тип | Описание |
|------|-----|----------|
| metadata | объект | Доп. данные (для ИИ‑ботов) |

---

# 7. Расширенные типы ходов (ExtendedMoveType)

v0.2 добавляет:

- **PASS** — пропуск хода  
- **RESIGN** — сдача  
- **HINT** — запрос подсказки (UI)  
- **TEAM_SIGNAL** — командный сигнал (TEAM-TEAM)  
- **DEBUG_MOVE** — отладочный ход (AI-AI)  

---

# 8. Расширенный формат Event

### Ошибка хода
```json
{
  "event": "MOVE_REJECTED",
  "error": {
    "code": "ILLEGAL_MOVE",
    "message": "Move is not allowed in current state."
  }
}
```

### Тайм-аут
```json
{
  "event": "TIMEOUT",
  "player_id": "PLAYER_2"
}
```

### Командный сигнал
```json
{
  "event": "TEAM_SIGNAL_RECEIVED",
  "team_id": "TEAM_ALPHA",
  "signal": "ATTACK_RIGHT"
}
```

---

# 9. Ошибки (Error)

```json
{
  "code": "ILLEGAL_MOVE",
  "message": "Move is not allowed in current state."
}
```

### Коды ошибок:

| Код | Описание |
|------|----------|
| ILLEGAL_MOVE | Недопустимый ход |
| TIMEOUT | Игрок превысил лимит времени |
| INVALID_FORMAT | Некорректный формат данных |
| ENGINE_ERROR | Ошибка движка |
| BOT_ERROR | Ошибка ИИ‑бота |
| TEAM_PROTOCOL_ERROR | Ошибка командного протокола |

---

# 10. Расширенный протокол для ботов

## 10.1 Engine → Bot

### Состояние игры
```json
{
  "type": "state",
  "payload": { }
}
```

### Ошибка
```json
{
  "type": "error",
  "payload": { }
}
```

### Тайм-аут
```json
{
  "type": "timeout",
  "player_id": "BOT_1"
}
```

---

## 10.2 Bot → Engine

### Ход
```json
{
  "type": "move",
  "payload": { }
}
```

### Сдача
```json
{
  "type": "resign"
}
```

### Командный сигнал (TEAM-TEAM)
```json
{
  "type": "team_signal",
  "payload": "ATTACK_RIGHT"
}
```

---

# 11. Расширенный протокол UI ↔ Engine

### UI → Engine

- `submitMove(move)`
- `requestHint()`
- `resign()`

### Engine → UI

- `updateGameState(state)`
- `sendEvent(event)`
- `sendError(error)`
- `sendHint(move)`

---

# 12. Применение API v0.2

| Модуль | Использует v0.2 | Особенности |
|--------|------------------|-------------|
| CTOR-UI | Да | Подсказки, ошибки, тайминг |
| CTOR-Engine | Да | Полная реализация |
| CTOR-AI-AI | Да | Тайминг, ошибки, расширенные ходы |
| CTOR-H-AI | Да | Тайм-ауты, подсказки |
| CTOR-H-H | Частично | Ошибки, тайминг |
| CTOR-TEAM-TEAM | Да | Командные сигналы |

---

# 13. Статус документа

Версия: **v0.2**  
Статус: **расширенный контракт**  
Назначение: подготовка к полноценной интеграции UI, Engine, ботов и командных матчей.  
Совместим с v0.1.

---

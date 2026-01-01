# 🔧 Troubleshooting Guide / Руководство по устранению проблем

[🇷🇺 Русская версия](#-русская-версия) | [🇬🇧 English Version](#-english-version)

---

## 🇷🇺 Русская версия

### Частые проблемы и решения

#### 1. Бот не отвечает на сообщения

**Симптомы:**
- Отправляете сообщение в Telegram, но нет ответа
- Нет индикатора "печатает..."

**Диагностика:**

1. **Проверьте статус workflow:**
   ```
   n8n → Откройте workflow → Проверьте статус в правом верхнем углу
   ```
   ✅ Должно быть: `Active` (зелёная кнопка)
   ❌ Если `Inactive` → Нажмите кнопку для активации

2. **Проверьте логи выполнения:**
   ```
   n8n → Executions (вкладка внизу слева) → Последние выполнения
   ```
   - Если нет новых executions → проблема с Telegram webhook
   - Если есть executions с ошибками → смотрите детали ошибки

3. **Проверьте Owner ID:**
   ```
   Узел "Owner Verification" → Условие → rightValue: ваш Telegram ID
   ```
   Получите свой ID через [@userinfobot](https://t.me/userinfobot)

4. **Проверьте Telegram webhook:**
   ```bash
   curl https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getWebhookInfo
   ```
   Ответ должен содержать `url` с адресом n8n

**Решение:**

```bash
# Если webhook не установлен, n8n должен сделать это автоматически
# Попробуйте деактивировать и активировать workflow:
1. Нажмите "Active" → "Inactive"
2. Подождите 5 секунд
3. Нажмите "Inactive" → "Active"
```

---

#### 2. Ошибка "Unauthorized" / Бот отвечает "только для личного использования"

**Симптомы:**
```
⛔ К сожалению, этот бот только для личного использования.

Если хотите такого же бота для себя — напишите @khanalytiq
```

**Причина:** Ваш Telegram ID не совпадает с ID в Owner Verification

**Решение:**

1. **Узнайте свой Telegram ID:**
   - Напишите [@userinfobot](https://t.me/userinfobot)
   - Скопируйте ваш ID (например: `123456789`)

2. **Обновите Owner Verification:**
   ```
   Узел "Owner Verification" → Правило "boss" → Условие
   rightValue: замените "331119294" на ваш ID
   ```

3. **Обновите Memory Buffer:**
   ```
   Узел "Simple Memory" → sessionKey
   Замените "331119294" на ваш ID
   ```

4. **Обновите Error Notification:**
   ```
   Узел "Error Notification" → chatId
   Замените "331119294" на ваш ID
   ```

5. **Сохраните workflow** (Ctrl+S или Cmd+S)

---

#### 3. Ошибка OpenAI API

**Симптомы:**
```
❌ Произошла ошибка при обработке запроса.

OpenAI Chat Model

Error: Incorrect API key provided
```

**Возможные причины:**

1. **Неправильный API ключ**

   **Решение:**
   ```
   n8n → Credentials → OpenAI API
   → Проверьте ключ: должен начинаться с "sk-proj-" или "sk-"
   → Если неверный → создайте новый на platform.openai.com/api-keys
   ```

2. **Нет баланса на аккаунте OpenAI**

   **Проверка:**
   ```
   platform.openai.com → Settings → Billing → Check balance
   ```
   
   **Решение:**
   ```
   Add payment method → Add credits (минимум $5)
   ```

3. **API ключ отозван или истёк**

   **Решение:**
   ```
   platform.openai.com → API keys
   → Проверьте статус ключа
   → Если "Revoked" → создайте новый ключ
   → Обновите в n8n credentials
   ```

4. **Rate limit превышен**

   **Ошибка:**
   ```
   Error: Rate limit reached for gpt-4-mini
   ```
   
   **Решение:**
   ```
   Подождите несколько минут или:
   platform.openai.com → Settings → Limits
   → Увеличьте лимиты (если доступно)
   ```

---

#### 4. Ошибка Google Calendar API

**Симптомы:**
```
❌ Произошла ошибка при обработке запроса.

Create an event in Google Calendar

Error: Invalid Credentials
```

**Возможные причины:**

1. **Credential не авторизован**

   **Решение:**
   ```
   n8n → Найдите узел с Google Calendar
   → Credential → Нажмите "Reconnect"
   → Войдите в Google аккаунт
   → Разрешите доступ к Calendar
   ```

2. **Google Calendar API не включен**

   **Решение:**
   ```
   1. console.cloud.google.com
   2. Выберите ваш проект
   3. APIs & Services → Library
   4. Найдите "Google Calendar API"
   5. Нажмите "Enable"
   ```

3. **OAuth consent screen не настроен**

   **Решение:**
   ```
   1. console.cloud.google.com
   2. APIs & Services → OAuth consent screen
   3. Заполните обязательные поля:
      - App name
      - User support email
      - Developer contact
   4. Add Scopes:
      - https://www.googleapis.com/auth/calendar
      - https://www.googleapis.com/auth/calendar.events
   5. Add Test Users: ваш email
   6. Сохраните
   ```

4. **Токен истёк**

   **Симптом:**
   ```
   Error: Token has been expired or revoked
   ```
   
   **Решение:**
   ```
   n8n → Google Calendar credential
   → Нажмите "Reconnect"
   → Заново авторизуйтесь
   ```

---

#### 5. Голосовые сообщения не распознаются

**Симптомы:**
- Отправляете голосовое, но нет ответа
- Ошибка в узле "Transcribe a recording"

**Возможные причины:**

1. **Файл слишком большой**

   **Ограничение:** 25 МБ (Telegram) и 25 МБ (OpenAI Whisper)
   
   **Решение:**
   ```
   Отправляйте более короткие голосовые сообщения (до 2-3 минут)
   ```

2. **Неподдерживаемый формат**

   **Решение:**
   ```
   Telegram автоматически конвертирует в OGG
   Если проблема сохраняется:
   - Проверьте узел "Get a file"
   - Убедитесь, что Binary data передаётся в "Transcribe"
   ```

3. **Ошибка Whisper API**

   **Симптом:**
   ```
   Error: Audio file could not be processed
   ```
   
   **Решение:**
   ```
   - Проверьте качество голосового (не слишком тихо)
   - Убедитесь, что есть баланс на OpenAI
   - Проверьте rate limits Whisper (50 req/min)
   ```

4. **Плохое качество звука**

   **Решение:**
   ```
   - Записывайте в тихом месте
   - Говорите чётко и медленно
   - Избегайте фоновых шумов
   ```

---

#### 6. AI неправильно интерпретирует запросы

**Симптомы:**
- Создаёт событие не на то время
- Не понимает название события
- Неправильно определяет дату

**Примеры:**

**Проблема:** "Создай встречу завтра" → Создаёт на следующую неделю

**Решение:**
```
Будьте более конкретны:
✅ "Создай встречу завтра 2 января в 15:00"
✅ "Создай встречу на завтра 15 часов"

Проверьте часовой пояс в узле "HTTP Request1" (Get Timezone)
```

**Проблема:** "Встреча в 3 часа" → Создаёт на 03:00 вместо 15:00

**Решение:**
```
Уточняйте:
✅ "Встреча в 3 часа дня" или "в 15:00"
✅ "Встреча в 3 PM"

Или обновите промпт в "Calendar AI Agent":
"If time is ambiguous (1-12), assume PM for business hours"
```

**Проблема:** AI не находит событие для редактирования

**Решение:**
```
1. Сначала запросите список событий:
   "Что у меня завтра?"

2. Затем укажите точное название:
   "Перенеси 'Встреча с Ивановым' на 16:00"
   (с кавычками для точного совпадения)
```

---

#### 7. Workflow выполняется слишком долго

**Симптомы:**
- Ответ приходит через 30+ секунд
- Timeout ошибки

**Диагностика:**

```
n8n → Executions → Выберите медленное выполнение
→ Смотрите время каждого узла
```

**Частые причины:**

1. **OpenAI API медленный отклик**

   **Решение:**
   ```
   - Проверьте status.openai.com
   - Если проблема сохраняется:
     Узел "OpenAI Chat Model"
     → Options → Timeout → Увеличьте до 60 секунд
   ```

2. **Google Calendar API медленный**

   **Решение:**
   ```
   - Обычно это временно
   - Проверьте status.cloud.google.com
   ```

3. **Большой контекст памяти**

   **Решение:**
   ```
   Узел "Simple Memory"
   → contextWindowLength: уменьшите с 10 до 5
   
   Это ускорит обработку, но уменьшит контекстную память
   ```

4. **Сложный промпт AI**

   **Решение:**
   ```
   Узел "Calendar AI Agent" → promptType
   → Упростите System Prompt (удалите лишние инструкции)
   ```

---

#### 8. События создаются не в том часовом поясе

**Симптомы:**
- Создаёте на 15:00, появляется на 12:00 (или наоборот)
- Время сдвинуто на N часов

**Причина:** Неправильный часовой пояс

**Диагностика:**

1. **Проверьте часовой пояс Google Calendar:**
   ```
   calendar.google.com → Settings → General → Time zone
   ```

2. **Проверьте часовой пояс n8n:**
   ```
   n8n → Workflow Settings → Timezone
   ```

3. **Проверьте HTTP Request (Get Timezone):**
   ```
   Узел "HTTP Request1" → Test step
   → Проверьте ответ: {"value": "Europe/Moscow"}
   ```

**Решение:**

1. **Установите правильный timezone в n8n:**
   ```
   Workflow Settings → Timezone → выберите ваш часовой пояс
   Например: Europe/Moscow, America/New_York, Asia/Tokyo
   ```

2. **Обновите Default timezone в промпте:**
   ```
   Узел "Calendar AI Agent" → text
   
   Найдите строку:
   "Default timezone: Use HTTP Request tool to fetch user's timezone"
   
   Замените на:
   "Default timezone: Europe/Moscow (or your timezone)"
   ```

3. **Используйте ISO 8601 с timezone:**
   ```
   При создании событий AI должен использовать:
   ✅ "2025-01-02T15:00:00+03:00"
   ❌ "2025-01-02T15:00:00"
   ```

---

### Продвинутая диагностика

#### Проверка логов n8n

**Self-hosted n8n:**

```bash
# Docker
docker logs n8n

# npm
~/.n8n/logs/n8n.log

# Фильтр по ошибкам
docker logs n8n 2>&1 | grep ERROR
```

**n8n Cloud:**

```
Dashboard → Executions → Фильтр: "Failed only"
```

---

#### Тестирование отдельных узлов

1. **Откройте workflow в n8n**

2. **Выберите узел для тестирования**

3. **Нажмите "Execute Node"** (иконка ▶️)

4. **Проверьте входные и выходные данные:**
   ```
   Input → JSON → проверьте входящие данные
   Output → JSON → проверьте результат
   ```

5. **Если ошибка:**
   ```
   Output → Error → читайте сообщение ошибки
   ```

---

#### Debug Mode

**Включение:**

```
n8n → Workflow Settings → Execution Settings
→ Save Execution Progress: ON
→ Save Data On Success Execution: ON
→ Save Data On Error Execution: ON
```

**Использование:**

```
Executions → Выберите execution
→ Нажмите на каждый узел
→ Смотрите детальные данные на каждом шаге
```

---

### Частые ошибки и их коды

| Код ошибки | Причина | Решение |
|------------|---------|---------|
| `401 Unauthorized` | Неверный API ключ или токен | Перепроверьте credentials |
| `403 Forbidden` | Нет прав доступа | Проверьте scopes и permissions |
| `404 Not Found` | Событие/ресурс не найден | Проверьте Event ID |
| `429 Too Many Requests` | Rate limit превышен | Подождите или увеличьте лимиты |
| `500 Internal Server Error` | Проблема на стороне API | Проверьте status pages |
| `ECONNREFUSED` | n8n не может подключиться к API | Проверьте интернет и firewall |
| `ETIMEDOUT` | Timeout соединения | Увеличьте timeout в настройках узла |

---

### Получение помощи

Если проблема не решается:

1. **Соберите информацию:**
   ```
   - Версия n8n: Settings → About
   - Текст ошибки: Executions → Error message
   - Скриншот узла с ошибкой
   - Версия workflow: из файла JSON
   ```

2. **Проверьте документацию:**
   - [n8n Docs](https://docs.n8n.io/)
   - [OpenAI API Docs](https://platform.openai.com/docs/)
   - [Google Calendar API Docs](https://developers.google.com/calendar/api)
   - [Telegram Bot API Docs](https://core.telegram.org/bots/api)

3. **Сообщество:**
   - [n8n Community Forum](https://community.n8n.io/)
   - [GitHub Issues](https://github.com/n8n-io/n8n/issues)

4. **Контакт:**
   - Telegram: [@khanalytiq](https://t.me/khanalytiq)
   - GitHub Issues: [этот репозиторий]

---

## 🇬🇧 English Version

### Common Issues and Solutions

#### 1. Bot Doesn't Respond

**Symptoms:**
- Send message to Telegram but no response
- No "typing..." indicator

**Diagnosis:**

1. **Check workflow status:**
   ```
   n8n → Open workflow → Check status (top right)
   ```
   ✅ Should be: `Active` (green button)
   ❌ If `Inactive` → Click to activate

2. **Check execution logs:**
   ```
   n8n → Executions (bottom left tab) → Recent executions
   ```
   - If no new executions → Telegram webhook issue
   - If executions with errors → check error details

3. **Verify Owner ID:**
   ```
   Node "Owner Verification" → Condition → rightValue: your Telegram ID
   ```
   Get your ID via [@userinfobot](https://t.me/userinfobot)

**Solution:**

```bash
# Try deactivating and reactivating workflow:
1. Click "Active" → "Inactive"
2. Wait 5 seconds
3. Click "Inactive" → "Active"
```

---

#### 2. "Unauthorized" Error

**Symptom:**
```
⛔ Unfortunately, this bot is for personal use only.
```

**Cause:** Your Telegram ID doesn't match ID in Owner Verification

**Solution:**

1. **Get your Telegram ID:**
   - Message [@userinfobot](https://t.me/userinfobot)
   - Copy your ID (e.g., `123456789`)

2. **Update Owner Verification:**
   ```
   Node "Owner Verification" → Rule "boss" → Condition
   rightValue: replace "331119294" with your ID
   ```

3. **Update Memory Buffer:**
   ```
   Node "Simple Memory" → sessionKey
   Replace "331119294" with your ID
   ```

4. **Update Error Notification:**
   ```
   Node "Error Notification" → chatId
   Replace "331119294" with your ID
   ```

5. **Save workflow** (Ctrl+S or Cmd+S)

---

#### 3. OpenAI API Error

**Symptom:**
```
Error: Incorrect API key provided
```

**Possible Causes:**

1. **Invalid API key**

   **Solution:**
   ```
   n8n → Credentials → OpenAI API
   → Verify key starts with "sk-proj-" or "sk-"
   → If incorrect → create new at platform.openai.com/api-keys
   ```

2. **No balance on OpenAI account**

   **Check:**
   ```
   platform.openai.com → Settings → Billing → Check balance
   ```
   
   **Solution:**
   ```
   Add payment method → Add credits (minimum $5)
   ```

3. **Rate limit exceeded**

   **Error:**
   ```
   Error: Rate limit reached for gpt-4-mini
   ```
   
   **Solution:**
   ```
   Wait a few minutes or:
   platform.openai.com → Settings → Limits
   → Increase limits (if available)
   ```

---

#### 4. Google Calendar API Error

**Symptom:**
```
Error: Invalid Credentials
```

**Solutions:**

1. **Credential not authorized**

   ```
   n8n → Find Google Calendar node
   → Credential → Click "Reconnect"
   → Sign in to Google account
   → Allow Calendar access
   ```

2. **Google Calendar API not enabled**

   ```
   1. console.cloud.google.com
   2. Select your project
   3. APIs & Services → Library
   4. Find "Google Calendar API"
   5. Click "Enable"
   ```

---

#### 5. Voice Messages Not Recognized

**Possible Causes:**

1. **File too large**

   **Limit:** 25 MB (Telegram) and 25 MB (OpenAI Whisper)
   
   **Solution:**
   ```
   Send shorter voice messages (up to 2-3 minutes)
   ```

2. **Whisper API error**

   **Solution:**
   ```
   - Check audio quality (not too quiet)
   - Verify OpenAI balance
   - Check Whisper rate limits (50 req/min)
   ```

---

#### 6. Events Created in Wrong Timezone

**Symptom:**
- Create at 3 PM, appears at 12 PM (or vice versa)
- Time shifted by N hours

**Solution:**

1. **Set correct timezone in n8n:**
   ```
   Workflow Settings → Timezone → select your timezone
   E.g., Europe/Moscow, America/New_York, Asia/Tokyo
   ```

2. **Update default timezone in prompt:**
   ```
   Node "Calendar AI Agent" → text
   
   Find line:
   "Default timezone: Use HTTP Request tool to fetch user's timezone"
   
   Replace with:
   "Default timezone: America/New_York (or your timezone)"
   ```

---

### Getting Help

If issue persists:

1. **Gather information:**
   ```
   - n8n version: Settings → About
   - Error text: Executions → Error message
   - Screenshot of node with error
   - Workflow version: from JSON file
   ```

2. **Check documentation:**
   - [n8n Docs](https://docs.n8n.io/)
   - [OpenAI API Docs](https://platform.openai.com/docs/)
   - [Google Calendar API Docs](https://developers.google.com/calendar/api)

3. **Community:**
   - [n8n Community Forum](https://community.n8n.io/)
   - [GitHub Issues](https://github.com/n8n-io/n8n/issues)

4. **Contact:**
   - Telegram: [@khanalytiq](https://t.me/khanalytiq)
   - GitHub Issues: [this repository]

---

### Common Error Codes

| Error Code | Cause | Solution |
|------------|-------|----------|
| `401 Unauthorized` | Invalid API key/token | Recheck credentials |
| `403 Forbidden` | No access rights | Check scopes/permissions |
| `404 Not Found` | Event/resource not found | Check Event ID |
| `429 Too Many Requests` | Rate limit exceeded | Wait or increase limits |
| `500 Internal Server Error` | API-side issue | Check status pages |
| `ETIMEDOUT` | Connection timeout | Increase timeout in settings |


# 🛠️ Setup Guide / Инструкция по настройке

[🇬🇧 English](#-english-version) | [🇷🇺 Русский](#-русская-версия)

---

## 🇬🇧 English Version

### Prerequisites

Before starting, ensure you have:
- ✅ Installed [n8n](https://n8n.io/) (version 1.0+)
- ✅ Active [OpenAI](https://platform.openai.com/) account with API key
- ✅ [Google](https://google.com/) account for Calendar API
- ✅ Telegram account to create a bot

### Step 1: Install n8n

#### Option A: Docker (recommended)

```bash
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  docker.n8n.io/n8nio/n8n
```

#### Option B: npm

```bash
npm install n8n -g
n8n start
```

#### Option C: n8n Cloud

Sign up at [n8n.cloud](https://n8n.cloud/) and get a ready instance.

After launch, open browser: `http://localhost:5678`

---

### Step 2: Create Telegram Bot

1. **Open Telegram** and find [@BotFather](https://t.me/BotFather)

2. **Create new bot:**
   ```
   /newbot
   ```

3. **Follow instructions:**
   - Enter bot name (e.g., `My Calendar Assistant`)
   - Enter bot username (e.g., `my_calendar_bot`)

4. **Save the token:**
   ```
   Token: 1234567890:ABCdefGHIjklMNOpqrsTUVwxyz
   ```

5. **Get your Telegram ID:**
   - Message [@userinfobot](https://t.me/userinfobot)
   - Copy your ID (e.g., `331119294`)

---

### Step 3: Get OpenAI API Key

1. **Go to** [platform.openai.com](https://platform.openai.com/)

2. **Sign in** or create account

3. **Navigate to API Keys:**
   - Click profile → "View API Keys"
   - Or direct link: [platform.openai.com/api-keys](https://platform.openai.com/api-keys)

4. **Create new key:**
   - Click "Create new secret key"
   - Name it (e.g., `n8n-calendar-bot`)
   - Copy key: `sk-proj-...`

5. **Add billing:**
   - Minimum $5 to start
   - GPT-4.1-mini costs ~$0.15 per 1M tokens (input)

⚠️ **Important:** Save the key securely. You won't see it again!

---

### Step 4: Setup Google Calendar API

#### 4.1 Create Google Cloud Project

1. **Go to** [console.cloud.google.com](https://console.cloud.google.com/)

2. **Create new project:**
   - Click project dropdown (top)
   - "New Project"
   - Name: `Calendar Bot`
   - Click "Create"

#### 4.2 Enable Google Calendar API

1. **In sidebar** select "APIs & Services" → "Library"

2. **Search for** "Google Calendar API"

3. **Click** "Enable"

#### 4.3 Create OAuth2 Credentials

1. **Go to** "APIs & Services" → "Credentials"

2. **Configure OAuth consent screen:**
   - Click "Configure Consent Screen"
   - Select "External"
   - Fill required fields:
     - App name: `Calendar Bot`
     - User support email: your email
     - Developer contact: your email
   - Click "Save and Continue"

3. **Add scopes:**
   - Click "Add or Remove Scopes"
   - Find and add:
     - `https://www.googleapis.com/auth/calendar`
     - `https://www.googleapis.com/auth/calendar.events`
   - Click "Update" → "Save and Continue"

4. **Add test users:**
   - Click "Add Users"
   - Enter your Gmail: `your.email@gmail.com`
   - Click "Save and Continue"

5. **Create OAuth2 Client ID:**
   - Return to "Credentials"
   - Click "Create Credentials" → "OAuth client ID"
   - Application type: "Web application"
   - Name: `n8n Calendar Bot`
   - Authorized redirect URIs:
     ```
     http://localhost:5678/rest/oauth2-credential/callback
     ```
   - Click "Create"

6. **Save credentials:**
   - Client ID: `xxxxx.apps.googleusercontent.com`
   - Client Secret: `GOCSPX-xxxxx`

---

### Step 5: Import Workflow to n8n

1. **Download workflow file:**
   ```bash
   git clone https://github.com/yourusername/google-calendar-ai-tg-assistant.git
   cd google-calendar-ai-tg-assistant
   ```

2. **Open n8n** in browser: `http://localhost:5678`

3. **Import workflow:**
   - Click menu "☰" (top left)
   - Select "Import from File"
   - Choose file: `💀 - Google Calendar + TG + AI assistant v2.json`
   - Click "Import"

---

### Step 6: Configure Credentials in n8n

#### 6.1 Telegram API Credentials

1. **In workflow** find any Telegram node (e.g., "Telegram Trigger")

2. **Click Credential field:**
   - "Select Credential" → "+ Create New"

3. **Fill in:**
   - Credential Name: `@tgcalobot` (or your name)
   - Access Token: `<your token from BotFather>`

4. **Save:** "Save"

5. **Apply to all Telegram nodes**

#### 6.2 OpenAI API Credentials

1. **Find node** "OpenAI Chat Model" or "Transcribe a recording"

2. **Create new Credential:**
   - "Select Credential" → "+ Create New"

3. **Fill in:**
   - Credential Name: `OpenAI Account`
   - API Key: `sk-proj-xxxxx`

4. **Save and apply** to all OpenAI nodes

#### 6.3 Google Calendar OAuth2 Credentials

1. **Find node** "Create an event in Google Calendar"

2. **Create new Credential:**
   - "Select Credential" → "+ Create New"

3. **Fill in:**
   - Credential Name: `Google Calendar - Your Email`
   - Client ID: `<from Google Cloud Console>`
   - Client Secret: `<from Google Cloud Console>`

4. **Authorize:**
   - Click "Connect my account"
   - Sign in to Google account
   - Allow Calendar access

5. **Save and apply** to all Google Calendar nodes

---

### Step 7: Configure Owner ID

Replace owner ID with yours in all necessary places:

#### 7.1 Owner Verification (Switch node)

1. **Open node** "Owner Verification"

2. **Find condition** with ID `331119294`

3. **Replace with your Telegram ID** in both conditions

#### 7.2 Simple Memory (Memory Buffer node)

1. **Open node** "Simple Memory"

2. **Find field** `sessionKey`

3. **Replace** `331119294` with your Telegram ID

#### 7.3 Error Notification (Telegram node)

1. **Open node** "Error Notification"

2. **Find field** `chatId`

3. **Replace** `331119294` with your Telegram ID

---

### Step 8: Testing

1. **Activate workflow:**
   - Top right corner toggle "Inactive" → "Active"

2. **Open your bot** in Telegram

3. **Send test message:**
   ```
   Hello!
   ```

4. **Check response:**
   - Bot should respond with greeting
   - If not — check logs in n8n ("Executions" tab)

5. **Test event creation:**
   ```
   Create a meeting tomorrow at 3 PM
   ```

6. **Check Google Calendar:**
   - Event should appear in your calendar

---

### 🎉 Done!

Your AI Calendar Assistant is ready to use!

**Test commands:**
- "Create meeting with John tomorrow at 2 PM"
- "What do I have this week?"
- "Move meeting to 4 PM"
- "Delete Monday's meeting"
- 🎤 Send a voice message

---

### 🐛 Troubleshooting

#### Bot doesn't respond

**Problem:** Sent message but no response

**Solution:**
1. Check if workflow is active (green "Active" button)
2. Check logs: "Executions" tab in n8n
3. Ensure your Telegram ID is correct in "Owner Verification"
4. Verify Telegram webhook is set (should be automatic)

#### "Unauthorized" error

**Problem:** Bot responds "Unfortunately, this bot is for personal use only"

**Solution:**
- You forgot to replace Owner ID with yours
- Check "Owner Verification" node and replace `331119294`

#### OpenAI API error

**Problem:** "Error: Incorrect API key provided"

**Solution:**
1. Check API key in credentials
2. Ensure you have balance on OpenAI account
3. Verify key is active (not revoked)

#### Google Calendar error

**Problem:** "Error: Invalid credentials"

**Solution:**
1. Re-authorize Google Calendar credential
2. Check that API is enabled in Google Cloud Console
3. Ensure you added yourself as "test user" in OAuth consent screen

---

### 📞 Support

If you have questions or need help:
- 📧 Open an issue on GitHub
- 💬 Contact: [@khanalytiq](https://t.me/khanalytiq)

**⭐ If this project is useful, please star it!**

---

## 🇷🇺 Русская версия

### Предварительные требования

Перед началом убедитесь, что у вас есть:
- ✅ Установленный [n8n](https://n8n.io/) (версия 1.0+)
- ✅ Активный аккаунт [OpenAI](https://platform.openai.com/) с API ключом
- ✅ Аккаунт [Google](https://google.com/) для работы с Calendar API
- ✅ Telegram аккаунт для создания бота

### Шаг 1: Установка n8n

#### Вариант A: Docker (рекомендуется)

```bash
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  docker.n8n.io/n8nio/n8n
```

#### Вариант B: npm

```bash
npm install n8n -g
n8n start
```

#### Вариант C: n8n Cloud

Зарегистрируйтесь на [n8n.cloud](https://n8n.cloud/) и получите готовый инстанс.

После запуска откройте браузер: `http://localhost:5678`

---

### Шаг 2: Создание Telegram бота

1. **Откройте Telegram** и найдите [@BotFather](https://t.me/BotFather)

2. **Создайте нового бота:**
   ```
   /newbot
   ```

3. **Следуйте инструкциям:**
   - Введите имя бота (например: `My Calendar Assistant`)
   - Введите username бота (например: `my_calendar_bot`)

4. **Сохраните токен:**
   ```
   Token: 1234567890:ABCdefGHIjklMNOpqrsTUVwxyz
   ```

5. **Настройте команды (опционально):**
   ```
   /setcommands
   ```
   Добавьте описание команд:
   ```
   help - Показать справку
   start - Начать работу с ботом
   ```

6. **Узнайте свой Telegram ID:**
   - Напишите боту [@userinfobot](https://t.me/userinfobot)
   - Скопируйте ваш ID (например: `331119294`)

---

### Шаг 3: Получение OpenAI API ключа

1. **Перейдите на** [platform.openai.com](https://platform.openai.com/)

2. **Войдите** или создайте аккаунт

3. **Перейдите в раздел API Keys:**
   - Нажмите на профиль → "View API Keys"
   - Или прямая ссылка: [platform.openai.com/api-keys](https://platform.openai.com/api-keys)

4. **Создайте новый ключ:**
   - Нажмите "Create new secret key"
   - Дайте имя (например: `n8n-calendar-bot`)
   - Скопируйте ключ: `sk-proj-...`

5. **Пополните баланс:**
   - Минимум $5 для начала работы
   - GPT-4.1-mini стоит ~$0.15 за 1M токенов (input)

⚠️ **Важно:** Сохраните ключ в надёжном месте. Вы не сможете увидеть его снова!

---

### Шаг 4: Настройка Google Calendar API

#### 4.1 Создание проекта в Google Cloud

1. **Перейдите на** [console.cloud.google.com](https://console.cloud.google.com/)

2. **Создайте новый проект:**
   - Нажмите на выпадающий список проектов (вверху)
   - "New Project"
   - Имя: `Calendar Bot`
   - Нажмите "Create"

#### 4.2 Включение Google Calendar API

1. **В боковом меню** выберите "APIs & Services" → "Library"

2. **Найдите** "Google Calendar API"

3. **Нажмите** "Enable"

#### 4.3 Создание OAuth2 credentials

1. **Перейдите в** "APIs & Services" → "Credentials"

2. **Настройте OAuth consent screen:**
   - Нажмите "Configure Consent Screen"
   - Выберите "External" (если у вас нет Google Workspace)
   - Заполните обязательные поля:
     - App name: `Calendar Bot`
     - User support email: ваш email
     - Developer contact: ваш email
   - Нажмите "Save and Continue"

3. **Добавьте scopes:**
   - Нажмите "Add or Remove Scopes"
   - Найдите и добавьте:
     - `https://www.googleapis.com/auth/calendar`
     - `https://www.googleapis.com/auth/calendar.events`
   - Нажмите "Update" → "Save and Continue"

4. **Добавьте тестовых пользователей:**
   - Нажмите "Add Users"
   - Введите ваш Gmail: `your.email@gmail.com`
   - Нажмите "Save and Continue"

5. **Создайте OAuth2 Client ID:**
   - Вернитесь в "Credentials"
   - Нажмите "Create Credentials" → "OAuth client ID"
   - Application type: "Web application"
   - Name: `n8n Calendar Bot`
   - Authorized redirect URIs:
     ```
     http://localhost:5678/rest/oauth2-credential/callback
     ```
     (Или ваш домен если используете n8n cloud)
   - Нажмите "Create"

6. **Сохраните credentials:**
   - Client ID: `xxxxx.apps.googleusercontent.com`
   - Client Secret: `GOCSPX-xxxxx`

---

### Шаг 5: Импорт workflow в n8n

1. **Скачайте файл workflow:**
   ```bash
   git clone https://github.com/yourusername/google-calendar-ai-tg-assistant.git
   cd google-calendar-ai-tg-assistant
   ```

2. **Откройте n8n** в браузере: `http://localhost:5678`

3. **Импортируйте workflow:**
   - Нажмите на меню "☰" (вверху слева)
   - Выберите "Import from File"
   - Выберите файл: `💀 - Google Calendar + TG + AI assistant v2.json`
   - Нажмите "Import"

---

### Шаг 6: Настройка Credentials в n8n

#### 6.1 Telegram API Credentials

1. **В workflow** найдите любой узел с Telegram (например, "Telegram Trigger")

2. **Нажмите на поле Credential:**
   - "Select Credential" → "+ Create New"

3. **Заполните данные:**
   - Credential Name: `@tgcalobot` (или ваше имя)
   - Access Token: `<ваш токен из BotFather>`

4. **Сохраните:** "Save"

5. **Примените ко всем узлам Telegram:**
   - n8n предложит обновить все узлы
   - Нажмите "Update all"

#### 6.2 OpenAI API Credentials

1. **Найдите узел** "OpenAI Chat Model" или "Transcribe a recording"

2. **Создайте новый Credential:**
   - "Select Credential" → "+ Create New"

3. **Заполните:**
   - Credential Name: `OpenAI Account`
   - API Key: `sk-proj-xxxxx`

4. **Сохраните и примените** ко всем OpenAI узлам

#### 6.3 Google Calendar OAuth2 Credentials

1. **Найдите узел** "Create an event in Google Calendar"

2. **Создайте новый Credential:**
   - "Select Credential" → "+ Create New"

3. **Заполните данные:**
   - Credential Name: `Google Calendar - Your Email`
   - Client ID: `<из Google Cloud Console>`
   - Client Secret: `<из Google Cloud Console>`

4. **Авторизуйтесь:**
   - Нажмите "Connect my account"
   - Войдите в Google аккаунт
   - Разрешите доступ к Calendar

5. **Сохраните и примените** ко всем Google Calendar узлам

---

### Шаг 7: Настройка Owner ID

Замените ID владельца на ваш во всех нужных местах:

#### 7.1 Owner Verification (узел Switch)

1. **Откройте узел** "Owner Verification"

2. **Найдите условие** с ID `331119294`

3. **Замените на ваш Telegram ID** в обоих условиях:
   - `leftValue`: `={{ $json.message.chat.id }}`
   - `rightValue`: `<ваш ID>` (например: `123456789`)

#### 7.2 Simple Memory (узел Memory Buffer)

1. **Откройте узел** "Simple Memory"

2. **Найдите поле** `sessionKey`

3. **Замените** `331119294` на ваш Telegram ID

#### 7.3 Error Notification (узел Telegram)

1. **Откройте узел** "Error Notification"

2. **Найдите поле** `chatId`

3. **Замените** `331119294` на ваш Telegram ID

---

### Шаг 8: Тестирование

1. **Активируйте workflow:**
   - В правом верхнем углу переключите "Inactive" → "Active"

2. **Откройте вашего бота** в Telegram

3. **Отправьте тестовое сообщение:**
   ```
   Привет!
   ```

4. **Проверьте ответ:**
   - Бот должен ответить приветствием
   - Если нет — проверьте логи в n8n (вкладка "Executions")

5. **Протестируйте создание события:**
   ```
   Создай встречу завтра в 15:00
   ```

6. **Проверьте Google Calendar:**
   - Событие должно появиться в вашем календаре

---

### Шаг 9: Настройка часового пояса (опционально)

По умолчанию workflow автоматически определяет часовой пояс, но вы можете настроить его вручную:

1. **Откройте узел** "Calendar AI Agent"

2. **Найдите в промпте** строку про часовой пояс

3. **Измените на ваш:**
   ```
   Default timezone: Europe/Moscow
   ```
   (см. список: [timezones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones))

---

### 🎉 Готово!

Ваш AI-ассистент для календаря готов к работе!

**Полезные команды для тестирования:**
- "Создай встречу с Иваном завтра в 14:00"
- "Что у меня на этой неделе?"
- "Перенеси встречу на 16:00"
- "Удали встречу в понедельник"
- 🎤 Отправьте голосовое сообщение

---

### 🐛 Решение проблем

#### Бот не отвечает

**Проблема:** Отправили сообщение, но нет ответа

**Решение:**
1. Проверьте, активен ли workflow (зелёная кнопка "Active")
2. Проверьте логи: вкладка "Executions" в n8n
3. Убедитесь, что ваш Telegram ID правильно указан в "Owner Verification"
4. Проверьте, что webhook Telegram настроен (должен быть автоматически)

#### Ошибка "Unauthorized"

**Проблема:** Бот отвечает "К сожалению, этот бот только для личного использования"

**Решение:**
- Вы забыли заменить Owner ID на свой
- Проверьте узел "Owner Verification" и замените `331119294`

#### Ошибка OpenAI API

**Проблема:** "Error: Incorrect API key provided"

**Решение:**
1. Проверьте API ключ в credentials
2. Убедитесь, что у вас есть баланс на аккаунте OpenAI
3. Проверьте, что ключ активен (не отозван)

#### Ошибка Google Calendar

**Проблема:** "Error: Invalid credentials"

**Решение:**
1. Переавторизуйтесь в Google Calendar credential
2. Проверьте, что API включен в Google Cloud Console
3. Убедитесь, что вы добавили себя как "test user" в OAuth consent screen

#### Голосовые сообщения не работают

**Проблема:** Голосовые сообщения не распознаются

**Решение:**
1. Проверьте, что узел "Get a file" правильно настроен
2. Убедитесь, что OpenAI API credential действителен
3. Проверьте, что у вас достаточно баланса для Whisper API
4. Максимальный размер файла: 20 МБ

---

### 📊 Мониторинг и логи

#### Просмотр executions

1. Откройте workflow в n8n
2. Перейдите на вкладку "Executions" (внизу слева)
3. Выберите execution для просмотра деталей

#### Debugging

Для отладки workflow:
1. Откройте узел, который хотите проверить
2. Нажмите "Test step" (иконка ▶️)
3. Проверьте входные и выходные данные

---

### 🔄 Обновление workflow

Когда выходит новая версия:

```bash
cd google-calendar-ai-tg-assistant
git pull origin main
```

Затем:
1. Деактивируйте старый workflow
2. Импортируйте новую версию
3. Перенесите credentials
4. Активируйте новый workflow

---

### 📞 Поддержка

Если у вас есть вопросы или нужна помощь:
- 📧 Откройте issue на GitHub
- 💬 Контакт: [@khanalytiq](https://t.me/khanalytiq)

**⭐ Если проект оказался полезным, поставьте звезду!**

# 🚀 Roadmap / Дорожная карта

[🇬🇧 English](#-english-version) | [🇷🇺 Русский](#-русская-версия)

---

## 🇬🇧 English Version

### Current Version: v2.0.0

Features:
- ✅ Basic calendar operations (CRUD)
- ✅ Voice messages (Whisper)
- ✅ Context memory (10 messages)
- ✅ Automatic timezone detection
- ✅ Natural language processing (GPT-4.1-mini)
- ✅ Error handling with notifications

---

### 🎯 Planned Features

#### v2.1.0 - Q1 2025 (Jan-Mar)

**UX Improvements:**
- [ ] Inline buttons in Telegram for action confirmation
- [ ] Markdown formatting in responses
- [ ] Image sending (schedule visualization)
- [ ] Event preview before creation

**Calendar Features:**
- [ ] Recurring events support
- [ ] Attendees invitations
- [ ] Multiple calendars support
- [ ] Color labels for event categories
- [ ] File attachments to events

**AI Improvements:**
- [ ] Smart time suggestions (free slots analysis)
- [ ] Automatic event categorization
- [ ] Priority recognition (important/regular meetings)
- [ ] Event duration prediction based on history

---

#### v2.2.0 - Q2 2025 (Apr-Jun)

**Integrations:**
- [ ] Zoom - automatic meeting links
- [ ] Google Meet - video call integration
- [ ] Slack - upcoming event notifications
- [ ] Notion - sync with Notion Calendar
- [ ] Gmail - email invitations

**Reminders:**
- [ ] Custom reminders (X minutes/hours/days before)
- [ ] Smart reminders (considering traffic, weather)
- [ ] Multi-channel reminders (Telegram, Email, SMS)
- [ ] Meeting preparation briefs

**Analytics:**
- [ ] Time statistics (how time is spent)
- [ ] Productivity reports
- [ ] Workload visualization by days/weeks
- [ ] Data export (CSV, PDF)

---

#### v2.3.0 - Q3 2025 (Jul-Sep)

**Multi-user Support:**
- [ ] Multiple users support
- [ ] Per-user calendar separation
- [ ] Shared calendars (collaborative events)
- [ ] Permissions and roles (admin, user, viewer)

**NLP Improvements:**
- [ ] Multi-language support (English, Spanish, German)
- [ ] Complex temporal constructions understanding
- [ ] Relative dates processing ("two weeks from Tuesday")
- [ ] Context understanding ("same meeting next week")

**Automation:**
- [ ] Automatic event creation from emails
- [ ] Invitation parsing (ICS files)
- [ ] Smart scheduling (AI suggests optimal time)
- [ ] Automatic focus time blocking

---

#### v3.0.0 - Q4 2025 (Oct-Dec)

**Advanced AI:**
- [ ] RAG (Retrieval-Augmented Generation) for context
- [ ] Fine-tuned model for calendar planning
- [ ] Personal AI assistant (learns your habits)
- [ ] Proactive suggestions (AI optimizes schedule)

**Enterprise Features:**
- [ ] Team calendars
- [ ] Resource booking (meeting rooms, equipment)
- [ ] Approval workflows
- [ ] Corporate system integration (MS Exchange, Outlook)

**Security:**
- [ ] End-to-end encryption for messages
- [ ] Multi-factor authentication
- [ ] Audit logs
- [ ] GDPR compliance mode

---

### 💡 Future Ideas

**AI-powered features:**
- 🤖 Automatic meeting preparation (participant research)
- 🤖 Meeting agenda generation
- 🤖 Automatic meeting transcription + summary
- 🤖 Intelligent vacation planning
- 🤖 Conflict detection (overlapping events, overwork)

**Integrations:**
- 📧 Microsoft Outlook Calendar
- 📋 Trello / Asana / Jira (tasks → events)
- 🚗 Uber / Lyft (automatic taxi before meeting)
- 🍽️ OpenTable (restaurant booking)
- ✈️ Google Flights (trip planning)

**Mobile Apps:**
- 📱 Native iOS app (SwiftUI)
- 📱 Native Android app (Kotlin)
- ⌚ Apple Watch / Wear OS support

**Platforms:**
- 💬 WhatsApp bot
- 💬 Discord bot
- 💬 Slack app
- 🌐 Web interface (Progressive Web App)

---

### 🤝 How to Suggest a Feature

Have an idea for a new feature?

1. **Open GitHub Issue:**
   ```
   Title: [Feature Request] Feature Name
   
   Description:
   - What is this feature?
   - What problem does it solve?
   - How do you envision it working?
   - Are there examples in other products?
   ```

2. **Vote for existing suggestions:**
   ```
   GitHub → Issues → Label: "enhancement"
   → Give 👍 to those you need
   ```

3. **Join the discussion:**
   ```
   Comment on Issues with your ideas and use cases
   ```

---

### 📊 Development Priorities

Features are implemented based on:

1. **Impact** - how many users it affects
2. **Effort** - implementation time
3. **Value** - UX improvement
4. **Votes** - 👍 count in GitHub Issues

**High Priority:**
- Features requested by many users
- Critical bugs and security issues
- Performance improvements

**Medium Priority:**
- New integrations
- UI/UX improvements
- Additional languages

**Low Priority:**
- Nice-to-have features
- Experimental capabilities
- Specific use cases

---

### 🐛 Known Issues

#### v2.0.0

**Limitations:**
- Maximum 10 events per request (Google Calendar API limit)
- Voice messages: only Russian and English
- Memory buffer: only last 10 messages
- Timezone detection: sometimes requires manual specification

**Planned Fixes:**
- v2.1: Pagination for large event lists
- v2.1: More languages for voice support
- v2.2: Configurable memory buffer size
- v2.1: Improved timezone detection logic

---

## 🇷🇺 Русская версия

### Текущая версия: v2.0.0

Функционал:
- ✅ Базовые операции с календарём (CRUD)
- ✅ Голосовые сообщения (Whisper)
- ✅ Контекстная память (10 сообщений)
- ✅ Автоопределение часового пояса
- ✅ Обработка естественного языка (GPT-4.1-mini)
- ✅ Обработка ошибок с уведомлениями

---

### 🎯 Планируемые функции

#### v2.1.0 - Q1 2025 (Январь-Март)

**Улучшения UX:**
- [ ] Inline кнопки в Telegram для подтверждения действий
- [ ] Форматирование ответов с использованием Markdown
- [ ] Отправка изображений (визуализация расписания)
- [ ] Предпросмотр событий перед созданием

**Календарные функции:**
- [ ] Поддержка повторяющихся событий (recurrence)
- [ ] Приглашение участников (attendees)
- [ ] Поддержка нескольких календарей
- [ ] Цветные метки для категорий событий
- [ ] Прикрепление файлов к событиям

**AI улучшения:**
- [ ] Умное предложение времени (анализ свободных слотов)
- [ ] Автоматическая категоризация событий
- [ ] Распознавание приоритетов (важные/обычные встречи)
- [ ] Предсказание длительности событий на основе истории

---

#### v2.2.0 - Q2 2025 (Апрель-Июнь)

**Интеграции:**
- [ ] Zoom - автоматическое создание ссылок на встречи
- [ ] Google Meet - интеграция видео-звонков
- [ ] Slack - уведомления о предстоящих событиях
- [ ] Notion - синхронизация с Notion Calendar
- [ ] Gmail - отправка email-приглашений

**Напоминания:**
- [ ] Кастомные напоминания (за X минут/часов/дней)
- [ ] Умные напоминания (учитывая пробки, погоду)
- [ ] Напоминания в разных каналах (Telegram, Email, SMS)
- [ ] Предварительная подготовка к встречам (briefs)

**Аналитика:**
- [ ] Статистика по времени (сколько времени на что уходит)
- [ ] Отчёты по продуктивности
- [ ] Визуализация загруженности по дням/неделям
- [ ] Экспорт данных (CSV, PDF)

---

#### v2.3.0 - Q3 2025 (Июль-Сентябрь)

**Multi-user поддержка:**
- [ ] Поддержка нескольких пользователей
- [ ] Разделение календарей по пользователям
- [ ] Shared календари (совместные события)
- [ ] Permissions и roles (admin, user, viewer)

**NLP улучшения:**
- [ ] Поддержка нескольких языков (English, Spanish, German)
- [ ] Понимание сложных временных конструкций
- [ ] Обработка относительных дат ("через две недели во вторник")
- [ ] Понимание контекста ("ту же встречу на следующей неделе")

**Автоматизация:**
- [ ] Автоматическое создание событий из email
- [ ] Парсинг приглашений (ICS файлы)
- [ ] Smart scheduling (AI предлагает оптимальное время)
- [ ] Автоматическая блокировка focus time

---

#### v3.0.0 - Q4 2025 (Октябрь-Декабрь)

**Продвинутый AI:**
- [ ] RAG (Retrieval-Augmented Generation) для контекста
- [ ] Fine-tuned модель специально для календарного планирования
- [ ] Персональный AI ассистент (изучает ваши привычки)
- [ ] Proactive suggestions (AI сам предлагает оптимизацию расписания)

**Enterprise функции:**
- [ ] Team календари
- [ ] Resource booking (переговорные, оборудование)
- [ ] Approval workflows (согласование встреч)
- [ ] Integration с корп. системами (MS Exchange, Outlook)

**Безопасность:**
- [ ] End-to-end encryption для сообщений
- [ ] Multi-factor authentication
- [ ] Audit logs (кто что изменил)
- [ ] GDPR compliance режим

---

### 💡 Идеи для будущих версий

**AI-powered features:**
- 🤖 Автоматическая подготовка к встречам (поиск информации о участниках)
- 🤖 Генерация agenda для встреч
- 🤖 Автоматическая расшифровка встреч (transcription + summary)
- 🤖 Интеллектуальное планирование отпусков
- 🤖 Конфликт-детекция (наложение событий, переработки)

**Интеграции:**
- 📧 Microsoft Outlook Calendar
- 📋 Trello / Asana / Jira (задачи → события)
- 🚗 Uber / Lyft (автоматический заказ такси перед встречей)
- 🍽️ OpenTable (бронирование ресторанов)
- ✈️ Google Flights (планирование поездок)

**Мобильные приложения:**
- 📱 Native iOS app (SwiftUI)
- 📱 Native Android app (Kotlin)
- ⌚ Apple Watch / Wear OS поддержка

**Платформы:**
- 💬 WhatsApp bot
- 💬 Discord bot
- 💬 Slack app
- 🌐 Web interface (Progressive Web App)

---

### 🤝 Как внести предложение

Есть идея для новой функции?

1. **Откройте Issue на GitHub:**
   ```
   Title: [Feature Request] Название функции
   
   Описание:
   - Что это за функция?
   - Какую проблему она решает?
   - Как вы представляете её работу?
   - Есть ли примеры в других продуктах?
   ```

2. **Голосуйте за существующие предложения:**
   ```
   GitHub → Issues → Label: "enhancement"
   → Поставьте 👍 на те, которые вам нужны
   ```

3. **Присоединяйтесь к обсуждению:**
   ```
   Комментируйте Issues с вашими идеями и use cases
   ```

---

### 📊 Приоритеты разработки

Функции реализуются по следующим критериям:

1. **Impact** - сколько пользователей это затронет
2. **Effort** - сколько времени займёт реализация
3. **Value** - насколько это улучшит UX
4. **Votes** - сколько 👍 в GitHub Issues

**Высокий приоритет:**
- Функции, запрошенные многими пользователями
- Критические баги и проблемы безопасности
- Улучшения производительности

**Средний приоритет:**
- Новые интеграции
- UI/UX улучшения
- Дополнительные языки

**Низкий приоритет:**
- Nice-to-have функции
- Экспериментальные возможности
- Специфичные use cases

---

### 🐛 Known Issues (Известные проблемы)

#### v2.0.0

**Ограничения:**
- Максимум 10 событий в одном запросе (Google Calendar API limit)
- Голосовые сообщения: только русский и английский
- Memory buffer: только последние 10 сообщений
- Timezone detection: иногда требует ручного указания

**Планируемые исправления:**
- v2.1: Pagination для больших списков событий
- v2.1: Поддержка больше языков для голоса
- v2.2: Настраиваемый размер memory buffer
- v2.1: Улучшенная логика определения timezone

---

**⭐ Star this project to follow updates!**

# 🤝 Contributing Guide / Руководство по участию

[🇬🇧 English](#-english-version) | [🇷🇺 Русский](#-русская-версия)

---

## 🇬🇧 English Version

Thank you for your interest in the project! We welcome any contribution - from fixing typos to adding new features.

### 🎯 How You Can Help

**For Everyone:**
- 🐛 Report bugs and issues
- 💡 Suggest new features
- 📝 Improve documentation
- 🌍 Add translations
- ⭐ Star the project

**For Developers:**
- 🔧 Fix bugs
- ✨ Implement new features
- 🧪 Write tests
- 📊 Optimize performance
- 🔒 Improve security

---

### 🚀 Getting Started

#### 1. Fork and Clone

```bash
# Fork the project on GitHub (click "Fork" button)

# Clone your fork
git clone https://github.com/your-username/google-calendar-ai-tg-assistant.git
cd google-calendar-ai-tg-assistant

# Add upstream remote
git remote add upstream https://github.com/original-author/google-calendar-ai-tg-assistant.git
```

#### 2. Setup Environment

```bash
# Install n8n (if not installed)
npm install n8n -g

# Start n8n
n8n start

# Import workflow
# n8n → Import from File → select JSON file
```

#### 3. Create Branch

```bash
# Update main branch
git checkout main
git pull upstream main

# Create feature branch
git checkout -b feature/amazing-feature
# or
git checkout -b fix/bug-description
```

---

### 📝 Development Guidelines

#### Workflow Changes

**When modifying n8n workflow:**

1. ✅ Test all changes locally
2. ✅ Document new nodes/features
3. ✅ Update `docs/architecture.md` if structure changes
4. ✅ Export workflow without credentials
5. ✅ Verify JSON is valid

**Export workflow:**

```
n8n → Workflow → Menu (☰) → Download
→ Save as: 💀 - Google Calendar + TG + AI assistant v2.json
```

**⚠️ Important:** Remove all credentials before export:
```
Settings → Workflow → Remove sensitive data
```

#### Commits

**Commit message format:**

```
type: brief description

[optional] Detailed description

[optional] Fixes #issue-number
```

**Types:**
- `feat`: new feature
- `fix`: bug fix
- `docs`: documentation changes
- `style`: formatting, typos
- `refactor`: code refactoring
- `test`: adding tests
- `chore`: dependency updates, configuration

**Examples:**

```bash
git commit -m "feat: add recurring events support"

git commit -m "fix: timezone detection issue

Timezone is now correctly detected via HTTP Request node
instead of using default value from prompt.

Fixes #42"

git commit -m "docs: update examples in README"
```

---

### 🐛 Reporting Bugs

**Before creating Issue:**

1. ✅ Check if bug hasn't been reported
2. ✅ Ensure you're using latest version
3. ✅ Try reproducing on clean install

**Issue Template:**

```markdown
## 🐛 Bug Description

Clear and concise description of the problem.

## 📋 Steps to Reproduce

1. Open workflow
2. Send message '...'
3. Click '...'
4. See error

## ✅ Expected Behavior

What should have happened.

## ❌ Actual Behavior

What actually happened.

## 🖥️ Environment

- **n8n version:** 1.x.x
- **OS:** macOS 14.1 / Ubuntu 22.04 / Windows 11
- **Node.js version:** 18.x.x
- **Installation type:** Docker / npm / n8n Cloud

## 📸 Screenshots

If applicable, add screenshots.

## 📝 Logs

```
Paste relevant logs here
```

## 🔍 Additional Context

Any other information about the problem.
```

---

### 💡 Suggesting Features

**Feature Request Template:**

```markdown
## ✨ Feature Description

Clear and concise description of what you want to add.

## 🎯 Problem

What problem does this solve?
Example: "It's inconvenient to [...] because [...]"

## 💡 Proposed Solution

How do you envision the implementation?

## 🔄 Alternatives

What alternative solutions have you considered?

## 📋 Use Cases

Specific usage examples:

1. As a user, I want to [...]
2. This will allow me to [...]

## 🎨 Mockups / Examples

If available, attach UI examples or code.

## 🚀 Priority

- [ ] Nice to have
- [ ] Important
- [ ] Critical

## 💬 Additional Information

Any other information or context.
```

---

### 🔄 Pull Request Process

#### 1. Before Creating PR

**Checklist:**

- [ ] Code works and is tested
- [ ] Documentation updated
- [ ] Commit messages follow guidelines
- [ ] Branch updated with upstream/main
- [ ] No conflicts
- [ ] JSON workflow is valid
- [ ] Credentials removed from export

#### 2. Creating Pull Request

```bash
# Push to your fork
git push origin feature/amazing-feature

# Create PR on GitHub
# base: main ← compare: feature/amazing-feature
```

**PR Template:**

```markdown
## 📝 Description

Brief description of changes.

## 🔗 Related Issues

Closes #issue-number (if applicable)

## 🎯 Type of Change

- [ ] 🐛 Bug fix (non-breaking change)
- [ ] ✨ New feature (non-breaking change)
- [ ] 💥 Breaking change
- [ ] 📝 Documentation update

## ✅ Checklist

- [ ] Code tested and works
- [ ] Documentation updated
- [ ] Commit messages correct
- [ ] No conflicts with main
- [ ] Credentials removed from workflow
- [ ] Usage examples added (if new feature)

## 📸 Screenshots / Examples

If applicable, add screenshots or usage examples.

## 🧪 How Tested

Describe how you tested the changes:

1. Step 1
2. Step 2
3. Result

## 💬 Additional Information

Any other information for reviewers.
```

#### 3. Code Review

**Process:**

1. Maintainer will review your PR
2. Changes may be requested
3. Make changes and push to same branch
4. After approval, PR will be merged

**Response time:**
- Usually: 1-3 days
- For urgent (security): 24 hours

---

### 🧪 Testing

#### Manual Testing

**Basic test scenario:**

```
1. ✅ Event creation
   Command: "Create meeting tomorrow at 3 PM"
   Expected: Event created in Google Calendar

2. ✅ View events
   Command: "What do I have this week?"
   Expected: List of all events

3. ✅ Update event
   Command: "Move meeting to 4 PM"
   Expected: Event time changed

4. ✅ Delete event
   Command: "Delete tomorrow's meeting"
   Expected: Event deleted

5. ✅ Voice message
   Action: Send voice command
   Expected: Transcription and execution

6. ✅ Error handling
   Action: Invalid command
   Expected: Clear error message
```

#### Testing New Features

**When adding a new feature:**

1. Positive scenarios (happy path)
2. Negative scenarios (errors, edge cases)
3. Boundary conditions (empty values, large data)
4. Backward compatibility

---

### 📚 Resources

**Documentation:**
- [n8n Documentation](https://docs.n8n.io/)
- [Telegram Bot API](https://core.telegram.org/bots/api)
- [Google Calendar API](https://developers.google.com/calendar/api)
- [OpenAI API](https://platform.openai.com/docs/)

**Tools:**
- [n8n Community](https://community.n8n.io/)
- [Markdown Guide](https://www.markdownguide.org/)
- [Conventional Commits](https://www.conventionalcommits.org/)

---

### 📞 Questions?

If something is unclear:
- 💬 Ask in Issue
- 📧 Contact: [@khanalytiq](https://t.me/khanalytiq)
- 💬 Discuss in Discussions (if enabled)

---

## 🇷🇺 Русская версия

Спасибо за интерес к проекту! Мы рады любому вкладу - от исправления опечаток до добавления новых функций.

### 🎯 Как можно помочь

**Для всех:**
- 🐛 Сообщать о багах и проблемах
- 💡 Предлагать новые функции
- 📝 Улучшать документацию
- 🌍 Добавлять переводы
- ⭐ Ставить звёздочку проекту

**Для разработчиков:**
- 🔧 Исправлять баги
- ✨ Реализовывать новые функции
- 🧪 Писать тесты
- 📊 Оптимизировать производительность
- 🔒 Улучшать безопасность

---

### 🚀 Начало работы

#### 1. Fork и клонирование

```bash
# Fork проекта на GitHub (кнопка "Fork" вверху справа)

# Клонирование вашего fork
git clone https://github.com/ваш-username/google-calendar-ai-tg-assistant.git
cd google-calendar-ai-tg-assistant

# Добавление upstream remote
git remote add upstream https://github.com/original-author/google-calendar-ai-tg-assistant.git
```

#### 2. Настройка окружения

```bash
# Установка n8n (если ещё не установлен)
npm install n8n -g

# Запуск n8n
n8n start

# Импорт workflow
# n8n → Import from File → выберите JSON файл
```

#### 3. Создание ветки

```bash
# Обновление main ветки
git checkout main
git pull upstream main

# Создание feature ветки
git checkout -b feature/amazing-feature
# или
git checkout -b fix/bug-description
```

---

### 📝 Правила разработки

#### Workflow изменения

**При изменении n8n workflow:**

1. ✅ Тестируйте все изменения локально
2. ✅ Документируйте новые узлы/функции
3. ✅ Обновляйте `docs/architecture.md` если меняется структура
4. ✅ Экспортируйте workflow без credentials
5. ✅ Проверьте что JSON валидный

**Экспорт workflow:**

```
n8n → Workflow → Menu (☰) → Download
→ Сохраните как: 💀 - Google Calendar + TG + AI assistant v2.json
```

**⚠️ Важно:** Перед экспортом удалите все credentials:
```
Settings → Workflow → Remove sensitive data
```

#### Документация

**При добавлении функций:**

1. ✅ Обновите `README.md` (Features секция)
2. ✅ Добавьте примеры в `docs/examples.md`
3. ✅ Обновите `docs/architecture.md` (если меняется структура)
4. ✅ Добавьте в `docs/troubleshooting.md` (если есть особенности)
5. ✅ Обновите `SETUP.md` (если меняется установка)

**Стиль документации:**
- Используйте ясный и простой язык
- Добавляйте примеры кода где возможно
- Используйте эмодзи для улучшения читаемости
- Поддерживайте двуязычность (RU + EN)

#### Коммиты

**Формат commit message:**

```
тип: краткое описание

[опционально] Подробное описание

[опционально] Fixes #номер-issue
```

**Типы:**
- `feat`: новая функция
- `fix`: исправление бага
- `docs`: изменения в документации
- `style`: форматирование, опечатки
- `refactor`: рефакторинг кода
- `test`: добавление тестов
- `chore`: обновление зависимостей, конфигурации

**Примеры:**

```bash
git commit -m "feat: добавлена поддержка повторяющихся событий"

git commit -m "fix: исправлена проблема с timezone detection

Timezone теперь корректно определяется через HTTP Request узел
вместо использования default значения из промпта.

Fixes #42"

git commit -m "docs: обновлены примеры в README"
```

---

### 🐛 Сообщение о багах

**Перед созданием Issue:**

1. ✅ Проверьте, что баг ещё не был заявлен
2. ✅ Убедитесь, что используете последнюю версию
3. ✅ Попробуйте воспроизвести на чистой установке

**Шаблон Issue:**

```markdown
## 🐛 Описание бага

Четкое и краткое описание проблемы.

## 📋 Шаги для воспроизведения

1. Откройте workflow
2. Отправьте сообщение '...'
3. Нажмите '...'
4. Видим ошибку

## ✅ Ожидаемое поведение

Что должно было произойти.

## ❌ Фактическое поведение

Что произошло на самом деле.

## 🖥️ Окружение

- **n8n версия:** 1.x.x
- **OS:** macOS 14.1 / Ubuntu 22.04 / Windows 11
- **Node.js версия:** 18.x.x
- **Тип установки:** Docker / npm / n8n Cloud

## 📸 Скриншоты

Если применимо, добавьте скриншоты.

## 📝 Логи

```
Вставьте релевантные логи здесь
```

## 🔍 Дополнительный контекст

Любая другая информация о проблеме.
```

---

### 💡 Предложение функций

**Шаблон Feature Request:**

```markdown
## ✨ Описание функции

Четкое и краткое описание того, что вы хотите добавить.

## 🎯 Проблема

Какую проблему это решает?
Пример: "Мне неудобно [...] потому что [...]"

## 💡 Предлагаемое решение

Как вы представляете реализацию?

## 🔄 Альтернативы

Какие альтернативные решения вы рассматривали?

## 📋 Use Cases

Конкретные примеры использования:

1. Как пользователь, я хочу [...]
2. Это позволит мне [...]

## 🎨 Mockups / Примеры

Если есть, приложите примеры UI или кода.

## 🚀 Приоритет

- [ ] Nice to have
- [ ] Important
- [ ] Critical

## 💬 Дополнительная информация

Любая другая информация или контекст.
```

---

### 🔄 Pull Request процесс

#### 1. Перед созданием PR

**Чеклист:**

- [ ] Код работает и протестирован
- [ ] Документация обновлена
- [ ] Commit messages следуют guidelines
- [ ] Ветка обновлена с upstream/main
- [ ] Нет конфликтов
- [ ] JSON workflow валидный
- [ ] Credentials удалены из экспорта

#### 2. Создание Pull Request

```bash
# Push в ваш fork
git push origin feature/amazing-feature

# Создайте PR на GitHub
# base: main ← compare: feature/amazing-feature
```

**Шаблон PR:**

```markdown
## 📝 Описание

Краткое описание изменений.

## 🔗 Связанные Issues

Closes #номер-issue (если применимо)

## 🎯 Тип изменений

- [ ] 🐛 Bug fix (non-breaking change)
- [ ] ✨ New feature (non-breaking change)
- [ ] 💥 Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] 📝 Documentation update

## ✅ Checklist

- [ ] Код протестирован и работает
- [ ] Документация обновлена
- [ ] Commit messages корректны
- [ ] Нет конфликтов с main
- [ ] Credentials удалены из workflow
- [ ] Добавлены примеры использования (если новая функция)

## 📸 Скриншоты / Примеры

Если применимо, добавьте скриншоты или примеры использования.

## 🧪 Как тестировал

Опишите как вы тестировали изменения:

1. Шаг 1
2. Шаг 2
3. Результат

## 💬 Дополнительная информация

Любая другая информация для ревьюверов.
```

#### 3. Code Review

**Процесс:**

1. Maintainer проверит ваш PR
2. Могут быть запрошены изменения
3. Внесите изменения и push в ту же ветку
4. После одобрения PR будет смержен

**Время ответа:**
- Обычно: 1-3 дня
- Для срочных (security): 24 часа

---

### 🧪 Тестирование

#### Ручное тестирование

**Базовый тест сценарий:**

```
1. ✅ Создание события
   Команда: "Создай встречу завтра в 15:00"
   Ожидание: Событие создано в Google Calendar

2. ✅ Просмотр событий
   Команда: "Что у меня на этой неделе?"
   Ожидание: Список всех событий

3. ✅ Обновление события
   Команда: "Перенеси встречу на 16:00"
   Ожидание: Время события изменено

4. ✅ Удаление события
   Команда: "Удали встречу завтра"
   Ожидание: Событие удалено

5. ✅ Голосовое сообщение
   Действие: Отправка голосовой команды
   Ожидание: Транскрипция и выполнение

6. ✅ Обработка ошибок
   Действие: Неверная команда
   Ожидание: Понятное сообщение об ошибке
```

#### Тестирование новых функций

**При добавлении новой функции:**

1. Положительные сценарии (happy path)
2. Негативные сценарии (ошибки, edge cases)
3. Граничные условия (пустые значения, большие данные)
4. Обратная совместимость

---

### 📚 Ресурсы

**Документация:**
- [n8n Documentation](https://docs.n8n.io/)
- [Telegram Bot API](https://core.telegram.org/bots/api)
- [Google Calendar API](https://developers.google.com/calendar/api)
- [OpenAI API](https://platform.openai.com/docs/)

**Инструменты:**
- [n8n Community](https://community.n8n.io/)
- [Markdown Guide](https://www.markdownguide.org/)
- [Conventional Commits](https://www.conventionalcommits.org/)

---

### 🏆 Contributors

Спасибо всем, кто внёс вклад в проект!

<!-- Будет автоматически генерироваться -->

---

### 📞 Вопросы?

Если что-то непонятно:
- 💬 Задайте вопрос в Issue
- 📧 Свяжитесь: [@khanalytiq](https://t.me/khanalytiq)
- 💬 Обсудите в Discussions (если включены)

---

**⭐ Если проект оказался полезным, поставьте звезду!**

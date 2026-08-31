# 🧩 Paradox Test

## 📌 Описание

**Paradox Test** — это SPA-приложение на Vue.js для отображения и поиска категорий и элементов. Проект демонстрирует работу с компонентами, стилями и конфигурацией Vue CLI.

## 🛠 Технологический стек

| Технология | Назначение |
|-------------|------------|
| **Vue.js 2** | Фреймворк для построения UI |
| **Vue CLI** | Сборка и конфигурация проекта |
| **SCSS** | Препроцессор стилей |
| **Babel** | Транспиляция JavaScript |
| **JavaScript (ES6+)** | Основной язык |

## 🚀 Установка и запуск

### Требования
- Node.js ≥ 12
- npm ≥ 6

### Установка зависимостей

```bash
npm install
```

### Запуск в режиме разработки

```bash
npm run serve
```

Приложение будет доступно по адресу: `http://localhost:8080`

### Сборка для продакшена

```bash
npm run build
```

### Проверка кода (lint)

```bash
npm run lint
```

## 💻 Примеры использования

### Основной компонент приложения

```vue
<!-- src/App.vue -->
<template>
  <div id="app">
    <CategoryItem />
    <ElementItem />
    <SearchItem />
  </div>
</template>
```

### Импорт компонентов

```javascript
import CategoryItem from './components/CategoryItem.vue';
import ElementItem from './components/ElementItem.vue';
import SearchItem from './components/SearchItem.vue';
```

## 📁 Структура проекта

```
paradox-test/
├── public/                    # Публичные файлы
│   ├── favicon.ico
│   └── index.html            # HTML-шаблон
├── src/                      # Исходный код
│   ├── assets/               # Статические ресурсы
│   │   ├── logo.png
│   │   └── styles.scss       # Глобальные стили
│   ├── components/           # Vue-компоненты
│   │   ├── CategoryItem.vue  # Компонент категории
│   │   ├── ElementItem.vue   # Компонент элемента
│   │   ├── SearchItem.vue    # Компонент поиска
│   │   └── ui/               # UI-компоненты
│   ├── App.vue               # Корневой компонент
│   └── main.js               # Точка входа
├── babel.config.js           # Конфигурация Babel
├── jsconfig.json             # Настройки IDE
├── package.json              # Зависимости и скрипты
├── vue.config.js             # Конфигурация Vue CLI
└── README.md
```

## 📄 Лицензия

MIT License

---

**Автор:** Paradox Team
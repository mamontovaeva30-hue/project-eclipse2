
/* ===================================
   PROJECT: ECLIPSE
   MAIN SYSTEM SCRIPT
=================================== */

const $ = (selector) => document.querySelector(selector);
const $$ = (selector) => document.querySelectorAll(selector);

// ДЕМО-ДАННЫЕ ДЛЯ ВХОДА
const DEMO_ID = "EC-1047";
const DEMO_PASSWORD = "ECLIPSE2026";

// ЭЛЕМЕНТЫ САЙТА
const loadingScreen = $("#loading-screen");
const loginScreen = $("#login-screen");
const app = $("#app");
const modal = $("#modal");
const toast = $("#toast");

// ===================================
// ЗАГРУЗКА
// ===================================

window.addEventListener("load", () => {
  setTimeout(() => {
    loadingScreen.style.opacity = "0";

    setTimeout(() => {
      loadingScreen.classList.add("hidden");
    }, 700);
  }, 1300);
});

// ===================================
// ВХОД И ВЫХОД
// ===================================

$("#login-button").addEventListener("click", login);

$("#login-password").addEventListener("keydown", (event) => {
  if (event.key === "Enter") login();
});

$("#login-id").addEventListener("keydown", (event) => {
  if (event.key === "Enter") login();
});

function login() {
  const id = $("#login-id").value.trim();
  const password = $("#login-password").value;

  if (id === DEMO_ID && password === DEMO_PASSWORD) {
    $("#login-error").textContent = "";

    loginScreen.classList.add("hidden");
    app.classList.remove("hidden");

    showToast("ДОСТУП РАЗРЕШЁН. ДОБРО ПОЖАЛОВАТЬ.");
    showPage("dashboard");
  } else {
    $("#login-error").textContent =
      "ОШИБКА: НЕВЕРНЫЙ ИДЕНТИФИКАТОР ИЛИ ПАРОЛЬ";
  }
}

$("#logout-button").addEventListener("click", () => {
  app.classList.add("hidden");
  loginScreen.classList.remove("hidden");

  $("#login-id").value = "";
  $("#login-password").value = "";

  showToast("СЕАНС ЗАВЕРШЁН");
});

// ===================================
// ПЕРЕКЛЮЧЕНИЕ СТРАНИЦ
// ===================================

const pageNames = {
  dashboard: "Обзор системы",
  archive: "Архив аномалий",
  missions: "Активные операции",
  map: "Карта объектов",
  laboratory: "Лаборатория",
  cameras: "Видеонаблюдение",
  agents: "Сотрудники",
  messages: "Сообщения",
  terminal: "Системный терминал",
  secrets: "Секретные файлы"
};

function showPage(pageId) {
  const page = document.getElementById(pageId);

  if (!page) return;

  $$(".page").forEach((item) => {
    item.classList.remove("active");
  });

  page.classList.add("active");

  $$(".nav-btn").forEach((button) => {
    button.classList.toggle(
      "active",
      button.dataset.page === pageId
    );
  });

  $("#page-title").textContent =
    pageNames[pageId] || "PROJECT: ECLIPSE";

  window.scrollTo({ top: 0, behavior: "smooth" });
}

$$("[data-page]").forEach((button) => {
  button.addEventListener("click", () => {
    showPage(button.dataset.page);
  });
});

// ===================================
// ВСПЛЫВАЮЩИЕ УВЕДОМЛЕНИЯ
// ===================================

let toastTimeout;

function showToast(message) {
  toast.textContent = message;
  toast.classList.add("show");

  clearTimeout(toastTimeout);

  toastTimeout = setTimeout(() => {
    toast.classList.remove("show");
  }, 3000);
}

// ===================================
// БАЗА ДОКУМЕНТОВ И АНОМАЛИЙ
// ===================================

const documents = {

  "alert-case": {
    label: "СРОЧНОЕ УВЕДОМЛЕНИЕ",
    title: "Неизвестный сигнал",
    content: `
СИСТЕМНОЕ УВЕДОМЛЕНИЕ № 009

В 22:41 исследовательская станция
зафиксировала неизвестную передачу.

Источник сигнала не установлен.

Особенность:
Передача содержит голосовые сообщения,
которые совпадают с голосами сотрудников.

ПОСЛЕДНЯЯ ЗАПИСЬ:
«Вы не должны были нас найти».

Статус: РАССЛЕДОВАНИЕ ОТКРЫТО.
`
  },

  "file-104": {
    label: "СЕКРЕТНО",
    title: "Досье № 104",
    content: `
ДОКУМЕНТ № 104

Объект: неизвестное явление.
Первое обнаружение: 14.08.2019.
Место: сектор B-12.

Во время наблюдения камеры
зафиксировали движение в пустом помещении.

Все записи после 03:17 были повреждены.

Примечание исследователя:
«Оно появляется только тогда,
когда никто не смотрит».

Доступ: УРОВЕНЬ 03.
`
  },

  "file-209": {
    label: "ОГРАНИЧЕННЫЙ ДОСТУП",
    title: "Запись № 209",
    content: `
АРХИВНАЯ ЗАПИСЬ № 209

Источник: камера 03.
Время: 03:17.

В течение 47 секунд на записи
присутствует неизвестный силуэт.

После анализа выяснилось:
силуэт находится за камерой.

Однако помещение перед камерой пустое.

Файл частично повреждён.
`
  },

  "file-001": {
    label: "УРОВЕНЬ ДОСТУПА 04",
    title: "Проект 001",
    content: `
ДОСТУП ОГРАНИЧЕН.

Для просмотра требуется специальный код.

Подсказка:
Первый объект организации.
Он находится в названии проекта.

ВВЕДИТЕ КОД В ТЕРМИНАЛ.
`
  },

  "anomaly-001": {
    label: "КРАСНЫЙ УРОВЕНЬ",
    title: "Зеркало № 001",
    content: `
ОБЪЕКТ: E-001
КАТЕГОРИЯ: АНОМАЛЬНОЕ ЯВЛЕНИЕ

Объект выглядит как обычное зеркало.

Но отражение иногда движется
с небольшой задержкой.

Однажды исследователь заметил,
что отражение продолжало двигаться
после того, как он отошёл.

КОД ДОСЬЕ: MIRROR001
`
  },

  "anomaly-009": {
    label: "НЕИЗВЕСТНЫЙ",
    title: "Сигнал № 009",
    content: `
ОБЪЕКТ: E-009
КАТЕГОРИЯ: НЕИЗВЕСТНАЯ ПЕРЕДАЧА

Радиосигнал обнаружен
в северном секторе.

Частота: 87.4 MHz.

Передача повторяется
каждые 13 минут.

Последние слова записи:
«Мы всё ещё здесь».

КОД ДОСЬЕ: SIGNAL009
`
  },

  "anomaly-014": {
    label: "СТАБИЛЬНЫЙ",
    title: "Чёрный куб",
    content: `
ОБЪЕКТ: E-014

Неизвестный предмет.
Не имеет видимых надписей.

При изменении освещения
его поверхность не меняется.

Исследования продолжаются.

КОД ДОСЬЕ: CUBE014
`
  },

  "anomaly-027": {
    label: "КРАСНЫЙ УРОВЕНЬ",
    title: "Пустой коридор",
    content: `
ОБЪЕКТ: E-027

Камеры станции 04
регулярно фиксируют движение
в пустом коридоре.

Сотрудники утверждают,
что слышат шаги после закрытия станции.

КОД ДОСЬЕ: HALL027
`
  },

  "mission-1": {
    label: "АКТИВНАЯ ОПЕРАЦИЯ",
    title: "Тихий сигнал",
    content: `
ЗАДАЧА № 01

Вы получили доступ к записи сигнала 009.

Необходимо определить его источник.

ЭТАП 1:
Откройте архив аномалий.

ЭТАП 2:
Изучите досье объекта 009.

ЭТАП 3:
Найдите код SIGNAL009 в терминале.

Операция продолжается...
`
  },

  "mission-2": {
    label: "РАССЛЕДОВАНИЕ",
    title: "Забытый этаж",
    content: `
ЗАДАЧА № 02

В архитектурных документах
комплекса отсутствует этаж 13.

Но камера 03 регулярно показывает
табличку с номером 13.

Последняя запись сотрудника:
«Он существует. Просто его нет
на обычных схемах».

ПРОВЕРЬТЕ СООБЩЕНИЯ МИРЫ ЛИ.
`
  },

  "experiment": {
    label: "ЛАБОРАТОРНЫЙ ОТЧЁТ",
    title: "Эксперимент EX-204",
    content: `
ОБРАЗЕЦ: НЕИЗВЕСТНЫЙ МАТЕРИАЛ

Результат анализа:
Структура не соответствует
известным материалам.

При воздействии сигнала 009
образец начинает светиться.

Статус: ТРЕБУЕТСЯ ПОВТОРНОЕ ИССЛЕДОВАНИЕ.
`
  },

  "map-a": {
    label: "ТОЧКА A",
    title: "Станция 01",
    content: "Главный исследовательский комплекс. Статус: активен."
  },

  "map-b": {
    label: "ТОЧКА B",
    title: "Сектор B-12",
    content: "Зона обнаружения объекта 001. Доступ ограничен."
  },

  "map-c": {
    label: "ТОЧКА C",
    title: "Северный сектор",
    content: "Источник неизвестного сигнала 009."
  },

  "map-d": {
    label: "ТОЧКА D",
    title: "Станция 04",
    content: "Последняя связь с персоналом: 19:03."
  },

  "camera-01": {
    label: "ВИДЕОАРХИВ",
    title: "Камера 01",
    content: "Запись доступна. Главный вход. Последняя проверка: 22:41."
  },

  "camera-02": {
    label: "ВИДЕОАРХИВ",
    title: "Камера 02",
    content: "Лаборатория. На записи зафиксировано изменение освещения."
  },

  "camera-03": {
    label: "ВИДЕОАРХИВ",
    title: "Камера 03",
    content: "Коридор 13. В архиве обнаружена неизвестная временная метка 03:17."
  },

  "camera-04": {
    label: "ОШИБКА СОЕДИНЕНИЯ",
    title: "Нет сигнала",
    content: "Связь с камерой потеряна. Последний сигнал: неизвестен."
  },

  "agent-director": {
    label: "ДОСЬЕ СОТРУДНИКА",
    title: "Александр Рейн",
    content: "Директор организации. Уровень доступа: 05. Последний вход в систему: сегодня, 22:30."
  },

  "agent-lee": {
    label: "ДОСЬЕ СОТРУДНИКА",
    title: "Мира Ли",
    content: "Главный исследователь. Специализация: аномальные сигналы. Статус: неизвестен."
  },

  "agent-ross": {
    label: "ДОСЬЕ СОТРУДНИКА",
    title: "Даниэль Росс",
    content: "Служба безопасности. Специализация: контроль объектов. Статус: на службе."
  },

  "chat-director": {
    label: "ЛИЧНАЯ ПЕРЕПИСКА",
    title: "Александр Рейн",
    content: `
22:30 — Рейн:
Не открывайте файл 001.

22:31 — Вы:
Почему?

22:33 — Рейн:
Потому что он уже открыт.

22:34 — Рейн:
И я не давал разрешения.
`
  },

  "chat-mira": {
    label: "ЛИЧНАЯ ПЕРЕПИСКА",
    title: "Мира Ли",
    content: `
21:47 — Мира:
Я нашла кое-что в архиве.

21:49 — Вы:
Что именно?

21:50 — Мира:
В документах есть упоминание
об этаже, которого нет.

21:51 — Мира:
И ещё кое-что.
Не доверяй директору.
`
  },

  "chat-unknown": {
    label: "НЕИЗВЕСТНЫЙ ОТПРАВИТЕЛЬ",
    title: "Новый контакт",
    content: `
22:52 — Неизвестный:
Ты уже видел меня.

22:53 — Вы:
Кто это?

22:54 — Неизвестный:
Посмотри запись камеры 03.

22:55 — Неизвестный:
Не ту, которую тебе показывают.
`
  },

  "file-013": {
    label: "ДОСТУП ОГРАНИЧЕН",
    title: "Протокол 013",
    content: "Для доступа требуется специальный код. Найдите его в переписке."
  },

  "file-last": {
    label: "ДОСТУП ОГРАНИЧЕН",
    title: "Последняя запись",
    content: "Для доступа требуется специальный код. Ищите подсказки в архиве."
  }
};

// ===================================
// ОТКРЫТИЕ ДОКУМЕНТОВ
// ===================================

function openDocument(id) {
  const doc = documents[id];

  if (!doc) {
    showToast("ДОКУМЕНТ НЕ НАЙДЕН");
    return;
  }

  $("#modal-label").textContent = doc.label;
  $("#modal-title").textContent = doc.title;
  $("#modal-content").textContent = doc.content;

  modal.classList.remove("hidden");
}

$$("[data-open]").forEach((element) => {
  element.addEventListener("click", () => {
    openDocument(element.dataset.open);
  });
});

$("#modal-close").addEventListener("click", closeModal);

modal.addEventListener("click", (event) => {
  if (event.target === modal) closeModal();
});

document.addEventListener("keydown", (event) => {
  if (event.key === "Escape") closeModal();
});

function closeModal() {
  modal.classList.add("hidden");
}

// ===================================
// ПОИСК В АРХИВЕ
// ===================================

$("#archive-search").addEventListener("input", filterArchive);
$("#archive-filter").addEventListener("change", filterArchive);

function filterArchive() {
  const search = $("#archive-search").value.toLowerCase();
  const category = $("#archive-filter").value;

  $$(".anomaly-card").forEach((card) => {
    const text = card.textContent.toLowerCase();
    const cardCategory = card.dataset.category;

    const matchesText = text.includes(search);
    const matchesCategory =
      category === "all" || cardCategory === category;

    card.style.display =
      matchesText && matchesCategory ? "" : "none";
  });
}

// ===================================
// ЧАСЫ
// ===================================

function updateClock() {
  const now = new Date();

  $("#clock").textContent =
    now.toLocaleTimeString("ru-RU", {
      hour12: false
    });
}

updateClock();
setInterval(updateClock, 1000);

// ===================================
// ТЕРМИНАЛ
// ===================================

const terminalOutput = $("#terminal-output");
const terminalInput = $("#terminal-input");

function terminalWrite(text) {
  const line = document.createElement("p");
  line.textContent = text;
  terminalOutput.appendChild(line);

  terminalOutput.scrollTop = terminalOutput.scrollHeight;
}

const secretCodes = {
  "MIRROR001": "anomaly-001",
  "SIGNAL009": "anomaly-009",
  "CUBE014": "anomaly-014",
  "HALL027": "anomaly-027",
  "ECLIPSE": "file-001",
  "FLOOR13": "file-013",
  "REMEMBER": "file-last"
};

const secretMessages = {
  "MIRROR001": "АРХИВ ОБЪЕКТА 001 РАЗБЛОКИРОВАН.",
  "SIGNAL009": "АРХИВ ОБЪЕКТА 009 РАЗБЛОКИРОВАН.",
  "CUBE014": "АРХИВ ОБЪЕКТА 014 РАЗБЛОКИРОВАН.",
  "HALL027": "АРХИВ ОБЪЕКТА 027 РАЗБЛОКИРОВАН.",
  "ECLIPSE": "ДОСТУП К ПРОЕКТУ 001 РАЗРЕШЁН.",
  "FLOOR13": "ПРОТОКОЛ 013 РАЗБЛОКИРОВАН.",
  "REMEMBER": "ПОСЛЕДНЯЯ ЗАПИСЬ РАЗБЛОКИРОВАНА."
};

const unlockedCodes = new Set();

function runTerminalCommand() {
  const command = terminalInput.value.trim().toUpperCase();

  if (!command) return;

  terminalWrite("> " + command);
  terminalInput.value = "";

  if (command === "HELP") {
    terminalWrite("ДОСТУПНЫЕ КОМАНДЫ:");
    terminalWrite("HELP — СПИСОК КОМАНД");
    terminalWrite("STATUS — СОСТОЯНИЕ СИСТЕМЫ");
    terminalWrite("TIME — ТЕКУЩЕЕ ВРЕМЯ");
    terminalWrite("CLEAR — ОЧИСТИТЬ ТЕРМИНАЛ");
    terminalWrite("КОДЫ — ОТКРЫТЬ СЕКРЕТНЫЕ ДОКУМЕНТЫ");
    return;
  }

  if (command === "STATUS") {
    terminalWrite("СИСТЕМА: АКТИВНА");
    terminalWrite("УРОВЕНЬ ДОСТУПА: 03");
    terminalWrite("УГРОЗА: ПОВЫШЕНА");
    return;
  }

  if (command === "TIME") {
    terminalWrite(new Date().toLocaleString("ru-RU"));
    return;
  }

  if (command === "CLEAR") {
    terminalOutput.innerHTML = "";
    terminalWrite("ТЕРМИНАЛ ОЧИЩЕН.");
    return;
  }

  if (secretCodes[command]) {
    unlockedCodes.add(command);

    terminalWrite(secretMessages[command]);

    setTimeout(() => {
      openDocument(secretCodes[command]);
    }, 300);

    updateSecretFiles();
    return;
  }

  if (command === "КОДЫ") {
    terminalWrite("ПОДСКАЗКА: ИЗУЧАЙТЕ АРХИВ, КАМЕРЫ И СООБЩЕНИЯ.");
    return;
  }

  terminalWrite("ОШИБКА: НЕИЗВЕСТНАЯ КОМАНДА.");
}

$("#terminal-send").addEventListener("click", runTerminalCommand);

terminalInput.addEventListener("keydown", (event) => {
  if (event.key === "Enter") runTerminalCommand();
});

// ===================================
// СЕКРЕТНЫЕ ФАЙЛЫ
// ===================================

function updateSecretFiles() {
  const secretButtons = $$(".secret-file");

  secretButtons.forEach((button) => {
    const id = button.dataset.open;

    const codeForFile = Object.keys(secretCodes).find(
      code => secretCodes[code] === id
    );

    if (codeForFile && unlockedCodes.has(codeForFile)) {
      button.querySelector("small").textContent = "РАЗБЛОКИРОВАНО";
      button.querySelector("small").style.color = "#5be5b0";
    }
  });
}

// ===================================
// СТАРТОВОЕ СОСТОЯНИЕ
// ===================================

console.log("PROJECT: ECLIPSE SYSTEM LOADED");
console.log("DEMO ID: EC-1047");
console.log("DEMO PASSWORD: ECLIPSE2026");

# 🏗️ Спецификация компонентов и раскладки (Components & Layout)

Документ описывает логику построения переиспользуемых элементов интерфейса и применение Auto Layout в Figma.

## 1. Разбор компонента «Кнопка» (Button)
На странице `Design System` создан мастер-компонент `Button` (Component Set) с двумя вариантами.

*   **Структура:** контейнер Auto Layout (`Direction: Horizontal`, `Padding: 16px 32px`, `Gap: 8px`, `Width: Hug contents`) с текстовым слоем `label`. Ширина кнопки подстраивается под длину текста; на Mobile у экземпляра включено `Width: Fill container`.
*   **Свойство варианта:** `State`.
    1.  `State=Default` — фон `Secondary` (#FFA800), текст `Neutral/Dark`.
    2.  `State=Hover` — фон `Primary` (#2D4BD6), текст `Neutral/Light`. В прототипе на варианте Default настроено `While hovering → Change to State=Hover` (Smart Animate, 200 ms), поэтому все экземпляры реагируют на наведение в режиме Present.
*   **Использование:** все кнопки макета («Хочу на пробное занятие», «Записаться», «Оставить заявку», «Связаться с нами») — экземпляры (Instances) этого компонента; меняется только текст через override.

## 2. Применение Auto Layout и связь с CSS Flexbox
Все секции собраны на Auto Layout, группы (`Ctrl + G`) и свободное позиционирование не используются (кроме фонового фото и декоративных штрихов в Hero — они помечены `Ignore auto layout` / `position: absolute`).

| Блок (имя слоя) | Настройки Auto Layout | Аналог в CSS |
|---|---|---|
| `Desktop` (корневой фрейм) | Vertical, Gap 0, Width 1440 | `flex-direction: column` |
| `Header` | Horizontal, `Space between`, Padding 24 / 120, выравнивание по центру | `display:flex; justify-content:space-between; align-items:center; padding:24px 120px` |
| `Header/Nav` | Horizontal, Gap 32 | `gap: 32px` |
| `Hero/Content` | Vertical, Gap 32, Width 680 | `flex-direction: column; gap: 32px` |
| `Advantages/Cards` | Horizontal, Gap 24, карточки `Fill container` | `display:flex; gap:24px` + `flex: 1` у карточек |
| `Advantage-card` | Vertical, Gap 16, Padding 32 | `flex-direction: column; gap:16px; padding:32px` |
| `Directions/Tabs` | Vertical, Gap 12 | `flex-direction: column; gap: 12px` |
| `Pricing/Tariffs` | Horizontal + **Wrap**, Gap 24 / 24, карточки 276px | `flex-wrap: wrap; gap: 24px` |
| `Teachers/Cards` | Horizontal, Gap 24 | `display:flex; gap:24px` |
| `Teacher-card` | Vertical, Gap 12: фото → имя → направление → ссылка | `flex-direction: column; gap:12px` |
| `Footer` | Horizontal, `Space between`, Padding 48 / 120 | `justify-content: space-between` |

**Ресайзинг:** у текстовых блоков стоит `Height: Hug contents`. Поэтому при удлинении текста карточка растёт вниз и сдвигает следующие секции, а не накладывается на них.

## 3. Mobile (390px)
*   `Header` — Horizontal, `Space between`, Padding 16 / 20: логотип + иконка меню (бургер). Навигация скрыта.
*   `Hero/Content` — Vertical, Gap 24, Padding 48 / 20; H1 уменьшен до 40px; кнопка `Width: Fill container`.
*   `Advantages/Cards` — Direction переключён на Vertical, Gap 16: карточки идут столбцом.

---
*Составил: Артём Кузнецов*

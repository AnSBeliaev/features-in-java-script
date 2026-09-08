---
theme: seriph
colorSchema: dark
background: '#1E1E1E'
title: Как фичи попадают в JavaScript?
class: text-center
drawings:
  persist: false
transition: slide-left
comark: true
duration: 35min
---

# Как фичи попадают в JavaScript?

Как устроен ТС39 и за какими стадиями следить разработчикам?

---
transition: fade-out
class: tc39-slide
---

# Кто развивает JavaScript?

<div class="grid grid-cols-[1fr_9rem] gap-8 items-center">
<div>

**Знакомьтесь: комитет TC39**

- **Архитекторы языка**: Международная группа экспертов, которая создаёт спецификацию ECMAScript.
- **Из кого состоит**: Делегаты от главных ИТ-гигантов: Google, Apple, Mozilla, Microsoft и др.
- **Главное правило**: Решения принимаются только абсолютным консенсусом (если хоть один против — фича не пройдёт).
- **Всё открыто**: Обсуждения, код и протоколы встреч лежат публично на GitHub.

</div>

<div class="flex flex-col gap-4 items-center">
  <img src="./images/logo-tc39.webp" class="w-32 rounded" alt="TC39" />
  <img src="./images/logo-js.jpg" class="w-32 rounded" alt="JavaScript" />
</div>
</div>


---
transition: slide-up
class: champions-slide
---

# Кто такие Champions?

<div class="temporal-body">
<div>

- **Двигатели прогресса:** Члены комитета TC39, которые добровольно берут шефство над конкретной фичей.

- **Полный цикл:** Чемпион пишет текст спецификации, защищает её на заседаниях и «тащит» от идеи (Stage 0) до релиза (Stage 4).

- **Сборщик хейта и фидбека:** Он координирует обсуждения на GitHub, общается с разработчиками браузеров и ищет тот самый консенсус.

- **Без чемпиона фича умирает:** Если у предложения нет активного лидера (или группа чемпионов выгорела) — фича навсегда застревает в архиве.

</div>
<div class="temporal-photo champions-photo">
  <img src="./images/champions.jpg" alt="We are the Champions" />
</div>
</div>

---
class: stages-slide
notes: |
  Stage 2.7 — инсайд. Дизайн уже заморожен, пишут test262. Без тестов в тройку не пустят.
---

# Стадии TC39

<div class="tc39-stages">

<div class="tc39-stage">
<span class="tc39-stage-emoji">🤔</span>
<div><strong>Stage 0: Strawman</strong> — Просто идея. Кто-то пришел и сказал: «Было бы круто, если бы в JS было вот так».</div>
</div>

<div class="tc39-stage">
<span class="tc39-stage-emoji">🧪</span>
<div><strong>Stage 1: Proposal</strong> — Проблема признана важной. Назначен чемпион, рождаются первые экспериментальные полифилы.</div>
</div>

<div class="tc39-stage">
<span class="tc39-stage-emoji">🧽</span>
<div><strong>Stage 2: Draft</strong> — Первое точное описание синтаксиса в спецификации. Архитектура фичи фиксируется.</div>
</div>

<div class="tc39-stage tc39-stage-27">
<span class="tc39-stage-emoji">🧊</span>
<div><strong>Stage 2.7: Assessment</strong> — (Новинка!) Дизайн фичи заморожен. Изменения больше не вносятся, авторы начинают писать тесты.</div>
</div>

<div class="tc39-stage">
<span class="tc39-stage-emoji">🤞</span>
<div><strong>Stage 3: Candidate</strong> — Тесты готовы. Браузерные движки (V8, WebKit) начинают писать нативную реализацию.</div>
</div>

<div class="tc39-stage">
<span class="tc39-stage-emoji">🥳</span>
<div><strong>Stage 4: Finished</strong> — Фича протестирована в реальных браузерах и официально становится частью стандарта JavaScript.</div>
</div>

</div>

---
class: decorators-slide
---

# Decorators

<div class="temporal-body">
<div>

- **Где можем увидеть:** `@Injectable()`, `@Get()`, `@logged` в Angular и NestJS.

- **Реальность:** TypeScript понимает их с 2015 года, **чистый JavaScript — нет**.

- **TC39:** Фичу обсуждают **с 2016 года**. Она была на Stage 3, но из-за проблем производительности движков её переделывали годами.

- **В чём проблема движков:** Браузер любит предсказуемость. Ему нужно один раз увидеть структуру класса, чтобы запустить его на максимальной скорости. Декоратор ломает эту логику: он влетает в последний момент, перетряхивает методы и лезет в приватные данные. Для браузера это хаос, который сильно тормозит работу сайта.

</div>
<div class="temporal-photo">
  <img src="./images/decorators-truck.png" alt="Грузовик с навесным оборудованием — метафора декораторов" />
</div>
</div>


---
class: two-fns-slide
---

# Старый vs Новый стандарт

TypeScript при сборке превращает `@logged` в обычный вызов. Какие аргументы туда подставить — решает он. В двух режимах это **разные аргументы**.

<div class="grid grid-cols-2 gap-4" style="--slidev-code-font-size: 14px; --slidev-code-line-height: 21px;">

```ts
// Nest / Angular сейчас
function logged(target, key, descriptor) {
  descriptor.value // здесь лежит исходный save
}
```

```ts
// будущий стандарт
function logged(fn, context) {
  fn // исходный save сразу здесь
}
```

</div>

Предположим, вы включили новый режим, а функции остались прежние: они берут `descriptor.value`, а `descriptor` — `undefined`.

Новый стандарт полностью меняет сигнатуру функций. **Ваши кастомные декораторы сломаются.**

<style>
.slidev-code {
  font-size: 14px !important;
  line-height: 21px !important;
}
</style>


---
class: temporal-slide
---

# Temporal: долгострой JS

<div class="temporal-body">
<div>

* **Масштаб изменений:** Это не просто новые методы, а полная замена `Date` (целый набор новых классов для дат, поясов и календарей).
* **Семь лет на конвейере:** Основное время фича провела между Stage 2 и Stage 3, пока инженеры решали критические проблемы.
* **Почему так долго?**
  * **Производительность:** Первые прототипы сильно перегружали память и тормозили браузеры.
  * **Стандартизация:** Формат строк с часовыми поясами (ISO) пришлось долго согласовывать на международном уровне с IETF.
  * **Совместимость:** Нужно было гарантировать, что новый API не сломает миллиарды сайтов со старым `Date`.
* **Текущий статус:** **Stage 4 достигнут**. Спецификация заморожена, движки браузеров активно внедряют нативную поддержку.

</div>
<div class="temporal-photo">
  <img src="./images/temporal-meme.jpg" alt="Почта России" />
</div>
</div>


---
class: records-slide
---

# Records & Tuples

<div class="temporal-body">
<div>

* **Идея:** Неизменяемые записи (`#{ a: 1 }`) и кортежи (`#[1, 2]`), работающие как сложные примитивы со сравнением по значению, а не по ссылке.
* **Итог:** Фича полностью **отозвана со Stage 2 в апреле 2025 года** после 6 лет разработки.
* **Технологический тупик:**
  * **Производительность:** В отличие от низкоуровневых языков, в JS глубокая неизменяемость создавала колоссальную нагрузку на движки и сборщик мусора (GC).
  * **Семантика `===`:** Для глубокого сравнения оператор `===` пришлось бы превратить в тяжелую рекурсивную операцию O(N). Изменение логики главного оператора языка сочли критической ошибкой.
* **Что дальше:** Вместо примитивов обсуждается проект **Composites** — обычные объекты с поверхностной неизменяемостью и сравнением через метод `.equals()`.

</div>
<div class="temporal-photo records-photo">
  <img src="./images/records-meme.jpg" alt="Усложнять просто. Упрощать сложно" />
</div>
</div>

---
class: links-slide
---

# Ссылки

<div class="grid grid-cols-[1fr_auto] gap-12 items-center">
<div>

Каталог TC39, Decorators, Temporal, Records & Tuples.

</div>

<QrLink url="https://github.com/AnSBeliaev/features-in-java-script/blob/master/links.md" :size="220" label="github.com/…/links.md" />
</div>


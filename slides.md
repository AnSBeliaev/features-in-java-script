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
  <img src="/champions.jpg" alt="We are the Champions" />
</div>
</div>

---
class: text-sm
---

# Стадии TC39

Каждая новая фича в JavaScript (ECMAScript) проходит 5 обязательных стадий в комитете TC39 (от зарождения идеи до полноценного релиза). Этот процесс гарантирует, что в язык попадают только хорошо продуманные и протестированные возможности.

| Стадия | Название | Что происходит | Готовность | |
| --- | --- | --- | --- | --- |
| **0** | Strawman (идея) | Любой делегат или контрибьютор выносит мысль на обсуждение | Пока только концепция | 🤔 |
| **1** | Proposal | Комитет признаёт проблему важной. Разбирают API, синтаксис, риски | Дизайн оформляют, появляются полифилы | 🧪 |
| **2** | Draft | Первое точное описание в языке спецификации. Архитектура фиксируется | Дошлифовывают детали | 🧽 |
| **2.7** | Candidate Spec | Спека и дизайн одобрены. Пора писать официальные тесты (test262) | Дизайн заморожен, ждут тестов | 🧊 |
| **3** | Candidate | Тесты есть. Движки (V8, SpiderMonkey) начинают реализацию | Почти готово, можно пробовать в браузерах | 🤞 |
| **4** | Finished | Прошла проверку на реальных движках. Входит в следующий ES | Часть стандарта JavaScript | 🥳 |

<style>
.slidev-layout {
  line-height: 1.25;
}
p {
  line-height: 1.3;
  margin: 0.4em 0 0.6em;
}
table {
  font-size: 0.92em;
  line-height: 1.45;
}
th, td {
  padding: 0.45rem 0.55rem;
  vertical-align: top;
  line-height: 1.45;
}
td:last-child {
  font-size: 1.85em;
  line-height: 1;
  text-align: center;
  vertical-align: middle;
  width: 3.2rem;
  padding-left: 0.2rem;
  padding-right: 0.2rem;
}
tbody tr:nth-child(1) :is(td:nth-child(-n+2), td:nth-child(4)) { color: #f87171; font-weight: 700; }
tbody tr:nth-child(2) :is(td:nth-child(-n+2), td:nth-child(4)) { color: #fb923c; font-weight: 700; }
tbody tr:nth-child(3) :is(td:nth-child(-n+2), td:nth-child(4)) { color: #fbbf24; font-weight: 700; }
tbody tr:nth-child(4) :is(td:nth-child(-n+2), td:nth-child(4)) { color: #fde047; font-weight: 700; }
tbody tr:nth-child(5) :is(td:nth-child(-n+2), td:nth-child(4)) { color: #a3e635; font-weight: 700; }
tbody tr:nth-child(6) :is(td:nth-child(-n+2), td:nth-child(4)) { color: #f7df1e; font-weight: 700; }
</style>

---
class: decorators-slide
---

# Decorators

<div class="temporal-body">
<div>

Декоратор — это функция **снаружи** класса или метода. Пишется как `@Injectable()`, `@Get()`, `@logged`.

Angular и Nest так пишут каждый день. TypeScript это понимает, **обычный JS — нет.**

Эту фичу обсуждают с **2016** года. В 2022 казалось, что она почти готова перейти в стадию 3, но в **2026** комитет вернул её на 2.7.

Почему так вышло. У движков не было общего способа проверить, что они делают одно и то же. Плюс в момент создания класса приходится запускать чужой код: подменять методы, трогать приватные поля. Движку проще ускорять класс, когда его устройство заранее известно. Поэтому декораторы так и остались на стороне TypeScript при сборке.

</div>
<div class="temporal-photo">
  <img src="/decorators-truck.png" alt="Грузовик с навесным оборудованием — метафора декораторов" />
</div>
</div>


---
class: two-fns-slide
---

# Почему две функции — это проблема

Вы пишете только `@logged` над методом. Сами `logged()` нигде не вызываете.

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

`@Injectable` / `@Get` правят Nest и Angular. Свои декораторы придется переписать.

<style>
.slidev-code {
  font-size: 14px !important;
  line-height: 21px !important;
}
</style>


---
class: temporal-slide
---

# Temporal: долгострой в истории JavaScript

<div class="temporal-body">
<div>

Если затронут фундамент языка, TC39 может годами не выпускать фичу в релиз. Temporal постигли семь лет ожидания. 

Замена `Date`: даты, пояса, календари. Не пара методов — целый набор классов. Большую часть времени провёл на стадиях **2 и 3**. На тройке специально не релизят, пока нет двух реализаций в движках.

Почему так долго:
- первые прототипы тормозили браузер
- формат с часовыми поясами согласовывали с IETF
- новое API не должно было сломать старый `Date`

**Stage 4** — спека заморожена, ломать API уже не будут. Движки снимают флаги. Фича идёт в ES2025/ES2026, полная раскатка — к ES2027.

</div>
<div class="temporal-photo">
  <img src="/temporal-meme.jpg" alt="Почта России" />
</div>
</div>


---
class: records-slide
---

# Records & Tuples

<div class="temporal-body">
<div>

История с Records & Tuples — это зеркальное отражение успеха Temporal. Если Temporal доказал, что фича может долго рождаться, но дойти до финала, то Records & Tuples стали примером того, как фичу полностью отозвали после шести лет активной разработки.

Идея казалась идеальной: неизменяемые записи (`#{ a: 1 }`) и кортежи (`#[1, 2]`) как сложные примитивы (как `String` или `BigInt`), которые сравнивают по значению, а не по ссылке. При попытке подружить их с движками браузеров уперлись в технологический тупик.

**Performance.** : В отличие от низкоуровневых языков, в JS глубокая неизменяемость создавала колоссальную нагрузку на движки браузеров и сборщик мусора (GC)

**Перегрузка `===`.** : Для глубокого сравнения вложенных структур оператор === пришлось бы превратить в тяжелую, рекурсивную операцию O(N). Комитет посчитал, что менять базовое поведение главного оператора языка ради одной фичи — критическая архитектурная ошибка.

</div>
<div class="temporal-photo records-photo">
  <img src="/records-meme.jpg" alt="Усложнять просто. Упрощать сложно" />
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


# Ссылки к докладу «Как фичи попадают в JavaScript?»

Доклад: https://features-in-java-script.vercel.app

## Как проверить статус фичи за две минуты

1. [Каталог TC39](https://github.com/tc39/proposals) — есть ли предложение и какая у него стадия. Нет в каталоге — это ещё не путь в стандарт.
2. [MDN Baseline](https://developer.mozilla.org/en-US/docs/Glossary/Baseline/Compatibility) — достаточно ли широко фича в браузерах, чтобы опираться на неё.
3. [node.green](https://node.green/) — есть ли она в нужной версии Node.
4. [caniuse](https://caniuse.com/) — в каких браузерах фича уже есть.

Стадия в каталоге и «можно ли это использовать» — не одно и то же. Stage 4 не значит, что фича доступна везде без полифила. Stage 2.7 не значит, что ее нельзя использовать в проде: в Nest вы пишете `@Injectable()`, TypeScript при сборке превращает это в обычный вызов функции. До браузера декоратор даже не доезжает.

## Процесс TC39

- [Каталог предложений](https://github.com/tc39/proposals)
- [Протоколы заседаний](https://github.com/tc39/notes)
- [Заседание 19 мая 2026: Decorators → 2.7](https://github.com/tc39/notes/blob/main/meetings/2026-05/may-19.md)
- [Сайт TC39](https://tc39.es/)
- [Стадии процесса](https://tc39.es/process-document/)

## Decorators

- [proposal-decorators](https://github.com/tc39/proposal-decorators) — Stage 2.7

## Temporal

- [proposal-temporal](https://github.com/tc39/proposal-temporal)
- [Спецификация Temporal](https://tc39.es/proposal-temporal/)
- [caniuse: Temporal](https://caniuse.com/temporal) — Safari только Technology Preview

## Records & Tuples

- [proposal-record-tuple](https://github.com/tc39/proposal-record-tuple) — в апреле 2025 отозван со Stage 2: withdrawn; subsumed by Composites
- [Issue об отзыве](https://github.com/tc39/proposal-record-tuple/issues/394)
- [proposal-composites](https://github.com/tc39/proposal-composites) — Stage 1, та же задача другим подходом

## Что есть, но не стоит использовать

- [Приложение B](https://tc39.es/ecma262/multipage/additional-ecmascript-features-for-web-browsers.html) — `substr`. Раздел есть, потому что веб нельзя сломать
- [`with`](https://tc39.es/ecma262/multipage/ecmascript-language-statements-and-declarations.html#sec-with-statement) — основной текст спецификации, не приложение B. Замедляет код, делает его нечитаемым, запрещена в `use strict`. [Подробнее](https://learn.javascript.ru/with)
- [Legacy RegExp features](https://github.com/tc39/proposal-regexp-legacy-features) — Stage 3, чтобы описать `RegExp.$1`

## Stage 3

- [import defer](https://github.com/tc39/proposal-defer-import-eval)
- [Iterator.prototype.join](https://github.com/tc39/proposal-iterator-join)

## Stage 2.7

- [Await Dictionary / Promise.allKeyed](https://github.com/tc39/proposal-await-dictionary)

## Чего не стоит ждать

- [Pipeline operator](https://github.com/tc39/proposal-pipeline-operator) — Stage 2 с 2017 года, последнее заседание январь 2026
- [Pattern matching](https://github.com/tc39/proposal-pattern-matching) — Stage 1, последний раз в повестке комитета сентябрь 2023
- [Signals](https://github.com/tc39/proposal-signals) — Stage 1 с 2024 года

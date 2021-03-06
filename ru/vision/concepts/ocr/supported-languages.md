# Поддерживаемые языки и модели распознавания

Для распознавания текста в сервисе используется модель, обученная на определенном наборе языков. Некоторые языки сильно отличаются друг от друга (например, арабский и китайский), поэтому для них используются разные модели.

Модель выбирается автоматически на основе списка языков, указанных в свойстве `language_codes` в конфигурации возможности для анализа.

В рамках одной возможности для анализа может быть использована только одна модель. Если вы в одной конфигурации указали языки из разных моделей, то часть текста не будет распознана.

## Модели и поддерживаемые языки {#models}

Все модели распознавания текста поддерживают русский и английский языки.

### Англо-русская модель {#engrus}

Эта модель работает лучше всего, но поддерживает только два языка:

* `en` — английский.
* `ru` — русский.

### Латино-кириллическая модель {#latcyr}

Эта модель поддерживает языки с латинской и кириллической письменностью:

* `az` — азербайджанский.
* `ba` — башкирский.
* `be` — белорусский.
* `bg` — болгарский.
* `bs` — боснийский.
* `cs` — чешский.
* `da` — датский.
* `de` — немецкий.
* `en` — английский.
* `es` — испанский.
* `et` — эстонский.
* `fi` — финский.
* `fr` — французский.
* `hu` — венгерский.
* `id` — индонезийский.
* `it` — итальянский.
* `kk` — казахский.
* `ky` — киргизский.
* `lt` — литовский.
* `lv` — латышский.
* `mt` — мальтийский.
* `nl` — нидерландский.
* `no` — норвежский.
* `pl` — польский.
* `pt` — португальский.
* `ro` — румынский.
* `ru` — русский.
* `sk` — словацкий.
* `sl` — словенский.
* `sv` — шведский.
* `tg` — таджикский.
* `tr` — турецкий.
* `tt` — татарский.
* `uz` — узбекский.
* `vi` — вьетнамский.

### Прочие модели {#others}

Остальные модели поддерживают только один основной язык и русский с английским:

* `ar`, `en`, `ru` — арабский
* `el`, `en`, `ru` — греческий
* `he`, `en`, `ru` — иврит
* `hy`, `en`, `ru` — армянский
* `ja`, `en`, `ru` — японский
* `ka`, `en`, `ru` — грузинский
* `ko`, `en`, `ru` — корейский
* `th`, `en`, `ru` — тайский
* `zh`, `en`, `ru` — китайский

#### Что дальше

* [Посмотрите известные ограничения в текущей версии](known-issues.md)
* [Попробуйте распознать текст на картинке](../../operations/ocr/text-detection.md)
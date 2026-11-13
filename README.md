# S.T.I.M. - Stimulant Tolerance Immersion Mod

A mod for **S.T.A.L.K.E.R. Anomaly G.A.M.M.A.** by Expand.

**[Download the latest version](https://github.com/expand0501/stim-stimulant-tolerance/releases/latest)** · [Русский](#русский)

In G.A.M.M.A. you can skip sleep completely with coffee, energy drinks, cocaine or epinephrine. S.T.I.M. adds
stimulant tolerance: rest boosters get weaker the more rest they gave you since your last sleep, so sooner or later
you have to sleep.

## Features

- Boosters work at full strength at first, then their effect falls until it reaches 0% at the booster rest limit
  (default 50% of full rest between two sleeps).
- Every rest booster counts, including cigarettes and tea; weak items add little tolerance.
- Sleep removes tolerance (7.5% per hour by default); there is no recovery while awake.
- Tooltip line with your tolerance and the item's current effect; the Rest row shows what the item gives right now.
- Everything configurable in MCM. Event-driven, no per-frame work.

## Installation (Mod Organizer 2)

1. Install the zip from [Releases](https://github.com/expand0501/stim-stimulant-tolerance/releases) as a new mod.
2. Any position in the load order. Needs the G.A.M.M.A. sleep system (part of base G.A.M.M.A.).
3. In game: MCM > S.T.I.M. Safe to add to an existing save.

The full manual is in [`src/readme.md`](src/readme.md) (also inside the zip).
Changes per version: [`CHANGELOG.md`](CHANGELOG.md).

## Bug reports

Open an [issue](https://github.com/expand0501/stim-stimulant-tolerance/issues) with the lines starting with `[STIM]`
from `Anomaly\appdata\logs\xray_*.log` and describe what you saw.

---

## Русский

Мод для **S.T.A.L.K.E.R. Anomaly G.A.M.M.A.**, автор Expand.

**[Скачать последнюю версию](https://github.com/expand0501/stim-stimulant-tolerance/releases/latest)**

В G.A.M.M.A. можно совсем не спать, если пить кофе и энергетики или принимать кокаин и адреналин. S.T.I.M. добавляет
привыкание к стимуляторам: чем больше бодрости они дали вам с последнего сна, тем слабее действуют, так что рано или
поздно спать придётся.

### Возможности

- Сначала стимуляторы действуют в полную силу, затем их эффект падает до 0% на пределе бодрости от стимуляторов
  (по умолчанию 50% полного отдыха между двумя снами).
- Учитываются все средства от усталости, включая сигареты и чай; слабые добавляют мало привыкания.
- Сон снимает привыкание (по умолчанию 7,5% в час); без сна оно не проходит.
- Строка в подсказке показывает ваше привыкание и текущий эффект предмета; строка «Отдых» в характеристиках —
  сколько предмет даёт прямо сейчас.
- Всё настраивается в MCM. Работает только по событиям, без нагрузки каждый кадр.

### Установка (Mod Organizer 2)

1. Установите zip из [Releases](https://github.com/expand0501/stim-stimulant-tolerance/releases) как новый мод.
2. Любое место в порядке загрузки. Нужна система сна G.A.M.M.A. (входит в базовую G.A.M.M.A.).
3. В игре: MCM > S.T.I.M. Можно ставить на текущее сохранение.

Полное описание (на английском) — в [`src/readme.md`](src/readme.md), он же лежит в архиве.

### Сообщить об ошибке

Создайте [issue](https://github.com/expand0501/stim-stimulant-tolerance/issues), приложите строки, начинающиеся с
`[STIM]`, из `Anomaly\appdata\logs\xray_*.log` и опишите, что произошло.

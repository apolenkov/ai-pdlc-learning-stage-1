# Ступень 1. Спецификация в Git

Это вход в основной маршрут R1 → R2 → R3. Все три ступени выполняются в этой папке на последовательных личных ветках: принятые правки наследуются через Git, поэтому повторно клонировать эталоны ступеней 2 и 3 или импортировать свою `specification.md` не нужно.

Результат R1: личный коммит с уточнённой `specification.md` и его полный SHA. Нужны Git и редактор Markdown. Node.js, OpenSpec и код калькулятора на R1 не нужны.

## Где работать и какие права нужны

Клонируйте [общий учебный эталон](https://github.com/apolenkov/sdd-guide-credit-calculator-stage-1) и откройте его корень:

```bash
git clone https://github.com/apolenkov/sdd-guide-credit-calculator-stage-1.git
cd sdd-credit-calculator-stage-1-example
```

В общем эталоне организатор выдаёт доступ на чтение и отправку личных учебных веток. Не отправляйте решение в `main`, не обходите её защиту и не сливайте учебные PR. Если вы проходите курс в собственном репозитории, допустимую базу и merge определяют его правила; команды курса всё равно используют последовательные личные ветки.

В примерах ниже замените `your_login` своим GitHub-логином. Для повторного прохождения добавьте ко всем веткам одинаковый суффикс, например `-2`.

## Задание R1

1. Проверьте папку и создайте ветку:

   ```bash
   git status --short --branch
   git switch -c course/your_login/stage-1-error-result
   ```

   Если `status` показывает чужие или неожиданные правки, остановитесь и уточните папку у организатора. Ничего не сбрасывайте.

2. Прочитайте [исходную спецификацию](specification.md). Внесите решение точно в три места:

   - в разделе «Требования и сценарии» добавьте правило: при ошибочном вводе предыдущий результат очищается до «—», а сообщение указывает ошибочное поле;
   - в таблицу того же раздела добавьте сценарий: сначала `120 000 ₽`, `0%`, `12 месяцев` → `10 000 ₽`; затем срок `1,5 месяца` → ошибка у поля срока и «—» вместо результата;
   - в разделе «Открытые вопросы» удалите решённый вопрос и оставьте: «Для данного упражнения открытых вопросов нет».

   Это заданное решение упражнения, а не правило, которое нужно угадать. Четыре исходных сценария должны сохраниться.

3. Проверьте и сохраните только спецификацию:

   ```bash
   git diff --check
   git diff -- specification.md
   git add specification.md
   git diff --cached --check
   git diff --cached -- specification.md
   git commit -m "docs: clarify result after invalid input"
   git status --short
   git rev-parse HEAD
   ```

   После коммита `status` не выводит строк, а `rev-parse` печатает полный 40-символьный SHA. Проверка Markdown не доказывает работу приложения или человеческое одобрение.

4. Отправьте личную ветку:

   ```bash
   git push -u origin course/your_login/stage-1-error-result
   ```

   Если точная учебная задача Jira уже выдана, добавьте туда ссылку на ветку, полный SHA и краткое решение. Не придумывайте ключ, родителя или факт согласования: при отсутствии задачи сохраните эти данные для организатора.

Необязательная помощь на R1 описана в [готовом сообщении OpenCode](ai/request.md). Она не меняет требования к итоговому diff и личному решению.

## Переход в R2 в этой же папке

Откройте [полную инструкцию R2](https://apolenkov.github.io/customdev-learning/guides/stage-2.html). Её основной режим продолжает текущий checkout: не выполняйте команды отдельного старта из репозитория `sdd-credit-calculator-stage-2-example`.

Короткий контракт перехода:

1. Убедитесь, что открыта принятая R1 и дерево чистое; получите SHA командами `git status --short --branch` и `git rev-parse HEAD`.
2. От этого коммита создайте `course/your_login/stage-2-reset`.
3. В `specification.md` сохраните пять сценариев R1 и добавьте правило сброса плюс три сценария: после успешного расчёта, после ошибки и повторный сброс.
4. Прочитайте diff, сделайте коммит, отправьте ветку и откройте PR с base `course/your_login/stage-1-error-result` и head `course/your_login/stage-2-reset`.
5. Сначала другой аналитик, затем разработчик или архитектор проверяют актуальный diff. После содержательной правки нужны повторные подтверждения обоих людей.
6. Только после основного цикла можно пройти необязательную [2-ИИ](https://apolenkov.github.io/customdev-learning/guides/stage-2-ai.html). Принятые правки сохраняются в той же R2-ветке и снова предъявляются обоим людям, если изменили проверенный diff.

ИИ не заменяет два review. При разрешённом техническом walkthrough без отзывов отмечайте человеческую приёмку как незавершённую.

## Переход в ручную R3

После принятой R2 продолжайте в том же checkout по [полной инструкции R3](https://apolenkov.github.io/customdev-learning/guides/stage-3.html). Не клонируйте сервисный пример и не добавляйте приложение ради этой ступени.

R3 создаётся веткой `course/your_login/stage-3-reset-years` от принятой R2. До инициализации обновите `AGENTS.md` под правила R3. Затем выполните native OpenSpec-команды вручную из этого же корня:

```bash
openspec --version
openspec init --tools opencode --language ru .
openspec new change add-reset-and-years-term --description "Накопительное ТЗ: сброс формы и срок в месяцах или годах"
openspec status --change add-reset-and-years-term --json
openspec instructions proposal --change add-reset-and-years-term --json
```

Далее запрашивайте `status` и `instructions` для следующего planning-артефакта и заполняйте его сами. Переносите все восемь сценариев R2 поэтапно. Удаляйте рабочую `specification.md` только после таблицы соответствия и строгой проверки полного Change; исходный SHA R2 должен остаться записан. В этой папке нет доказанного runtime baseline: новые функции остаются в активном Change с незавершёнными задачами. Apply запрещён. Если CLI недоступна, init завершился ошибкой или root оказался другим, остановитесь и следуйте разделу устранения ошибки полной инструкции; не создавайте структуру наугад.

Необязательная [3-ИИ](https://apolenkov.github.io/customdev-learning/guides/stage-3-ai.html) — другое упражнение. В ветке `course/your_login/stage-3-ai-payment-summary` поверх личной R3 она создаёт или продолжает новый `add-payment-summary` через сообщение в OpenCode, а не повторяет ручной Change. Для неё открывается отдельный PR с base `course/your_login/stage-3-reset-years`; Apply не запускается. После R3 и 3-ИИ код по-прежнему не реализован.

## Карта семи стабильных страниц

- [R1 — спецификация в Git](https://apolenkov.github.io/customdev-learning/guides/stage-1.html)
- [1-ИИ — помощь с R1](https://apolenkov.github.io/customdev-learning/guides/stage-1-ai.html)
- [R2 — сброс, PR и два review](https://apolenkov.github.io/customdev-learning/guides/stage-2.html)
- [2-ИИ — необязательная предпроверка](https://apolenkov.github.io/customdev-learning/guides/stage-2-ai.html)
- [R3 — ручной переход в OpenSpec](https://apolenkov.github.io/customdev-learning/guides/stage-3.html)
- [3-ИИ — отдельный `add-payment-summary`](https://apolenkov.github.io/customdev-learning/guides/stage-3-ai.html)
- [R4 — изолированный продуктовый Store](https://apolenkov.github.io/customdev-learning/guides/stage-3-star.html)

Каталог курса: <https://apolenkov.github.io/customdev-learning/guides/>.

## Отдельная передача R1 в реализацию

Она не заменяет продолжение R2/R3 и не входит в приёмку R1. Передайте разработчику фактические URL репозитория, ветку, полный SHA и путь `specification.md`:

```bash
git status --short --branch
git remote get-url origin
git branch --show-current
source_sha=$(git rev-parse HEAD)
git cat-file -e "$source_sha^{commit}"
git show "${source_sha}:specification.md"
```

Дерево должно быть чистым, а `show` — выводить принятую спецификацию. В корне отдельного checkout сервиса откройте [общий практикум разработчика](https://github.com/apolenkov/sdd-guide-credit-calculator-stage-3/blob/main/docs/developer-handoff.md) и выполните только начальную read-only проверку:

```bash
git status --short --branch
git rev-parse HEAD
sed -n '1,240p' docs/developer-handoff.md
```

Сообщение агенту:

```text
Прочитай docs/developer-handoff.md и AGENTS.md сервиса. Источник требований:
<URL репозитория>, <ветка>, <полный SHA>, путь specification.md.
Проверь доступность коммита и покажи specification.md из этого SHA.
Сопоставь требования с текущим baseline, перечисли пробелы и предложи план
с проверками. Пока не меняй файлы или код, не создавай Change, не запускай
Apply и не называй read-only проверку реализацией новых функций.
```

Если SHA недоступен, дерево грязное или документ не совпадает с передачей, остановитесь. Переход к Change, Apply и коду требует отдельного разрешения.

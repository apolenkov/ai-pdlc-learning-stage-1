# Шаг 1. Требования в Git: расчёт кредита

Учебный репозиторий курса «Анализ с ИИ-агентами»: один запрос заказчика на кредитный калькулятор, который вы превращаете в свой intent и уточнённую спецификацию. В маршруте курса это шаг 1 после подготовки («Зачем меняем процесс», «Markdown, Git, GitLab», «SDD и OpenSpec», «Мета-репозиторий»); дальше идут шаг 2 «Проверяем и согласуем» и обязательный шаг 3 «Изменение в OpenSpec».

| | |
| --- | --- |
| Шаг курса | [Шаг 1. Требования в Git](https://apolenkov.github.io/customdev-learning/guides/s1-git.html) |
| Вход | Обращение заказчика и ответы (`request-and-answers.md`), `specification.md` с четырьмя сценариями. |
| Действие | Свой intent в `intents/clear-calculation-result.md`, пятый сценарий в `specification.md`, личная ветка `course/your_login/stage-1-error-result`. |
| Результат | Опубликованная личная ветка с intent и уточнённой спецификацией; ссылка на неё в учебной задаче. |

**С чего начать.** На GitHub нажмите **Fork**. Если вы работаете в GitLab, создайте проект через **New project → Import project → Repository by URL** и вставьте адрес `https://github.com/apolenkov/sdd-guide-credit-calculator-stage-1.git`. При Fork на GitHub снимите флажок **Copy the main branch only**: тогда в ваш fork попадут и ветки разобранного примера.

## Разобранный пример

Ветки `course/example/*` показывают одно прохождение шагов 1–3 в этом же репозитории. Сверяйте с ними свою работу после того, как сделали шаг самостоятельно, и смотрите только то, что в ветке есть:

| Ветка | Что сверять | Чего в ветке нет |
| --- | --- | --- |
| `course/example/stage-1-error-result` | `specification.md`: правило очистки результата при ошибке, пятый сценарий, снятый открытый вопрос | `intents/clear-calculation-result.md` |
| `course/example/stage-2-reset` | `specification.md`: правило сброса и три сценария сброса поверх пяти сценариев шага 1 | `intents/clear-calculation-result.md` |
| `course/example/stage-3-reset-years` | change `add-reset-and-years-term` в `openspec/changes/` | `specification.md` и `intents/` |
| `course/example/stage-3-ai-payment-summary` | дополнительный change `add-payment-summary` (итоги выплат и переплата) рядом с предыдущим | `specification.md` и `intents/` |

Intent в этих ветках не хранится. Свой `intents/clear-calculation-result.md` сверяйте с [примером intent в main](https://github.com/apolenkov/sdd-guide-credit-calculator-stage-1/blob/main/examples/clear-calculation-result.md): ветки примера проверяют `specification.md` и OpenSpec, но не intent.

## Сначала сформулируйте запрос

Мы переносим договорённости из разрозненных страниц в Git, чтобы у людей и ИИ был один актуальный источник вместо догадок и старых копий. ИИ не всегда знает последние решения команды; рядом с требованиями можно хранить документацию, схемы устройства продукта и код. Позже метарепозиторий свяжет их, а история Git покажет, кто и почему менял договорённость. Шаги 1–3 разбирают один запрос; Git сохраняет его документ и историю между шагами. Отдельный запрос для шага 4 показывает, как к уже описанному продукту добавляется новая потребность.

Результат шага 1: собственный документ `intents/clear-calculation-result.md`, уточнённая `specification.md` в личной ветке `course/your_login/stage-1-error-result` и ссылка на ветку в учебной задаче. Документ объясняет проблему и желаемый результат; спецификация описывает точные правила и сценарии. Нужны VS Code, Git и учебная задача (issue в вашем fork; если курс проходят в компании, задача в трекере команды). Node.js, OpenSpec и код калькулятора на шаге 1 не нужны.

Прочитайте [исходное обращение и ответы](request-and-answers.md) — это источник фактов упражнения. По [общему шаблону замысла](intent-template.md) составьте свой рабочий документ `intents/clear-calculation-result.md`, затем сравните его с [предоставленным примером](examples/clear-calculation-result.md). Папка `examples/` показывает один способ разбора, но не задаёт факты и не заменяет ваш документ. В рабочей ветке файл из `intents/` — единственный актуальный замысел для шагов 1–3; меняйте его вместе с уточнением потребности, а Git сохранит историю. В реальной работе смысл подтверждают инициатор и владелец решения; учебный пример такого согласования не заменяет.

## Где работать и какие права нужны

Откройте [общий учебный эталон](https://github.com/apolenkov/sdd-guide-credit-calculator-stage-1), нажмите **Fork** и выберите своё личное пространство. Скопируйте HTTPS-адрес вашего fork — здесь и во всех примерах ниже `your_login` заменяйте своим логином на GitHub (или GitLab):

```text
https://github.com/your_login/sdd-guide-credit-calculator-stage-1.git
```

В VS Code выполните **Git: Clone** через палитру команд или кнопку **Clone Repository**, вставьте адрес fork, выберите родительскую папку и откройте клонированный корень `sdd-guide-credit-calculator-stage-1`. В терминале из родительской папки то же делают две команды (в GitLab подставьте адрес своего проекта):

```sh
git clone https://github.com/your_login/sdd-guide-credit-calculator-stage-1.git
cd sdd-guide-credit-calculator-stage-1
```

Эта папка останется рабочей на шагах 1–3.

После клонирования `origin` уже указывает на ваш fork, поэтому второй remote добавлять не нужно. Не отправляйте решение в `main` и не обходите её защиту. На шагах 2–4 курс требует одобрения по текущему diff. Его даёт владелец продукта: он нажимает Approve. Аналитик и техлид оставляют замечания в MR/PR. Архитектора приглашают через @, если изменение затрагивает данные, интеграции, безопасность или производительность, либо при споре; он пишет замечания (и `design.md`), но одобряет по-прежнему владелец продукта. Автор не одобряет свой запрос. ИИ и автоматическая проверка одобрение не заменяют.

Для повторного прохождения добавьте ко всем веткам одинаковый суффикс, например `-2`.

## Задание шага 1

1. Проверьте папку и создайте личную ветку. В VS Code: щёлкните имя текущей ветки в левом конце строки состояния, выберите **Create new branch** и введите `course/your_login/stage-1-error-result`. В терминале: `git switch -c course/your_login/stage-1-error-result`, затем `git status --short --branch` — ожидается только строка `## course/your_login/stage-1-error-result`.

   Если панель **Source Control** показывает чужие или неожиданные правки, остановитесь и уточните папку у организатора. Ничего не сбрасывайте.

2. Откройте и прочитайте [исходную спецификацию](specification.md) в VS Code. Внесите решение точно в три места:

   - в подраздел «ПРАВИЛА» добавьте правило: при ошибочном вводе предыдущий результат очищается до «—», а сообщение указывает ошибочное поле;
   - в таблицу подраздела «СЦЕНАРИИ» добавьте сценарий: сначала `120 000 ₽`, `0%`, `12 месяцев` → `10 000 ₽`; затем срок `1,5 месяца` → ошибка у поля срока и «—» вместо результата;
   - в разделе «Открытые вопросы» удалите решённый вопрос и оставьте: «Для данного упражнения открытых вопросов нет».

   Это заданное решение упражнения, а не правило, которое нужно угадать. Четыре исходных сценария должны сохраниться: после правки в документе должно быть ровно пять сценариев.

3. Проверьте и сохраните замысел вместе со спецификацией. У каждого действия в VS Code (панель **Source Control**) после тире стоит та же команда для терминала:

   - откройте `intents/clear-calculation-result.md` и `specification.md` в списке **Changes** и прочитайте diff — `git diff -- specification.md` (новый файл intent появится в diff после следующего пункта);
   - нажмите **Stage Changes** у этих двух файлов — `git add specification.md intents/clear-calculation-result.md`, затем проверьте staged diff ещё раз — `git diff --cached`;
   - введите сообщение `docs: clarify result after invalid input` и нажмите **Commit** — `git commit -m "docs: clarify result after invalid input"`.

   После коммита список **Changes** снова пуст (`git status --short` ничего не выводит). Чтение diff не доказывает работу приложения или человеческое одобрение. Полный SHA коммита можно посмотреть командой `git rev-parse HEAD`, но для R1 это необязательная продвинутая фиксация, а не условие приёмки.

4. Опубликуйте личную ветку в свой fork. В VS Code: в **Source Control** нажмите **Publish Branch** — VS Code отправит `course/your_login/stage-1-error-result` в `origin` и начнёт отслеживать её. В терминале: `git push -u origin course/your_login/stage-1-error-result`. Ветка должна появиться в вашем fork.

   Личная учебная задача — обязательный шаг: это issue в вашем fork (если вкладки **Issues** нет, включите её в **Settings → General → Features**). Если курс проходят в компании, заведите задачу в трекере команды; порядок описан в [канонической инструкции шага 1](https://apolenkov.github.io/customdev-learning/guides/s1-git.html) и в [корпоративных ресурсах курса](https://apolenkov.github.io/customdev-learning/corporate-resources.html#jira) и здесь не повторяется. Добавьте в задачу ссылку на ветку и краткое решение; полный SHA можно приложить как точную фиксацию, но он необязателен. Не придумывайте номер задачи, родителя или факт согласования.

Необязательная помощь на шаге 1 описана в [готовом сообщении для корпоративного агента](ai/request.md): маршрут курса — Kilo в VS Code, именованная альтернатива — OpenCode. Она не меняет требования к итоговому diff и личному решению.

## Переход к шагу 2 на следующей ветке

Откройте [полную инструкцию шага 2](https://apolenkov.github.io/customdev-learning/guides/s2-review.html). Её основной режим продолжает текущий checkout: не выполняйте команды отдельного старта из репозитория `sdd-guide-credit-calculator-stage-2`.

Короткий контракт перехода:

1. Убедитесь, что в VS Code открыт тот же репозиторий с принятым шагом 1: текущая ветка — `course/your_login/stage-1-error-result`, а панель **Source Control** не показывает незакоммиченных правок.
2. От этой ветки создайте `course/your_login/stage-2-reset` — имя ветки в строке состояния → **Create new branch**; в терминале: `git switch -c course/your_login/stage-2-reset`.
3. В `specification.md` сохраните пять сценариев шага 1 и добавьте правило сброса плюс три сценария: после успешного расчёта, после ошибки и повторный сброс. Повторный сброс не меняет состояние, не запускает расчёт и не показывает ошибок.
4. Прочитайте diff в **Source Control** (`git diff -- specification.md`), выберите файл (**Stage Changes** — `git add specification.md`), сделайте коммит (**Commit** — `git commit -m "docs: describe form reset"`), опубликуйте ветку (**Publish Branch** — `git push -u origin course/your_login/stage-2-reset`) и откройте PR (в GitLab — MR) в своём fork: источник — `course/your_login/stage-2-reset`, база — `course/your_login/stage-1-error-result`. На GitHub шаблон PR подставит разделы описания и чек-лист одобрения сам. В GitLab шаблона для MR в проекте нет: скопируйте текст из [`.github/pull_request_template.md`](https://github.com/apolenkov/sdd-guide-credit-calculator-stage-1/blob/main/.github/pull_request_template.md) в описание MR.
5. Для текущего diff одобрение даёт владелец продукта (Approve); аналитик и техлид оставляют замечания. Если изменение затрагивает данные, интеграции, безопасность или производительность, либо есть спор, архитектора приглашают через @: он пишет замечания, но не одобряет. После новых коммитов владелец продукта одобряет последнюю версию заново. Автор не одобряет свой запрос.

ИИ и автоматическая проверка одобрение не заменяют. При разрешённом техническом walkthrough без отзывов отмечайте приёмку как незавершённую.

## Шаг 3: изменение в OpenSpec

Шаг 3 продолжается в этом же fork от ветки шага 2. Порядок действий — в [docs/step-3-openspec.md](docs/step-3-openspec.md).

## Основные страницы курса

- [Шаг 1. Требования в Git](https://apolenkov.github.io/customdev-learning/guides/s1-git.html)
- [Шаг 2. Проверяем и согласуем](https://apolenkov.github.io/customdev-learning/guides/s2-review.html)
- [SDD и OpenSpec (подготовка)](https://apolenkov.github.io/customdev-learning/guides/p3-sdd.html)
- [Шаг 3. Изменение в OpenSpec](https://apolenkov.github.io/customdev-learning/guides/s3-openspec.html)
- [Шаг 4. Команда продукта](https://apolenkov.github.io/customdev-learning/guides/s4-team.html)
- [Шаг 5. Контекст продукта](https://apolenkov.github.io/customdev-learning/guides/s4-product.html)

Каталог курса: <https://apolenkov.github.io/customdev-learning/guides/>.

## Отдельная передача шага 1 в реализацию

Если результат шага 1 передают разработчику отдельно, следуйте [docs/handoff-step-1.md](docs/handoff-step-1.md).

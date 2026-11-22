# Отдельная передача шага 1 в реализацию

Она не заменяет продолжение шагов 2–3 и не входит в приёмку шага 1. Передайте разработчику фактические URL репозитория, ветку, полный SHA и путь `specification.md`:

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
Сопоставь требования с текущим состоянием, перечисли пробелы и предложи план
с проверками. Пока не меняй файлы или код, не создавай Change, не запускай
Apply и не называй read-only проверку реализацией новых функций.
```

Если SHA недоступен, дерево грязное или документ не совпадает с передачей, остановитесь. Переход к Change, Apply и коду требует отдельного разрешения.

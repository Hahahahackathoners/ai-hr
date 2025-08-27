# SUBMODULES

## Клонирование репозитория

После `git clone` выполните `git submodule init`. Далее см. "Подтягивание новых
изменений".

## Добавление подмодуля

Предположим, вы начинаете работу над новой частью приложения. В пространстве
[Hahahahackathoners](https://github.com/Hahahahackathoners) создайте репозиторий
`ai-hr-<name>`.

Затем склонируйте текущий репозиторий и выполните:

```bash
git submodule add https://github.com/Hahahahackathoners/ai-hr-<name> <name>
git commit -m "Add submodule <name>"
git submodule update --remote --merge
```

> Поскольку подмодули, относящиеся к `ai-hr`, соответствуют паттерну
> `ai-hr-<name>`, будет удобно, если здесь директории, соответствующие
> этим репозиториям, будут названы просто `<name>`. Поэтому в bash-команде выше
> используется _git submodule add \<baseurl\>/ai-hr-\<name\>
> **\<name\>**_.

## Подтягивание новых изменений

Если вы хотите получить актуальные изменения из сабмодуля, выполните:

```bash
git submodule update --remote --merge
```

Изменения будут получены вами локально, они не отразятся в удалённом
репозитории, пока вы не выполните:

```bash
git add .
git commit -m "Update submodules"
git push
```

## Ренейминг подмодуля

Если вы хотите изменить название репозитория, сделайте это в UI GitHub, затем в
корне этого проекта выполните:

```bash
git mv <old-name> <new-name>
```

Откройте `.gitmodules` и обновите url, если он был изменён.

Добавьте изменения и запушьте в репозиторий.

## Checkout тега

`git checkout tag` не обновит подмодули до требуемой версии, а лишь укажет на нужные коммиты (см. `git diff` после `checkout`), поэтому корректное перемещение выглядит так:

```bash
git checkout tag
git submodule update --init --recursive --checkout
```
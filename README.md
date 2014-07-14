Репозиторий совместной работы над задачами Инновы в целом и Фогейма в частности


# HTML/CSS code conventions

## Требования к браузерам
Последние 2-3 версии `Firefox` и `Chrome`, а также `IE 10+` и `Opera 12+`

## HTML
Стараемся использовать не только `<div>`, но и другие элементы.
Используем все элементы, включая новые, появившиеся в HTML5.
Не боимся таблиц, но если данные не табличные – ставим атрибут `role="presentation"`.
Атрибуты `id` — метки для тестировщиков, для изменения внежнего вида используем только `class`.

## CSS
С учетом того, что поддерживаем только современные браузеры (см. требования к браузерам выше), то на полную катушку используем CSS3 и в частности `transition`, `animation`, `transform` (вкл. 3D) и т. п.
Активно используем псевдо элементов `:before` и `:after`, чтобы не создавать ненужные элементы в HTML.

## БЭМ
Исповедуем БЭМ с некоторыми изменениями, которые ввели в начале, поскольку не все в БЭМе казалось очевидным.
Изменения:
для блоков (b), элементов (e) и модификаторов (m) используем префиксы: `bBlock__eElement__mModifier_value`;
разделитель перед модификатором — два знака подчеркивания (бывают исключения);
модификатор может не иметь значение, пример: `bBlock__mModifier`;
многословные наименования пишем в camelCase (из-за префикса они всегда начинают с заглавной буквы): `bMyLittlePony`;
используем страничные (p) префиксы, в качестве пространства имен, с разделителем — одинарное подчеркивание: `pPB_bBlock__eElement`;
по возможности избегаем миксины — например использовать переменные less, а если есть одинаковые элементы, которые входят в состав других блоков, то создавать вложенные блоки.

##LESS
В качестве CSS-препроцессора используем только Less. Были попытки использовать Stylus, но пока они не очень удачные.
Для каждого блока готовим по одному .less файлу, в котором описаны стили всех элементов в этом блоке.

Организуем примерно такую иерархию:

```
.bBlockName {
    /* общие стили для блока */
    font: 18px/22px @textFont;
    color: pink;
    background: black;

    &__eElement1 {
        /* стили относящиеся к конкретному элементу */
        display: inline-block;
        border: 3px dotted cyan;
    }

    &__eElement2 {
        &__mModifier_value {
            /* стили модификатора */
            color: @defaultColor;
            backround: @defaultBgColor;
        }
        &:hover,
        &:active {
            /* одинаковые стили объединяем,
               псевдо-классы считаем отдельными элементами */
            color: @hoverColor;

            .bBlockName__eSubElement {
                /* каскад допустим только в случае с псевдоклассами у родителя,
                   либо если на это есть основательная причина */
            }
        }
    }

    /* избегаем вложенность в рамках названий элементов */
    &__Element {
        /* так стараемся не делать, хотя вроде общий префикс,
           потому что по полному названию элемента не найти в большом файле */
        &1 {  }
        &2 {  }
    }
}
```

## Другие детали

- Весь контент тянется между 960px и 1200px;
- Меньше 960px появляется скролл;
- Шрифты — если шрифт есть у гугла, то берем шрифт с гугла; если нет, то подключаем через font-face.


## Готовые компоненты (блоки)

Для использования на любых страницах Фогейма, у нас есть готовые блоки.

- Кнопка (\*TBD\*)
 
 

# Модель рощи из разных деревьев

## Введение

В [прошлой задаче][задача об апельсиновом дереве] мы смоделировали апельсиновое дерево для нашего клиента, фермера Федора. Мы смогли смоделировать для него производство апельсинового дерева в течение всей его жизни. Он был доволен нашей работой и поэтому привлек нас к ещё одному проекту. Его апельсиновая ферма рассматривает возможность приобретения соседней древесной рощи, роща, которая включает в себя разновидности деревьев помимо апельсиновых.

Мы собираемся построить простую модель рощи из разных деревьев. Мы начнем с нашего апельсинового дерева и используем его как образец для моделирования яблони. Когда у нас будут два древовидных класса и соответствующие классы фруктов, мы займемся реорганизацией нашего кода. После того, как наш код будет реорганизован, мы добавим дополнительный тип дерева: грушевые деревья. Наконец, мы сможем смоделировать целую рощу.


### Наследование
Когда мы позже реорганизуем наш код, мы будем использовать *наследование*, чтобы исключить повторение, которое создают наши нынешние классы `OrangeTree` и `AppleTree`. Мы создадим общий класс `FruitTree`, из которого мы можем создать более конкретные классы деревьев: апельсиновые, яблочные и позднее - грушевые. Наша общая модель фруктовых деревьев обеспечит обычное поведение наших деревьев: они растут, зреют, умирают и т. д. Апельсиновые, яблочные и грушевые деревья будут обладать одними и теми же базовыми характеристиками, но каждое дерево будет отличаться по своей реализации: одно дерево производит апельсины, другое - яблоки; одно дерево умирает в возрасте 100 лет, другое - в 45; и так далее. См. Таблицу 1.


|                    | Апельсиновые деревья | Яблочные деревья | Грушевые деревья |
| ------------------ | -----------: | ----------: | ---------: |
| Максимальная высота| 25           | 26          | 20         |
| Темп роста         | 2.5          | 2           | 2.5        |
| Ежегодный урожай фруктов  100 - 300    | 400 - 600   | 175 - 225  |
| Возраст зрелости    | 6            | 5           | 5          |
| Возраст смерти       | 100          | 45          | 40         |
| Тип фруктов      | oranges      | apples      | pears      |


*Таблица 1*.  Данные для апельсиновых, яблочных и грушевых деревьев


## Releases
### Pre-release: скопируйте модель оранжевого дерева
Прежде чем мы начнем, скопируйте код из задачи об апельсиновом дереве. Возьмите код для апельсинового дерева и апельсинов. Запустите тесты и убедитесь, что они работают должным образом.


### Release 0: Яблоки и яблочные деревья
У нас есть класс OrangeTree с открытым интерфейсом: такие методы, как `.age`,`.isMature`,` isDead` и т. д. Мы собираемся создать класс `AppleTree`, который в точности копирует этот интерфейс. Другими словами, запросы, которые мы отправляем апельсиновому дереву, будут такими же, как мы отправляем яблочному.

Однако несмотря на то, что апельсиновые деревья и яблочные будут вести себя одинаково, они будут иметь разные жизненные циклы. Они будут производить фрукты в разном возрасте, расти с разной скоростью, умирать в разное время и т. д. Детали для каждого типа дерева можно найти в Таблице 1.

Начните с написания тестов для класса `AppleTree`. Используйте тесты для апельсинового дерева как образец, изменяя их для деталей яблочного. Затем внедрим сам класс. Не забудьте, создавая класс `AppleTree` мы не хотим, чтобы яблочное дерево производило апельсины.

### Release 1: от конкретных типов до общего типа
Теперь мы смоделировали два конкретных типа фруктовых деревьев. Наши апельсиновые и яблочные деревья ведут себя очень похожим образом. Основываясь на сходстве поведения между двумя типами деревьев, мы можем создать более обобщенный случай: фруктовое дерево.

Мы можем создать класс `FruitTree` с обобщенным поведением. Наши классы `OrangeTree` и `AppleTree` могут наследовать поведение этого общего класса и реализовывать свои собственные особенности. Например, как апельсиновые деревья, так и яблочные растут вверх. С каждым сезоном деревья растут на некоторую величину, пока не достигнут своей максимальной высоты. Это общее поведение, которое может быть представлено в общей модели плодовых деревьев. Это общее поведение будет унаследовано каждым из конкретных типов фруктовых деревьев с каждым конкретным типом, определяющим, на сколько он растет каждый год и сколько составляет его собственная максимальная высота.

```js
class FruitTree {
  // define the class
}

class OrangeTree extends FruitTree
  // define the class
}

class AppleTree extends FruitTree
  // define the class
}

```
*Рисунок 1*. Определение классов `OrangeTree` и `AppleTree`, которые наследуются от суперкласса `FruitTree` или родительского класса.


Определите класс `FruitTree` и измените классы `OrangeTree` и `AppleTree` для их унаследования (см. Рис. 1). Поэтапно перемещайте общие черты от конкретных деревьев к общему. Сделайте то же самое для наших классов фруктов.

По мере того, как мы это делаем, наше тестирование должно продолжаться: возможно, нам потребуется добавить небольшие изменения в наши тесты, если мы изменим имена наших методов, но нам не нужно менять логику наших тестов. В этом и заключается прелесть тестов. Если наши тесты продолжают проходить после рефакторинга, то мы знаем, что наш код в порядке. Если нет, мы быстро поймаем наши ошибки.


### Release 2: Груши и грушевые деревья
Теперь, когда у нас есть обобщенная модель фруктового дерева, из которой мы можем получить определенные типы деревьев, мы воспользуемся этим, создав дополнительный тип дерева: `PearTree`.

Да, нам также нужно написать тесты для этого типа деревьев.

### Release 3: Модель дерева

|                  | Возраст 0 лет | Возраст 5 лет | Возраст 20 лет | Возраст 37 лет | Возраст 50 лет | Итого |
| :--------------- | ----: | ----: | -----: | -----: | -----: | ----------: |
| **Апельсиновые деревья** | 0     | 20    | 20     | 10     | 20     | 70          |
| **Яблочные деревья**  | 10    | 10    | 20     | 20     | 5      | 65          |
| **Грушевые деревья**   | 10    | 0     | 10     | 20     | 10     | 50          |

*Таблица 2*. Количество деревьев в роще, разделенных по типу и возрасту

Теперь, когда у нас есть модель для каждого типа дерева в роще, давайте построим модель рощи. Данные для деревьев рощи приведены в Таблице 2. Мы можем увидеть, сколько деревьев в роще, их типы и их возраст. Рассмотрим на примере апельсиновых деревьев - в роще в общей сложности 70 апельсиновых деревьев, 20 из них - пятилетние, другим 20 – по 20 лет, ещё 10 апельсиновым деревьям - 37 лет, оставшимся 20 – по 50 лет.

Определите класс `TreeGrove`, который будет отвечать за управление деревьями в роще. Вот список некоторых начальных действий для класса.

1. Рощу можно инициализировать массивом деревьев.
2. Роща может возвращать разные подмножества своих деревьев: все деревья, только деревья одного типа, только зрелые деревья и т. д.
3. Когда древесная роща проходит вегетационный период, каждое из ее деревьев проходит сезон.

*Подсказка:* Мы можем отредактировать наши деревья. Например, мы можем инициализировать их с заданными возрастом и высотой.

### Release 4: Модель ожидаемого производства
Пришло время использовать наши модели. Федор хочет, чтобы мы составили отчет о количестве ожидаемой продукции рощи в течение следующих 10 сезонов. По каждому сезону в нашем отчете должно указываться: (1) сколько апельсинов, яблок и груш наша модель будет производить каждый сезон, (2) средний размер каждого вида фруктов и (3) для каждого типа дерева мы должны указать, сколько незрелых, зрелых, мертвых  деревьев в роще, а также их общее количество. (См. [пример отчета])


## Выводы
В этой задаче мы начали изучать ннаследование. Это способ совместного использования поведения между подобными типами объектов, который может упростить наш код. Наследование подходит только тогда, когда подкласс (например, `OrangeTree`) является определенным типом суперкласса (например, `FruitTree`). У нас будет больше возможностей для изучения наследования.

[пример отчета]: readme-assets/example_report.md
[задача об апельсиновом дереве]: ../../../orange-tree-1-just-oranges-challenge

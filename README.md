# `Конспект лабораторных`

## Перед началом работы

(vscode)  
`python -m venv ./.venv`  
`./.venv/Scripts/activate`  
`pip3 install -r requirements.txt`

## Лабораторная работа № 1

### `Цель: построение модели машинного обучения, которая сможет обучиться на основе характеристик ирисов, уже классифицированных по сортам, и предскажет сорт для нового цветка ириса`

Поскольку у нас есть примеры, то задача является задачей обучения с учителем.
| Термин | Значение |
| --------------------------- | --------------------------------------------------------------------------- |
| Задача классификации | Прогнозирование (один из сортов ириса) |
| Классы | Возможные ответы |
| Метка | Сорт, к которому принадлежит цветок (конкретная точка данных) |
| Загружаемые данные | |
| Примеры | В машинном обучении - отдельные элементы |
| Характеристики или признаки | Их свойства |
| Форма массива данных | Определяется количеством примеров |
| Метрики эффективности: обучающий и тестовый наборы ||
| Обучающие данные (набор) | Часть данных, которые используются для построения модели машинного обучения |
| Тестовые данные | Часть данных, которые используются для оценки качества модели |
| Просмотр данных ||
| Диаграмма рассеяния | один из способов исследования данных (визуализация)|
| Матрица диаграмм рассеяния | размещение набора данных с 3+ признаками |

---

## Лабораторная работа № 2

Алгоритм К ближайших соседей (суть):  
Создается цветок с параметрами. Сравнивается с готовым набором данных (из лаб. 1) и выдается предположение о сорте цветка. Потом идет проверка прогноза на точность.
K означает количество ближайших соседей. Правильность -процент цветов, для которых модель предсказала правильный сорт.  
`fit()` - построение модели на обучающем наборе данных  
`predict()` - применение модели к новым данным (прогноз)  
`score()` - оценка точности модели

---

## Лабораторная работа № 3

### Классификация и регрессия

Две основные задачи машинного обучения: `классификация` и `регрессия`.

`Цель классификации` - спрогнозирвать метку класса, которая представляет собой выбор из заранее определенного списка возможных вариантов.

Классификация делится на: бинарную и мультиклассовую.

`Бинарная классификация` - частный случай разделения на два класса. Можно представить как попытку ответить на поставленный вопрос в формате "да/нет".

`Цель регрессии` - спрогнозивать непрерывное число или число с плавающей точкой (вещественное). Прогнозируемое значение называется `суммой` и может быть любым числом в заданном диапазоне.

Простой способ отличить - спросить, заложена ли в полученном ответе определенная непрерывность. Результаты непрерывно связаны - задача регрессии.

Модель обладает способностью `обобщать`, если может выдавать точные прогнозы на ранее не встечавшихся данных.

`Переобучение` - построение модели, которая слишком сложна для имеющегося объема информации. Происходит, когда модель слишком точно подстраивается под особенности обучающего набора и на выходе получается модель, которая хорошо работает на обучающем наборе, но не умеет обобщать результат на новые данные.

`Недообучение` - слишком простая модель, обратная "переобученной".

`Оптимальная точка` - наилучшая обобщающая способность.

Сложность модели связана с изменчивостью входных данных. Больше разнообразие точек в наборе - более сложная модель может использоваться. **Дублирования** лучше избегать.

```python
wave #синтетический набор для иллюстрации алгоритмов регрессии
```

Набор данных имеет единственный входной признак и непрерывную целевую переменную или `отклик`, который мы хотим смоделировать.

`Низкоразмерный набор (low-dimensional)` - набор с небольшим числом признаков.
Вывод может не подтвердится для `высокоразмерного набора (high-dimensional)`.

`Конструирование признаков` - включение производных признаков.

```python
load_extended_boston # набор данных с производными признаками
```

### Алгоритм k ближайших соседей

`Голосование` - для каждой точки тестового набора мы подсчитываем кол-во соседей, относящихся к классу 0, и кол-во соседей, относящихся к классу 1. Затем мы присваиваем точке тестового набора наиболее часто встречающийся класс. Используется при рассмотрении более одного соседа.

`Граница принятия решений` - граница, которая разбивает плоскость на две области: где алгоритм присваивает класс 0, и где класс 1.

Алгоритм регрессии k ближайших соседей реализован в классе `KNeighborsRegressor`

Метод `score()` возвращает значение R<sup>2</sup> (коэффициент детерминации), позволяет оценить качество модели.

В классификаторе `KNeighbors` два важных параметра: кол-во соседей и мера расстояния между точками данных.

Преимущества метода ближайших соседей:

- модель легко интерпретировать
- приемлемое качество без необходимости использования большого кол-ва настроек.

Недостатки:

- Занимает время, когда набор данных очень большой.
- Важно проводить предварительную обработку данных.
- Не хорош, когда признаков 100+ и особенно плох, когда много признаков в большей части наблюдения имеют 0-е значения (`разреженные наборы данных`).

---

## Лабораторная работа № 4

### Линейные модели. Метод наименьших квадратов.

Линейные модели дают прогноз, используя линейную функцию.

### Линейная регрессия (обычный метод наименьших квадратов)

Линейная регрессия или обычный метод наименьших квадратов - самый простой метод регрессии.

`Линейная регрессия` находит параметры w и b, которые минимизируют ошибку (mean squared error) между спрогнозированными и фактическими ответами в обучающем наборе.

`Среднеквадратичная ошибка` равна сумме квадратов разностей между спрогнозированными и
фактическими значениями. Линейная регрессия проста, что является преимуществом, но в то же
время у нее нет инструментов, позволяющих контролировать сложность модели.

Параметры «наклона» (w), также называемые `весами` или `коэффициентами` (coefficients),
хранятся в атрибуте `coef_`, тогда как `сдвиг (offset)` или `константа (intercept)`, обозначаемая как b,
хранится в атрибуте `intercept_`.

Атрибут `intercept_` - это всегда отдельное число с плавающей точкой, тогда как атрибут `coef_` - это массив NumPy, в котором каждому элементу соответствует входной признак.

### Гребневая регрессия

Гребневая регрессия также является линейной моделью регрессии, поэтому ее формула аналогична той, что используется в обычном методе наименьших квадратов.

Все элементы w должны быть близки к нулю.

`Регуляризация` означает явное ограничение модели для предотвращения переобучения.
Регуляризация, использующаяся в гребневой регрессии, известна как L2 регуляризация.
Гребневая регрессии реализована в классе `linear_model.Ridge`.

Модель `Ridge` позволяет найти компромисс между простотой модели (получением коэффициентов, близких к нулю) и качеством ее работы на обучающем наборе. Компромисс между простотой модели и качеством работы на обучающем наборе может быть задан пользователем при помощи параметра `alpha`. Увеличение alpha заставляет коэффициенты сжиматься до близких к нулю значений, что снижает качество работы модели на обучающем наборе, но может улучшить ее обобщающую способность.

`Кривые обучения` - это график, показывающий зависимость между оценкой модели и количеством используемых данных.

### Лассо

Является альтернативой `Ridge`.
Как и гребневая регрессия, лассо также сжимает коэффициенты до близких к нулю значений, но несколько иным способом, называемым `L1` регуляризацией. Результат `L1` регуляризации заключается в том, что при использовании лассо некоторые коэффициенты становятся равны
точно нулю.

---

## Лабораторная работа № 5

### Линейные модели для классификации.

Для линейных моделей классификации `граница принятия решений` (`decision boundary`) является линейной функцией аргумента. Другими словами, (бинарный) линейный классификатор – это классификатор, который разделяет два класса с помощью линии, плоскости или гиперплоскости.

Существует масса алгоритмов обучения линейных моделей. Два критерия задают различия между алгоритмами:

- Измеряемые метрики качества подгонки обучающих данных
- Факт использования регуляризации и вид регуляризации, если она используется

В силу технико-математических причин невозможно скорректировать `w` и `b`, чтобы
минимизировать количество неверно классифицированных случаев, выдаваемое алгоритмами,
как можно было бы надеяться. С точки зрения поставленных нами целей и различных сфер
применения различные варианты метрик качества подгонки (так называемые `функции потерь`
или `loss functions`) не имеют большого значения.

Двумя наиболее распространенными алгоритмами линейной классификации являются
`логистическая регрессия (logistic regression)`, реализованная в классе
`linear_model.LogisticRegression`, и `линейный метод опорных векторов (linear support vector machines)` или `линейный SVM`, реализованный в классе `svm.LinearSVC` (`SVC` расшифровывается как `support vector classifier` – классификатор опорных векторов).

Логистическая регрессия является алгоритмом классификации, а не алгоритмом регрессии.

По умолчанию обе модели используют `L2 регуляризацию`, тот же самый метод, который используется в гребневой регрессии.

Для `LogisticRegression` и `LinearSVC` компромиссный параметр, который определяет степень регуляризации, называется `C`, и более высокие значения `C` соответствуют меньшей регуляризации. Другими словами, когда вы используете высокое значение параметра `C`, `LogisticRegression` и `LinearSVC` пытаются подогнать модель к обучающим данным как можно лучше, тогда как при низких значениях параметра `C` модели делают больший акцент на поиске вектора коэффициентов (`w`), близкого к нулю.

## Лабораторная работа № 6

### Линейные модели для мультиклассовой классификации.

Многие линейные модели классификации предназначены лишь для бинарной классификации и не распространяются на случай
мультиклассовой классификации (за исключением логистической регрессии). Общераспространненный подход, позволяющий
распространить алгоритм бинарной классификации на случай мультиклассовой классификации называет подходом `один против остальных`
(`one-vs.-rest`).

В этом подходе `для каждого класса` строится `бинарная модель`, которая пытается `отделить` этот `класс` `от всех остальных`,
в результате чего количество моделей определяется количеством классов. Для получения прогноза точка тестового набора
подается на все бинарные классификаторы. Классификатор, который выдает по своему классу наибольшее значение, «побеждает»
и метка этого класса возвращается в качестве прогноза.

`Используя бинарный классификатор` для каждого класса, мы `получаем один вектор коэффициентов (w) и одну константу (b)
 по каждому классу`. Класс, который получает наибольшее значение согласно нижеприведенной формуле, становится
присвоенной меткой класса.

`Математический аппарат` мультиклассовой логистической регрессии несколько отличается от подхода «`один против остальных`»,
однако он также дает один вектор коэффициентов и константу для каждого класса и использует тот же самый способ получения
прогнозов.

Атрибут `coef_` имеет форму (3, 2) (матрица 3x2), это означает, что каждая строка `coef_`
содержит вектор коэффициентов для каждого из трех классов, а каждый столбец содержит
коэффициент для конкретного признака (в этом наборе данных их два). Атрибут `intercept_` теперь
является одномерным массивом, в котором записаны константы классов.

`Про середину треугольника`

> Однако что насчет треугольника в середине графика? Все три бинарных классификатора
> относят точки, расположенные там, к «остальным». Какой класс будет присвоен точке,
> расположенной в треугольнике? Ответ – класс, получивший наибольшее значение по формуле
> классификации, то есть класс ближайшей линии.

#### Преимущества, недостатки и параметры

Основной параметр линейных моделей – параметр регуляризации, называемый `alpha` в
моделях регрессии и `C` в `LinearSVC` и `LogisticRegression`. Большие значения `alpha` или маленькие
значения `C` означают простые модели. Конкретно для регрессионных моделей настройка этих
параметров имеет весьма важное значение. Как правило, поиск `C` и `alpha` осуществляется по
логарифмической шкале. Кроме того вы должны решить, какой вид регуляризации нужно
использовать: `L1` или `L2`. Если вы полагаете, что на самом деле важны лишь некоторые признаки,
следует использовать `L1`. В противном случае используйте установленную по умолчанию `L2`
регуляризацию. Еще `L1` регуляризация может быть полезна, если интерпретируемость модели
имеет важное значение.

Преимущества линейных моделей:

- Очень быстро обучаются.
- Быстро прогнозируют.
- Масштабируются на очень большие наборы данных, также хорошо работают с разреженными
  данными.
- Позволяют относительно легко понять, как был получен прогноз, при помощи формул, которые мы видели
  ранее для регрессии и классификации.

Как правило, линейные модели хорошо работают, когда количество признаков превышает
количество наблюдений. Кроме того, они часто используются на очень больших наборах данных,
просто потому, что не представляется возможным обучить другие модели.

Вместе с тем в низкоразмерном пространстве альтернативные модели могут показать более высокую обобщающую способность.

#### Цепочка методов (method chaining)

В общем, тут грится, что методы можно вызывать в одну строчку (через точку), так как они возвращают объект `self`.
Но надо аккуратно, потому что можно сделать код трудночитаемым. Не знаю зачем она про это написала, но пусть так.

## Лабораторная работа № 7

### Наивные байесовские классификаторы (Naive Bayesian)

Наивные `байесовские классификаторы` представляют собой семейство классификаторов,
которые очень схожи с `линейными моделями`. Однако они имеют тенденцию обучаться быстрее.
Цена, которую приходится платить за такую эффективность – немного более низкая обобщающая
способность моделей Байеса по сравнению с линейными классификаторами типа `LogisticRegression` и `LinearSVC`

Причина, по которой наивные байесовские модели столь эффективны, заключается в том,
что они оценивают параметры, рассматривая каждый признак отдельно и по каждому признаку
собирают простые статистики классов. В `scikit-learn` реализованы три вида наивных байесовских
классификаторов: `GaussianNB`, `BernoulliNB` и `MultinomialNB`. `GaussianNB` можно применить к
любым непрерывным данным, в то время как `BernoulliNB` принимает бинарные данные,
`MultinomialNB` принимает счетные или дискретные данные (то есть каждый признак представляет
собой подсчет целочисленных значений какой-то характеристики, например, речь может идти о
частоте встречаемости слова в предложении). `BernoulliNB` и `MultinomialNB` в основном
используются для классификации текстовых данных

Классификатор `BernoulliNB` подсчитывает ненулевые частоты признаков по каждому
классу.

```python
X = np.array([[0, 1, 0, 1], [1, 0, 1, 1], [0, 0, 0, 1], [1, 0, 1, 0]])
y = np.array([0, 1, 0, 1])
```

Здесь у нас есть четыре точки данных с четырьмя бинарными признаками. Есть два класса
0 и 1. Для класса 0 (первая и третья точки данных) первый признак равен нулю два раза и отличен
от нуля ноль раз, второй признак равен нулю один раз и отличен от нуля один раз и так далее.

Чё?

#### Преимущества, недостатки и параметры

Две другие наивные байесовские модели `MultinomialNB` и `GaussianNB`, немного отличаются
с точки зрения вычисляемых статистик. `MultinomialNB` принимает в расчет среднее значение
каждого признака для каждого класса, в то время как `GaussianNB` записывает среднее значение, а
также стандартное отклонение каждого признака для каждого класса.
Для получения прогноза точка данных сравнивается со статистиками для каждого класса и
прогнозируется наиболее подходящий класс.

`MultinomialNB` и `BernoulliNB` имеют один параметр `alpha`, который контролирует сложность
модели. Параметр `alpha` работает следующим образом: алгоритм добавляет к данным зависящее
от `alpha` определенное количество искусственных наблюдений с положительными значениями для
всех признаков. Это приводит к «сглаживанию» статистик. Большее значение `alpha` означает более
высокую степень сглаживания, что приводит к построению менее сложных моделей. Алгоритм
относительно устойчив к разным значениям `alpha`. Это означает, что значение `alpha` не оказывает
значительного влияния на хорошую работу модели.

`GaussianNB` в основном используется для данных с очень высокой размерностью, тогда как
остальные наивные байесовские модели широко используются для разреженных дискретных
данных, например, для текста. `MultinomialNB` обычно работает лучше, чем `BernoulliNB`, особенно
на наборах данных с относительно большим количеством признаков, имеющих ненулевые частоты.

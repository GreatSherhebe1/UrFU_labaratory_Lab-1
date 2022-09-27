# Анализ данных и искуственный интеллект Лабараторная № 1 конструкция языка python на примере реализации линейной регрессии
Отчет по лабораторной работе #1 выполнил:
- Устинов Никита Валерьевич
- РИ210910
Отметки о выполнении задания
(undone-#, done-*)

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

Структура отчета


## Цели работы
Ознакомиться с основными операторами языка Python на примере реализации линейной регрессии.

## Задание 1
### Написать программы Hello world на Python и Unity

## Задание 2
### В разделе "ход работы" пошагово выполнить каждый пунк с описание и примром реализации задачи по теме лабораторной работы

## Задание 3
### Изучить код на Python и ответить на вопросы:
- Должна ли величина "loss" стремиться к 0 при изменении исходных данных? Ответить на вопрос, привести пример кода, подтверждающий ответ
- Какова роль параметра "Lr" ? Ответить на вопрос, привести пример кода, подтверждающий ответ (можно изменять значение параметра).

Ход работы:
### Задание 1

- Создал файл блокнота в Google-colab. Написал команду вывода фразы "Hello world!" в консоль. Сохранил файл на Google Диск (скриншоты 1.1, 1.2)
- Создал новый 2D проект в Unity. Создал скрипт и написал программу на C#, выводящую нужную фразу (скриншот 1.3)

### Задание 2

1) Произвел подготовку данных для работы с алгоритмом линейной регрессии. Установил 10 видов данных случайным образом в линейной зависимости;
2) Данные преобразуются в список (массив) для прямого вычисления при сложении, умножении;
3) После выбрал случайное значение от 0 до 1 и компенсатор изменения передвижения точки по графику
4) Написал закон изменения функции, графиком которой является прямая, она же модель (model)
5) Написал функции линейной регрессии и её оптимизации для итерации
6) Запустил программу и построил графики по каждому (1-6) шагам (графики в папке задание 2).

```py

In[]:
import numpy as np
import matplotlib.pyplot as  plt
%matplotlib inline

x = [2, 11, 13, 16, 25, 36, 49, 56, 76, 84]
x = np.array(x)
y = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
y = np.array(y)


a = np.random.rand(1)
print(a)
b = np.random.rand(1)
print(b)
Lr = 0.000001


def model(a, b, x):
  return a * x + b


def loss_function(a, b, x, y):
  num = len(x)
  prediction = model(a, b, x)
  return (0.5 / num) * (np.square(prediction - y)).sum()


def optimize(a, b, x, y):
  num = len(x)
  prediction = model(a, b, x)
  da = (1.0 / num) * ((prediction - y) * x).sum()
  db = (1.0 / num) * (prediction - y).sum()
  a = a - Lr * da
  b = b - Lr * db
  return a, b

def iterate (a, b, x, y, times):
  for i in range(times):
    a, b = optimize(a, b, x, y)
  return a, b


a, b = iterate(a, b, x, y, 10000)
prediction = model(a, b, x)
loss = loss_function(a, b, x, y)
print(a, b, loss)
plt.scatter(x,y)
plt.plot(x,prediction)

plt.scatter(x, y)

```
### Задание 3

1)
```py
# loss increase
x = [1100, 2200, 3003, 4400, 5500, 6600, 7700, 8800, 9900, 10000]
x = np.array(x)
y = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
y = np.array(y)

# loss decrease
x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
x = np.array(x)
y = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
y = np.array(y)
```
чем больше значения x и y и разница между ними, тем больше значение loss, при уравновешивании значений x и y loss стремится к нулю (скриншоты 3.1 - 3.2).

2) параметр Lr отвечает за величину разброса значений графика и величины Lr: чем больше Lr -> меньше изменяется loss и наоборот (скриншоты 3.3 - 3.4)

## Выводы
В ходе работы ознакомился с основами языка Python, работы с его операторами, разобрался в использовании линейной регрессии, рассмотрел зависимости её значений от различных параметров.

## Приложение
### Основная литература:
1) Грас Дж. Data science. Наука о данных с нуля: Пер. с англ. - СПб.: БХВ- Петербург, 2020.-336с.: ил.
2) Николаенко С.И., Кадурин А.А., Архангельская Е.О. Глубокое обучение.-СПб.:Питер,2017.-480с.
3) Гудфеллоу Я., Бенджио И., Курвилль А. Глубокое обучение / пер. с анг. А.А.Слинкина.-2-е изд., испр. - Москва : ДМК Пресс, 2018. - 652с.: цв. ил.
4) Шолле Ф. Глубокое обучение на Python/ - СПб.: Питер, 2018. - 400с.

### Дополнительная литературра:
1) Клетте, Рейнхард. Компьютерное зрение. Теория и алгоритмы. -М.: ДМК Пресс, 2019
2) Пойнтер, Ян. Программируем с PyTorch. Создание приложений глубокогго обучения. -СПб: из-во Питер, 2020. -256 с.
3) Траск Эндрю. Грокаем глубокое обучение. -СПб.: Питер, 2019. - 352 с.
4) Ян, Э.С. Программирование компьютерного зрения на языке Python / Э.С. Ян; перевод с английского А.А. Слинкин. -Москва: ДМК Пресс, 2016. - 312 с.
5) Он-лайн курс  "Нейронные сети и компьютерное зрение". - URL: https://stepik.org/course/50352/promo.
6) приведенный в работе код: https://colab.research.google.com/drive/1UUPyIFC8FeTLLJSpfxn875iYEN-n9Y_8

## Комп'ютерні системи імітаційного моделювання
## СПм-22-5, **Вінтонович Микита Сергійович**
### Лабораторна робота №**2**. Редагування імітаційних моделей у середовищі NetLogo

<br>

### Варіант 5, модель у середовищі NetLogo:
[Fire Extension](http://www.netlogoweb.org/launch#http://www.netlogoweb.org/assets/modelslib/IABM%20Textbook/chapter%203/Fire%20Extensions/Fire%20Simple%20Extension%202.nlogo)

<br>

### Внесені зміни у вихідну логіку моделі, на власний розсуд:

**Додано наступні глобальні змінні у setup:**.

fireFighters - кількість пожежників
fireFightersSteps - додаткова змінна для підрахування наступної позиціїї пожежників
fireFighterColor - колір пожежника
distanceToFire - початкова відстань до лінії вогню

<pre>
globals [
  initial-trees   ;; how many trees (green patches) we started with
  fireFighterColor
  distanceToFire
  itterationsCount
]

turtles-own [
  isFire?
  speed
]

breed [firefighters firefighter]
</pre>

**Додано процедуру додавання пожежників перед початком симуляції:**.

<pre>
to makeAgents

  set distanceToFire (min-pxcor + distance-to-fire)

  create-turtles firefighters-count [
    setxy distanceToFire random-ycor
    set color fireFighterColor
    set isFire? false
    set speed 0.2
  ]

  create-firefighters firefighters-count [
    setxy distanceToFire random-ycor
  ]

end
</pre>

**Додано процедуру переміщення пожежників під час симуляції:**.

<pre>
to moveAgents

  ask turtles [
    if any? other turtles in-radius 1 with [isFire?] [
      set isFire? true
      set color cyan
    ]
    forward 1
  ]

end
</pre>

**Додано процедуру боротьби пожежників з вогнем під час симуляції:**.

<pre>
to fightWithFire

  let nearFire other turtles in-radius 1 with [isFire?]

  ask nearFire [
    if random-float 1 < 0.7 [
      set isFire? false
      set color white
    ]
  ]

end
</pre>

![Скріншот моделі в процесі симуляції](example.png)

Фінальний код моделі та її інтерфейс доступні за ![посиланням](https://github.com/mykavin/CSMS-SPm-22-5_Variant-5/blob/lab-2/V5/Lab-2/Project/Fire%20Simple%20Extension%202.nlogo).

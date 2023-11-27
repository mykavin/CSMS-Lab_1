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
fighterRadius - радіус дії пожежника
fireFighterSpeed - швидкість пожежника
fireFighterColor - колір пожежника
distanceToFire - початкова відстань до лінії вогню
agentsOn - включити/виключити агентів у симуляції

<pre>
globals [
  initial-trees   ;; how many trees (green patches) we started with
  fireFighterColor
  distanceToFire
  fireFighterSpeed
  fighterRadius
  agentsOn
]

turtles-own [
  speed
  fightRadius
]

breed [firefighters firefighter]
</pre>

**Додано процедуру додавання пожежників перед початком симуляції:**.

<pre>
to makeAgents

  set distanceToFire (min-pxcor + distance-to-fire)

  create-turtles firefighters-count [
    setxy distanceToFire random-ycor
    set color white
    set speed fireFighterSpeed
    set fightRadius fighterRadius
  ]

  create-firefighters firefighters-count [
    setxy distanceToFire random-ycor
  ]

end
</pre>

**Додано процедуру переміщення пожежників під час симуляції:**.

<pre>
to moveRandom

  rt random 50
  lt random 50
  fd 1

  set color fireFighterColor

end

to moveToSearchTheFire [target]

  face target
  fd speed

end
</pre>

**Додано процедуру боротьби пожежників з вогнем під час симуляції:**.

<pre>

to fightWithFire

  let fire-neighbors patches in-radius fight-radius with [pcolor = red]
  ask fire-neighbors [
    if random-float 1 < probability-fight-fire [
      ask myself [
        set pcolor green
      ]
    ]
  ]
end
</pre>

![Скріншот моделі в процесі симуляції](example.png)

Фінальний код моделі та її інтерфейс доступні за ![посиланням](https://github.com/mykavin/CSMS-SPm-22-5_Variant-5/blob/lab-2/V5/Lab-2/Project/Fire%20Simple%20Extension%202.nlogo).

# Структура языка

**Содержание:**

- [Строки и отступы](#строки-и-отступы)  
- [Утверждения](#утверждения-statements)      
- [Токены](#токены)
    - [Идентефикаторы](#идентефикаторы)    
    - [Разделители](#разделители)   
    - [Литералы](#литералы)   
    - [Операторы](#опреаторы)   
    - [Ключевые слова](#ключевые-слова)
- [Переменные и ссылки](#переменные-и-ссылки)
- [Управление потоком выполнения](#управление-потоком-выполнения)
    - [Ветвление](#ветвление)
    - [Цикл while](#цикл-while)
    - [Цикл for](#цикл-for)
    - [break](#break)
    - [continue](#continue)
    - [else в циклах](#else-в-циклах)
    - [pass](#pass)

## Строки и отступы

Любой скрипт на Python представляет собой последовательность *логических строк*, каждая из которых состоит из одной или нескольких *физических строк*. Физическая строка может содержать комментарии. Комментарием считается часть строки, идущая после символа #. Эта часть строки игнорируется интерпретатором. Помимо комментариев интерпретатором также игнорируются строки, состоящие только из символов табуляции. Такие строки считаются *пустыми* и служат для разбиения листингов кода на логические блоки.

    Совет: не пренебрегайте комментариями и пустыми строками. Несмотря на их полное игнорированием интерпретатором, эти элементы языка помогут вам четче и яснее структурировать ваши программы, а также улучшать читабельность вашего кода.

Для программистов, переходящих на Python с других языков, наподобие C или C++, будет необычно слышать, что конец любых утверждений и выражений в Python происходит с концом физической или логической строки, не требуя использования дополнительных разделителей типа точки с запятой. Как и в C++ слишком длинные физические строки могут быть разбиты на несколько физических строк и объединены в одну логическую с помощью символа \\. Однако этот стиль не рекомендуется, поскольку в Python присутствует более элегантное python-way решение. Интерпретатор Python автоматически объединяет физические строки, находящиеся в круглых ((), квадратных ([) и фигурных ({) скобках в одну логическую строку. Так что, не гнушайтесь использования этого механизма для повышения качества вашего кода.

```Python
# это физическая строка
light_velocity = 3e8

# а это логическая строка
very_long_string = 'this is very very very long string so long ' \
'so you need to postpone its part to the next physical line'

# логическая строка python-way
another_long_string = (
    'this is very very very long string so long '
    'so you need to postpone its part to the next physical line'
)
```

В отличие от C++ и многих других языков программирования, которые используют скобки или специальные ключевые слова для обозначения блока кода, Python использует отступы. Отступы - это единственный способ обозначить блок кода. Каждая логическая строка в вашей программе имеет свой уровень отступа. Блок кода - это непрерывная последовательность логических строк, имеющих одинаковый уровень отступа. Логическая строка с меньшим отступом завершает блок кода.

## Утверждения (statements)

Поимимо взгляда с позиции строк, вы можете смотреть на скрипт с точки зрения *простых* и *составных* утверждений. 

Простыми утверждениями называются утверждения, которые не содержат в себе прочих утверждений (да простят меня математики за подобные определения). Любое выражение, т.е. конструкция, порождающая некоторое значение, представляет собой просто выражение. В качестве примеров простых выражений можно привести вызов функций или операцию присваивания (или, как мы узнаем далее, операцию привязки).

Сложными утверждениями, по закону исключенного третьего, называются утверждения, которые содержат в себе не менее одного другого утверждения и осуществляют контроль их выполнения. Сложные утверждения имеют не менее одного положения (clause). Положения, принадлежащие к данному сложному утверждению имеют одинаковый отступ. Каждое положение обладает хедером, который обязательно начинается с ключевого слова и заканчивается двоеточием. За хедером следует набор утверждений, которые называются телом положения.

## Токены

Интерпретатор Python разбивает каждую логическую строку на последовательность языковых единиц, также известных, как токены. К токенам относятся: *идентефикаторы*, *разделители*, *литералы*, *операторы*, *ключевые слова*. Токены разделяются пробелами. Иногда разделение токенов пробелами необходимо, иногда - нет.

### Идентефикаторы

Идентефикатор - это имя, которое используется для обозначения переменных, функций, классов, модулей и прочих объектов. Идентефикаторы начинаются с буквы английского алфавита или с нижнего подчеркивания. За начальным символом следует сколько угодно букв, нижних подчеркиваний и цифр. Символы пунктуации недопустимы для использовании в идентефикаторах.

В Python используется следующее соглашение об идентефикаторых. Идентефикаторы переменных, функций и модулей пишутся в snake_case, идентефикаторы классов - в PascalCase.

Некоторые идентефикаторы, начинающиеся с двух нижних подчеркиваний и заканчивающиеся двумя нижними подчеркиваниями, являются зарезервированными специальными именами.

**Важно:** идентефикаторы чувствительны к регистру.

```Python

my_variable = 5         # валидное имя
MyVariable = 6          # тоже валидное имя

_var1 = 1               # и это валидное имя
__len__ = 4             # переопределение заразарвированной переменной
                        # так лучше никогда не делать

2var = 2                # SyntaxError

```

### Разделители 

В Python используются следующие символы и комбинации символов в качестве разделителей в выражениях, литералах и для прочих целей в различных утверждениях:

```Python
(   )   [   ]   {   }
,   :   .   `   =   ;   @
+=  -=  *=  /=  //  %=
&=  |=  ^=  >>= <<= **=
```

Также некоторые символы имеют специальные значения. К их числу относятся:

```Python
'   "   #   \
```

### Литералы

Литералы - это прямое указание в программы значения некоторых данных. Ниже приведены пример числовых литералов:

```Python
1                   # целое число
3.14                # число с плавающей точкой
1.0j                # комплексное число
```


### Опреаторы

Следующие символы используются Python в качестве операторов:

```Python
+   -   *   /   %   **  //  <<  >>  &
|   ^   ~   <   <=  >   >=  !=  ==
```

### Ключевые слова

Ключевые слова - это набор зарезервированных идентефикаторов, которые используются в Python для специальных синтаксических конструкций. Из этого следует, что вы не можете использовать ключевые слова в качестве идентефикатора дрегих объектов. Ключевые слова содержат только идентефикаторы в нижнем регистре. Некоторые ключевые слова служат для начала сложных утверждений, в то время как другие являются операторами.

## Переменные и ссылки

Программы, написанные на Python, получают доступ к данным с помощью ссылок. Ссылка - это некоторое имя, которое ссылается на какое-то значение (объект). Ссылка может быть представлена в виде переменной, атрибута или элемента коллекции. Ссылки в Python не имеют типа данных. Да, объект, на который ссылается ссылка имеет строго определенный тип данных (о типах данных мы поговорим в одной из следующих лекций), но сама ссылка в один момент времени может ссылаться на целое число, затем быть перепривязана к строке, ну и в конце концов может быть привязана к пользовательском типу данных. Далее мы подробнее рассмотрим переменные.

Как следует из предыдущего абзаца, переменные в Python - это ссылки на настоящие объекты в памяти. В отличие от C или C++ в Python нет объявления переменных. Переменные начинают существовать с момента выполнения привязки (определения переменной). Привязка осуществляется с использованием операции присваивания:

```Python
num1 = 5
num2 = num1
num1 = 6
```

Выполняя первое утверждение в памяти компьютера будет создан объек "целое число" со значением 5, ссылка на этот объект будет привязана к переменной num1. Во втором примере новый объект в памяти создан не будет, переменная num2 будет указывать на тот же объект в памяти, что и num1. В третьем утверждении num1 была перепривязана. Здесь происходит почти все то же, что происходило в первой строке листинга кода. Единственно исключение - это отвязка ссылки num1 от объект "целое число 5" и привязка этой ссылки к объекту "целое число 6". В итоге, после выполнения этого куска кода в памяти компьютера будет два объекта типа "целое число": со значением 5, на который в программе ссылается переменная num2, и со значением 6, на который ссылается переменная num1. 

Для лучшего понимания того, что происходит, можно использовать встроенную функцию `id()`, которая принимает на вход объект Python и возвращает целое число - его уникальный id.

*Код:*
```Python
num1 = 5
num2 = num1

print(id(num1) == id(num2))

num1 = 6

print(id(num1) == id(num2))

```
*Вывод:*
```Console
>>> True
>>> False
```

В данном примере отчетливо видно, что в момент определения переменной num2, ссылки num1 и num2 ссылаются на один и тот же объект в памяти (их id равны). После перепривязки num1, ссылки num1 и num2 начинают ссылаться на два разныъ объекта в памяти.

Понимание этой концепции является очень важной, и ни раз пригодиться нам в будущем при работе с изменяемыми типами данных.

Поговорим немного о присваивании, ибо с ним не все так просто. В Python присутствует два вида присваивания: простое и составное. Простое присваивание используется для привязки - в этот момент может создаваться новый объект в памяти компьютера и новая ссылка, используется для перепривязки. Пока мы ничего не знаем (или притворяемся, что не знаем) о коллекциях, рассмотрим следующие интересные случаи использования простого присваивания:

```Python
a = b = c = 0           # случай 1
a = 5

a, b = b, a             # случай 2
```

В первом случае мы привязали сразу три ссылки к объекту со значеним 0. Во втором перепривязали a к b, a b - к a. Это работает так, как мы ожидаем, потому что операция присваивания выполняется следующим образом: сначала вычисляется выражение, стоящее справа от знака =, затем осществляется превязка/перепревязка. В примере 1 мы сначала вычислили значение литерала 0 (сюрприз, сюрприз, оно оказалось равным нулю), затем привязали к объекту с этим значением ссылку с, затем вычислили значение ссылки с и привязали к ней b, и т.д. Во втором случае мы вычислил ссылки b и a и перепривязали a и b. Все просто!

Помимо простого присваивания в Python есть операторы составного присваивания. Обычно они имеют следующий вид: <бинарный оператор>=. В большинстве своем легко понять, что и как делают эти операторы. Интересующая нас вещь заключается в том, что в отличие от простого присваивания, при составном присваивании никогда не создаетя новой ссылки, для осуществления составного присваивания переменная должна уже сущестовать в программе. 

## Управление потоком выполнения

Поток выполнения программы - это порядок, в котором выполняется код. Порядок выполнения программы в Python зависит от конструкций ветвления, циклов и вызовов функции (о которых мы поговорим в одной из следующих лекци).

### Ветвление

Ветвление - это сложное утверждение, которое включает в себя положения if, elif и tlse. В самом общем виде конструкция ветвления выглядит следующим образом:

```Python
if expression1:
    do_something1()

elif expression2:
    do_somethin2()

elif expression3:
    do_somethong3()

else:
    do_another_thing()
```

Положения elif и else являются не обязательными. 

Вы вольны использовать любые выражения в положениях if и elif. Использование выражений таким образом называют использованием выражения в булевом контексте. В этом контексте любое значение приводится к типу bool и принимает значения True или False. Здесь существует существенная разница между фразой "выражение принимает значение True" и "выражение расценивается, как True". Когда мы работаем с ветвлением нас интересует именно второй вариант.

Если первое выражение расценивается как True, то выполняется блок кода, который следует за ним. Иначе Python оценивает выражение в первом блоке elif. Python будет оценивать все выражения, пока одно из них не будет расценено, как True, или пока мы не дойдем до блока else/конца ветвления.

### Цикл while

Цикл while предназначен для выполнения некоторой последовательности действий до тех пор, пока выражение, стоящее в условии цикла, расценивается как True. 

```Python
while expression:
    do_something()
```

### Цикл for

Цикл for осуществляет выполнение некоторой последовательности действий, котонтролируемую итерируемым объектом (рассмотрим позже в лекциях).

```Python
for target in iterable:
    do_something()
```

target - переменная контроля цикла. На каждой итерации она перепривязывается к новому элементу итерируемого объекта iterable. Что может показаться интересным - переменная target будет доступно вне цикла for даже после его завершения и содержать в себе последний рассмотренный элемент из iterable.

### break

Ключевое слово break может быть использовано только в циклах для мгновенного прерывания этих самых циклов. Когда break выполняется цикл завершается. Если имеет место вложенный цикл, содержащий break, break прерывает только вложенный цикл, в котором он встретился, не затрагивая выполнение внешнего цикла.

### continue

Как и break, continue может быть использовано только в циклах для пропуска части тела цикла. Обычно continue используется для уменьшения степени вложенности кода в теле цикла.

### else в циклах

Помимо очевидного использования else в ветвлении, else так же может быть использовано вместе с циклами. В контексте циклов слово else может сбивать с толку, поскольку по смыслу гораздо сильнее подходило бы слово then, но добавление нового ключевого слова испортило бы обратную совместимость, чего создатель языка Python Гвидо Ван Россум старательно избегает. Собственно, блок else, размещенный после цикла, будет выполнятся только в том случае, если цикл был завершен "естественным путем": без прерывания в теле цикла с помощью инструкции break.

### pass

Тело циклов и ветвлений не может состоять из пустых строк, однако мы не всегда ходим что-то делать при выполнении определенного условия. С этой целью в языке существует пустая команда pass, которая идеально подходит как раз для описанного случая.
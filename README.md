# Программа перевода словосочетаний в шаблоны LSPL. #
#### Написана на Python3 ####

Программа обрабатывает словосочетания, вид которых описан далее в форме РБНФ.

В python-скрипте можно задать входной файл, в каждой строке которого приводится <словосочетание>

Обратите внимание, что скобки `[]` являтся терминальными символами, а не конструкцией, означающей 0 или 1 вхождение.
Скобки `()` также являются терминальными символами.
Однако `{}` обозначают 0 или более вхождений.

### ` <словосочетание> = <инфинитив> <зависимые части> | <инфинитив>  ` ###

 <словосочетание> будет преобразовано в шаблон одного словосочетания, если зависимых частей 0 или 1, или несколько шаблонов словосочетаний вида <инфинитив><зависимая часть>, каждый из которых соответствует одной зависимой части

### ` <зависимые части> = <зависимая часть>{; <зависимые части>}  ` ###

т. е. зависимые части задаюся через точку с запятой с последующим пробелом

Фактически, <словосоветание> вида

### ` <инфинитив> <зависимая часть 1>; <зависимая часть 2>  ` ###

обрабатывается так же, как и два словосочетания, идущий в последовательных строках:

 ` <инфинитив> <зависимая часть 1>  `

 ` <инфинитив> <зависимая часть 2>  `

### ` <зависимая часть> = {<слова> | [<слова>{, [<слова>}] | (<слова с заменяемыми местоимениями>{, <слова с заменяемыми местоимениями>})}  ` ###

т. е. зависимая часть состоит из последовательности слов, слов в квадратных скобках для конструкций, вхождение шаблонов которых будет опциональным (альтернативы указываются через запятую), слов в круглых скобках опять же для опциональных конструкций, но местоимения в которых будут заменены на произвольные существительные, соответсвующие этим местоимениям по падежам. (Например, из конструкции (чего, о чём) будет получен шаблон [N2<c=gen> | Pr2<о> N3<c=prep>])
<зависимая часть> должна быть ненулевой.

### ` <слова> = <слово> {<слово> | [<слово>]}  ` ###

Каждое слово будет преобразовано в свой lspl-шаблон с приписыванием падежа в случае его наличия. Если слово в квадратных скобках, вхождение его шаблона будет опциональным.

### ` <слова с заменяемыми местоимениями> =  <слово> {<слово>}  ` ###

как отмечено выше, из местоимений будут получены шаблоны произвольных существительных с соответствующим согласованием.

### `<слово>` ###
представляет собой какое-то слово русского языка

### `<инфинитив>` ###
глагол в форме инфинитива

هذا الفصل مليء بأشياء جديدة. استمر!
إذا كان أي شيء غير منطقي الآن ، فلا تقلق:
ما نشرحه الآن سيعلمك أشياء مهمة
سنستخدمها في درس آخر.

جرب كل مثال في هذا الدرس ؛
ما يطبعه بايثون هو جزء مهم من الدرس.

# المصفوفات (Lists)

اليوم سنعرض لك كيفية العمل مع *المصفوفات*.
سنستخدم الأقواس المربعة كثيرًا لأن هذه هي الطريقة التي يتم بها إنشاء المصفوفات:

```python
numbers = [1, 1, 2, 3, 5, 8, 13]
print(numbers)
```


المصفوفة (list) هي قيمة يمكن أن تحتوي على العديد من القيم الأخرى.
تمامًا مثل النص (string) الذي يحتوي على تسلسل من الأحرف (characters)،
تحتوي المصفوفة (list) على تسلسل من أي شيء. الأرقام ، على سبيل المثال.
وكما يمكننا استخدام حلقة `for`
لطباعة النصوص (strings) حرفًا بحرف ،
يمكننا التكرار على عناصر المصفوفة (list elements):

```python
for number in numbers:
    print(number)
```

المصفوفات (lists) في البرامج شائعة جدًا:
يمكن استرداد ملف كمصفوفة (list) من النصوص (strings)
سطرًا بسطر.
يمكن استخدام مصفوفة (list) من النصوص (strings) مثل `7 ♥`
و `K ♣` كمجموعة من البطاقات.
الرياضيات مليئة بالمصفوفات العددية (numerical lists) و
لكل خدمة عبر الإنترنت مصفوفة أو  قائمة  (list) من المستخدمين.


يمكن أن تكون القيم الموجودة في المصفوفة (list) من أي نوع ،
يمكننا حتى مزج أنواع مختلفة في مصفوفة واحدة
(على الرغم من أننا لن نصادف مثل هذه المصفوفات المختلطة
في كثير من الأحيان - يتم استخدامها أكثر في المجموعات (tuples) ،
التي سنخبرك عنها لاحقًا):

```python
list = [1, 'abc', True, None, range(10), len]
print(list)
```

## الاختيار من المصفوفات (Selection from lists)

أنت تعرف بالفعل العملية الأساسية مع المصفوفات ،
حلقة `for`.
العملية الثانية الأكثر أهمية هي اختيار
عناصر فردية (individual elements).
يعمل هذا بنفس الطريقة كما في النصوص (strings): الأقواس المربعة و
رقم العنصر (element number). يتم ترقيم عناصر المصفوفة (list elements) من الصفر ،
تمامًا مثل الأحرف (characters) في النصوص (strings) ؛ تشير الأرقام السالبة إلى العناصر من النهاية.

```python
print(numbers[2])
```

نستخدم الأقواس المربعة للوصول إلى المجموعات الفرعية (subsets).

```plain
  ╭───┬───┬───┬───┬───┬───┬───┬───╮
  │ P │ y │ L │ a │ d │ i │ e │ s │
  ├───┼───┼───┼───┼───┼───┼───┼───┤
  │   │   │   │   │   │   │   │   │
  0   1   2   3   4   5   6   7   8
 -8  -7  -6  -5  -4  -3  -2  -1

  ╰───────────────╯
  'PyLadies'[:4] == 'PyLa'

          ╰───────────────╯
        'PyLadies'[2:6] == 'Ladi'

                      ╰───────────╯
                      'PyLadies'[-3:] == 'ies'
```

يوضح لك كيفية كتابة الأرقام عندما تريد أجزاء من المصفوفة:

```python
print(numbers[2:-3])
```

## تغيير المصفوفات (Changing lists)

من الميزات المهمة للمصفوفات أنها ليست أرقامًا ولا نصوصًا
(ولا `True`/`False`/`None`) ،
يمكن تغيير المصفوفات (فهي قابلة للتغيير - mutable).

لا يمكن تغيير الأرقام - إذا كان لديك `a = 3` و
تكتب `a = a + 1` ، فلن يتغير الرقم `3`.
سيتم حساب رقم جديد `4` ، والمتغير `a`
سيتم تعيينه لهذا الرقم الجديد.

على النقيض من ذلك ، يمكن تغيير المصفوفات دون تعيين متغير لقيمة جديدة.
أبسط طريقة لتغيير المصفوفة هي إضافة عناصر
إلى نهايتها ، باستخدام طريقة `append`.
لا يُرجع القيام بذلك *أي شيء* (في الواقع يُرجع `None`)
ولكنه يغير المصفوفة التي نعمل عليها *في مكانها* (`append` يعني
أضف إلى *نهاية* المصفوفة). جربه:

```python
prime_numbers = [2, 3, 5, 7, 11, 13, 17]
print(prime_numbers)
prime_numbers.append(19)
print(prime_numbers)
```

يمكن أن يكون تغيير القيمة هذا مفاجئًا في بعض الأحيان ،
لأن متغيرات متعددة يمكن أن يكون لها نفس القيمة.
لأن القيمة نفسها تتغير ، قد يبدو الأمر
أن المتغير "يتغير دون أن نلمسه":

```python
a = [1, 2, 3] # creates a list 'a' # إنشاء مصفوفة 'a'
b = a         # no new list is created, 'b' just points to 'a' # لم يتم إنشاء مصفوفة جديدة ، 'b' يشير فقط إلى 'a'

# the list created in the first row now has two variable names: "a" and "b",
# but we are still working with just one and the same list:
# المصفوفة التي تم إنشاؤها في الصف الأول لها الآن اسمان للمتغيرات: "a" و "b" ،
# لكننا ما زلنا نعمل بمصفوفة واحدة ونفسها فقط:

print(b)
a.append(4)
print(b)
```

## المزيد من طرق تعديل المصفوفات (More ways to edit lists)

بصرف النظر عن طريقة `append` التي تضيف
عنصر واحد فقط ، هناك أيضًا طريقة `extend` ،
التي يمكن أن تضيف المزيد من العناصر.
العناصر المراد إضافتها هنا تكون على شكل مصفوفة:

```python
more_prime_nr = [23, 29, 31]
prime_numbers.extend(more_prime_nr)
print(prime_numbers)
```

يمكن أن تعمل طريقة `extend` مع أخرى
أنواع المتغيرات - يمكن أن تعمل مع أي شيء
يمكننا استخدام حلقة `for` عليه: على سبيل المثال ،
نصوص فردية ، صفوف من الملفات ، أو أرقام من `()range`.

```python
listA = []
listA.extend('abcdef')
listA.extend(range(10))
print(listA)
```

## تغيير العناصر (Changing elements)

يمكنك تغيير عناصر فردية من المصفوفات ،
ببساطة عن طريق تعيين قيمة للعنصر ،
كما لو كان متغيرًا:

```python
numbers = [1, 0, 3, 4]
numbers[1] = 2
print(numbers)
```

يمكنك أيضًا تعيين قيم جديدة لمصفوفة فرعية - في هذه الحالة
يتم استبدال المجموعة الفرعية بالقيم الفردية التي نكتبها.
كما هو الحال مع `extend` ، يمكنك استبدال العناصر بأي شيء
يعمل مع حلقات `for` - مصفوفة ، نص ، `()range` ، إلخ.

```python
numbers = [1, 2, 3, 4]
numbers[1:-1] = [6, 5]
print(numbers)
```

## حذف العناصر (Deleting elements)

يمكننا أيضًا تغيير طول
المصفوفة عن طريق استبدال مصفوفة فرعية بعدد أقل من العناصر ،
أو عن طريق إزالة بعض العناصر تمامًا:

```python
numbers = [1, 2, 3, 4]
numbers[1:-1] = [0, 0, 0, 0, 0]
print(numbers)
numbers[1:-1] = []
print(numbers)
```

هذا الشكل من حذف العناصر غامض إلى حد ما ،
لذلك لدينا أمر خاص يسمى `del`.
يحذف كل ما نطلبه منه - فردي
عناصر ، مصفوفات فرعية وحتى متغيرات!

```python
numbers = [1, 2, 3, 4, 5, 6]
del numbers[-1]
print(numbers)
del numbers[3:5]
print(numbers)
del numbers
print(numbers)
```

طرق حذف أخرى هي:
* `pop` ، التي تزيل *وتُرجع* العنصر الأخير في المصفوفة - على سبيل المثال ، إذا
  لدي مصفوفة بطاقات في مجموعة ، فإن `pop` يشبه "سحب بطاقة".
* `remove` ، التي تجد العنصر في المصفوفة وتزيله ،
* `clear` ، التي تمسح المصفوفة بأكملها.

```python
numbers = [1, 2, 3, 'abc', 4, 5, 6, 12]
last = numbers.pop()
print(last)
print(numbers)

numbers.remove('abc')
print(numbers)

numbers.clear()
print(numbers)
```

## الترتيب (Sorting)

ولدينا أيضًا طريقة `sort` تقوم بترتيب عناصر المصفوفة.

```python
listA = [4, 7, 8, 3, 5, 2, 4, 8, 5]
listA.sort()
print(listA)
```

لكي يتم ترتيبها ، يجب أن تكون عناصر المصفوفة
*قابلة للمقارنة* - يجب أن نكون قادرين على استخدام عامل التشغيل `<` معها.
لا يمكن ترتيب مصفوفة مختلطة من الأرقام والنصوص.
يحدد العامل `<` كيف سيتم ترتيب العناصر بالضبط
(على سبيل المثال ، الأرقام حسب الحجم ؛ النصوص وفقًا لـ "الأبجدية" الخاصة
حيث تكون الأحرف الكبيرة أصغر من الأحرف الصغيرة ، إلخ).

تحتوي طريقة `sort` على قيمة `reverse`.
إذا قمت بتعيينها إلى *True* ، فسوف تقوم بترتيب العناصر بترتيب عكسي.
القيمة الافتراضية هي *False* ، لذلك إذا كنت تريد أن تكون العناصر
مرتبة من الأصغر إلى الأكبر ، فلا يتعين عليك تحديد هذه القيمة.

```python
listA = [4, 7, 8, 3, 5, 2, 4, 8, 5]
listA.sort(reverse=True)
print(listA)
```

## طرق أخرى (Other methods)

الكثير مما يمكننا فعله بالنصوص ، يمكننا فعله أيضًا بالمصفوفات.
على سبيل المثال  الإضافة والضرب  - يمكننا صنع مقطوعة موسيقية كالتالي -:

```python
melody = ['C', 'E', 'G'] * 2 + ['E', 'E', 'D', 'E', 'F', 'D'] * 2 + ['E', 'D', 'C']
print(melody)
```

كما هو الحال مع النصوص ، لا يمكن إضافة المصفوفة إلا إلى مصفوفات أخرى
- ليس إلى نص أو إلى رقم.

الطرق المعروفة الأخرى هي `len` و `count` و `index` ،
وعامل التشغيل `in`.

```python
print(len(melody)) # Length of the list # طول المصفوفة
print(melody.count('E')) # How many 'E's are in the list? # كم عدد 'E' الموجودة في المصفوفة؟
print(melody.index('E')) # Position of the first 'E' # موضع أول 'E'
print('E' in melody) # Is 'E' in the list? # هل 'E' موجودة في المصفوفة؟
```

تعمل الطرق الثلاثة الأخيرة بشكل مختلف قليلاً:
بالنسبة للنصوص ، فإنها تعمل على *نصوص فرعية* ،
بالنسبة للمصفوفات ، فإنها تعمل على عناصر *فردية*.
لذلك على الرغم من أن المقطوعة الموسيقية تحتوي على العناصر
`D` و `E` بجوار بعضهما البعض ، إلا أن `DE` ليس في المصفوفة:

```python
print('DE' in melody)
print(melody.count('DE'))
print(melody.index('DE'))
```

### مهمتان للتمرين (Two tasks for practice)

اكتب دالة (function) تُرجع العنصر الأوسط في المصفوفة (list).

{% filter solution%}
```python
test_list = [4, 12, 7]
def middle_element(l):
    # middle = l[ int(len(l) / 2) ]
    middle = l[ len(l) // 2 ]
    return middle

print(middle_element(test_list))
```
{% endfilter%}

اكتب دالة (function) تحسب عدد العناصر في المصفوفة (list) التي تكون أكبر من 10 وأصغر من 15:

{% filter solution%}
```python
test_list = [1, 3, 11, 13, 19]
def count_selected(l):
    counter = 0
    for number in l:
        if 10 <= number < 15:
            counter  = counter + 1
    return counter

print(count_selecter(test_list))
```
{% endfilter%}

## مصفوفة كشرط (A list as a condition)

يمكن استخدام المصفوفة (list) في عبارة `if` (أو `while`)
التي تكون صحيحة طالما يوجد شيء في تلك المصفوفة.
بعبارة أخرى ، `list` هي "اختصار" لـ `len(list) > 0`.

```python
if list:
    print ('There is something in the list!')
else:
    print ('The list is empty!')
```

يمكن استخدام النصوص (strings) بشكل مماثل.
وحتى الأرقام - يكون الشرط *True* إذا لم تكن صفرًا.

## إنشاء المصفوفات (Creating lists)

 مثلما تحول الدالة (function) `int`  القيم إلى
أعداد صحيحة والدالة (function) `str` تحول القيم إلى نصوص ،
فان الدالة (function) `list` تحول القيم إلى مصفوفة (list).
يمكننا إعطائها أي قيمة  (argument) ،
تقبل المعالجة بواسطة حلقة `for`.
سيتحول النص (string) إلى مصفوفة (list) من الأحرف (characters) ، وسيتحول الملف
 إلى مصفوفة (list) من الصفوف (rows)، وسيتحول `range`
إلى مصفوفة (list) من الأرقام.

```python
alphabet = list('abcdefghijklmnopqrstuvwxyz')
numbers = list(range(100))
print(alphabet)
print(numbers)
```

يمكن للدالة (function) `list` أيضًا إنشاء مصفوفة (list) من مصفوفة (list).
قد يبدو الأمر عديم الفائدة ، لكنه ليس كذلك - فهو ينشئ مصفوفة (list) *جديدة*
غير معتمدة على المصفوفة القديمة.
ستحتوي على نفس العناصر بنفس الترتيب ،
لكنها لن تكون نفس المصفوفة:
يمكنك تغييرها بشكل مستقل عن المصفوفة القديمة.

```python
a = [1, 2, 3]
b = list(a)

print(b)
a.append(4)
print(b)
```

طريقة أخرى لإنشاء المصفوفات
(خاصة المصفوفات الأكثر تعقيدًا) هي إنشاء مصفوفة فارغة أولاً ،
ثم ملؤها باستخدام الدالة (function) `append`.
على سبيل المثال ، إذا كنت تريد مصفوفة (list) بأرقام هي
قوى العدد اثنين ، مرر الأرقام إلى حلقة `for` ، و
لكل رقم ، أضف القوة المناسبة إلى المصفوفة:

```python
power_of_two = []
for number in range (10):
    power_of_two.append (2 ** number)
print(power_of_two)
```

إذا كنت تريد مصفوفة (list) تمثل مجموعة من البطاقات ،
استدعِ `append` لجميع تركيبات اللون والقيمة.

```python
deck = []
for color in '♠', '♥', '♦', '♣': # (Use text names on Windows) # (استخدم الأسماء النصية على ويندوز)
    for value in list(range(2, 11)) + ['J', 'Q', 'K', 'A']:
        deck.append(str(value) + color)
print(deck)
```

## المصفوفات والنصوص (Lists and Strings)

المصفوفات والنصوص (strings) هما نوعان من "التسلسلات" ،
لذلك ليس من المستغرب أنه يمكن تحويلهما
من نوع إلى آخر.
تنشئ الدالة (function) `list` مصفوفة (list) من الأحرف (characters) من نص (string).
إذا أردنا الحصول على مصفوفة (list) من الكلمات ، فإننا نستخدم طريقة `split` على جملة:

```python
words = 'This sentence is complex, split it into words!'.split()
print(words)
```

يمكن أن تأخذ طريقة `split` قيمة (argument) أيضًا.
إذا مررنا لها حرف فاصل (separator character) ، فسيتم "قطع" النص
عند هذا الفاصل المحدد ، بدلاً من المسافات (والأسطر الجديدة).
لذلك ، عندما يكون لدينا بعض البيانات مفصولة بفواصل ،
لا يوجد أسهل من استخدام `split` مع قيمة فاصلة:

```python
records  =  '3A, 8B, 2E, 9D' . split ( ',' )
print ( records )
```


إذا أردنا دمج مصفوفة (list) من النصوص (strings) في
نص (string) واحد ، فإننا نستخدم طريقة (method) `join`.
لاحظ أن هذه الطريقة (method) يتم استدعاؤها على حرف *الفاصل* (delimiter character) الذي نريد استخدامه
بين عناصر المصفوفة (list elements) ، وكـ وسيط (argument) ، فإنها تأخذ المصفوفة (list).

```python
sentence = ' '.join(words)
print(sentence)
```

## مهمة (Task)

تخيل أن المستخدمين (users) يدخلون أسماءهم وألقابهم ، وتقوم بتخزينها في
مصفوفة (list) للاستخدام المستقبلي ، على سبيل المثال ، سجلات الطلاب (student records).
ليس كل المستخدمين (users) حريصين عند إدخال أسمائهم ،
لذلك يمكن أن تظهر الأسماء بأحرف كبيرة (capitalized letters) بشكل غير صحيح.
على سبيل المثال:

```python
records = ['john doe', 'John Smith', 'Stuart little', 'petr File']
```

مهمتك هي:

* اكتب دالة (function) تحدد فقط الإدخالات التي تم إدخالها بشكل صحيح حيث
الحروف الأولى من الاسم الأول واسم العائلة مكتوبة بأحرف كبيرة.
* اكتب دالة (function) تحدد فقط السجلات التي تم إدخالها بشكل غير صحيح.
* *(اختياري (Optional))* - اكتب دالة (function) تُرجع مصفوفة (list) بسجلات مصححة.

يجب أن تبدو النتيجة هكذا:

```python
records = ['john doe', 'John Smith', 'Stuart little', 'petr File']

error_entries = select_errors(records)
print(error_entries) # → ['john doe', 'Stuart little', 'petr File']

ok_entries = select_correct(records)
print(ok_entries) # → ['John Smith']

corected_entries = correct_entries(records)
print(corected_entries) # → ['John Doe', 'John Smith', 'Stuart Little', 'Petr File']
```

> [note]
> طريقة سهلة لمعرفة ما إذا كان النص (string) مكتوبًا بأحرف صغيرة (lower case) ،
> هي طريقة (method) `()islower`، التي تُرجع True إذا كان النص (string) يحتوي فقط على أحرف صغيرة (lower)
> ، وإلا فإنها تُرجع False. على سبيل المثال ، `'abc'.islower() == True` ولكن
> `'aBc'.islower() == False`.
>
> أسهل طريقة لتحويل الحروف الأولى إلى أحرف كبيرة هي `capitalize()`:
> `'abc'.capitalize() == 'Abc'`

{% filter solution%}
```python
def select_errors(listA):
    result = []
    for record in listA:
        name_surname = record.split(' ')
        name = name_surname[0]
        surname = name_surname[1]
        if name[0].islower() or surname[0].islower():
            result.append(record)
    return result

def select_correct(listA):
    result = []
    for record in listA:
        name_surname = record.split(' ')
        name = name_surname[0]
        surname = name_surname[1]
        if not name[0].islower() and not surname[0].islower():
            result.append(record)
    return result

def correct_entries(listA):
    result = []
    for record in listA:
        name_surname = record.split(' ')
        name = name_surname[0]
        surname = name_surname[1]
        result.append(name.capitalize() + ' ' + surname.capitalize())
    return result
```
{% endfilter%}

## المصفوفات و (random)

تحتوي وحدة (module) `random` على دالتين (functions) يمكن استخدامهما مع المصفوفات (lists).

أولاً ، تقوم الدالة (function) `shuffle` بخلط العناصر - يتم ترك جميع العناصر بترتيب عشوائي (random order).
تمامًا مثل `sort` ، لا تُرجع `shuffle` أي شيء.

```python
import random

deck = []
for color in '♠', '♥', '♦', '♣':
    for value in list(range(2, 11)) + ['J', 'Q', 'K', 'A']:
        deck.append(str(value) + color)
print(deck)

random.shuffle(deck)
print(deck)
```

الثانية هي الدالة (function) `choice` التي تختار عنصرًا عشوائيًا (random element) من المصفوفة (list).
باستخدام مصفوفة (list) ، من الأسهل بكثير تنفيذ لعبة حجر/ورقة/مقص:

```python
import random
possibilities = ['rock', 'scissors', 'paper']
pc_choice = random.choice(possibilities)
```

## المصفوفات المتداخلة (Nested lists)

في بداية هذا الدرس قلنا أن المصفوفة (list)
يمكن أن تحتوي على أي نوع من القيم.
يمكن أن تحتوي المصفوفة (list) حتى على مصفوفات (lists) أخرى:

```python
list_of_lists = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
```

تتصرف هذه المصفوفة (list) كما هو متوقع - يمكننا اختيار
عناصر (elements) (وهي بالطبع مصفوفات (lists)):

```python
first_list = list_of_lists[0]
print(first_list)
```

وبما أن العناصر (elements) هي نفسها مصفوفات (lists) ،
يمكننا التحدث عن عناصر مثل "العنصر الأول من المصفوفة الثانية":

```python
second_list = list_of_lists[1]
first_element_of_second_list = second_list[0]
print(first_element_of_second_list)
```

ولأن `list_of_lists[1]`
يشير إلى المصفوفة (list) ، يمكننا أخذ العناصر (elements) مباشرة منها:

```python
first_element_of_second_list = (list_of_lists[1])[0]
```

أو:

```python
first_element_of_second_list = list_of_lists[1][0]
```

هذا النهج مفيد للغاية.
نفس حلقات `for` المتداخلة (nested `for` loops)
سمحت لنا بإدراج جدول ، المصفوفات المتداخلة (nested lists)
تسمح لنا بتخزين جدول.

```python
def create_tab(size=11):
    row_list = []
    for a in range(size):
        row = []
        for b in range(size):
            row.append(a * b)
        row_list.append(row)
    return row_list

multiplication_tab = create_tab()

print(multiplication_tab[2][3]) # two times three
print(multiplication_tab[5][2]) # five times two
print(multiplication_tab[8][7]) # eight times seven

# List the entire table
# سرد الجدول بأكمله
for row in multiplication_tab:
    for number in row:
        print(number, end = '')
    print()
```

ماذا يمكننا أن نفعل بمثل هذا الجدول المخزن؟ على سبيل المثال،
يمكنك حفظ مواضع القطع على لوحة الشطرنج ،
أو علامات الإكس والدوائر في لعبة إكس أو *ثنائية الأبعاد* (2D).
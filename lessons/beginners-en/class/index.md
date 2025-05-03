# الكائنات والقيم (Objects and values)

قبل أن نبدأ مع الفئات (classes)، سنتعلم عن الكائنات (objects).

ماذا يعني *كائن* (object) للمبرمجين؟

الأمر سهل بالفعل مع بايثون - كل قيمة (value) (هذا شيء يمكنك "تخزينه"
في متغير (variable)) هو كائن (object).
بعض لغات البرمجة (programming languages) (مثل JavaScript و C++‎ و Java) لديها أيضًا
قيم (values) أخرى غير الكائنات (objects). وعلى سبيل المثال، لغة C ليس لديها كائنات (objects) على الإطلاق.
ولكن في بايثون لا يوجد فرق بين القيمة (value) والكائن (object)، لذا
من الصعب بعض الشيء فهم ذلك. من ناحية أخرى، ليس عليك
معرفة التفاصيل.

السمة الأساسية للكائنات (objects) هي أنها تحتوي على بيانات (data) (معلومات) و *سلوك* (behaviour) -
تعليمات و/أو طرق (methods) لكيفية التعامل مع البيانات.
على سبيل المثال، تحتوي النصوص (strings) على معلومات (تسلسل من الأحرف) بالإضافة إلى
طرق (methods) مفيدة مثل `upper` و `count`.
إذا لم تكن النصوص (strings) كائنات (objects)، لكان على لغة بايثون أن تحتوي على الكثير
من الدوال (functions)، مثل `str_upper` و `str_count`.
تربط الكائنات (objects) البيانات والوظائف معًا.


> [note]
> ربما تقول أن، على سبيل المثال، `len` هي دالة (function)، وستكون على حق.
> بايثون ليست لغة موجهة للكائنات (object oriented language) بنسبة 100٪.
> لكن الدالة (function) `len` تعمل أيضًا على كائنات (objects) ليس لها أي شيء مشترك مع النصوص (strings).


#  الفئات (Classes)

تكون بيانات (data) كل كائن (object) محددة لكل كائن (object) ملموس
(على سبيل المثال، `"abc"` يحتوي على أحرف مختلفة عن `"def"`)،
ولكن الوظائف - الطرق (methods) - هي نفسها لجميع الكائنات (objects) من نفس
النوع (type) (الفئة (class)). على سبيل المثال، يمكن كتابة طريقة نصية (string method) `()count `
هكذا:


```python
def count(string, character):
    sum = 0
    for c in string:
        if c == character:
            sum = sum + 1
    return sum
```

وعلى الرغم من أن نصًا (string) مختلفًا سيُرجع قيمة مختلفة،
فإن الطريقة (method) نفسها هي نفسها لجميع النصوص (strings).

يتم تعريف هذا السلوك المشترك بواسطة *نوع* (type) أو *فئة* (class) الكائن (object).


> [note]
> في الإصدارات السابقة من بايثون كان هناك فرق بين "النوع" (type)
> و "الفئة" (class)، لكنهما الآن مترادفان.

يمكنك معرفة نوع (type) كائن (object) باستخدام الدالة (function) `type`:


```pycon
>>> type(0)
<class 'int'>
>>> type(True)
<class 'bool'>
>>> type("abc")
<class 'str'>
>>> with open('file.txt') as f:
...     type(f)
...
<class '_io.TextIOWrapper'>
```

تُرجع الدالة (function) `type` بعض الفئات (classes).
ما هي الفئة (class)؟ إنها وصف لكيفية تصرف كل كائن (object) من نفس النوع (type).

معظم الفئات (classes) في بايثون قابلة للاستدعاء كما لو كانت دوال (functions).
سيقوم هذا الكود التالي بإنشاء كائن (object) من الفئة (class) الذي استدعيناه:

```pycon
>>> string_class = type("abc")
>>> string_class(8)
'8'
>>> string_class([1, 2, 3])
'[1, 2, 3]'
```

إذن، إنه يتصرف مثل الدالة (function) `str`! أليس هذا غريبًا؟

الآن يجب أن نعتذر:
[للدوال](../functions/)
كذبنا قليلاً. الدوال (functions) `str` و `int` و `float` وما إلى ذلك، هي في الواقع فئات (classes).

```pycon
>>> str
<class 'str'>
>>> type('abcdefgh')
<class 'str'>
>>> type('abcdefgh') == str
True
```

لكن يمكننا استدعائها كما لو كانت دوال (functions).
لذا لا تحتوي الفئات (classes) فقط على "وصف" لكيفية تصرف كائن (object) من الفئة (class)،
ولكن يمكنها أيضًا إنشاء كائنات (objects).


## فئات مخصصة (Custom classes)

الآن سنحاول إنشاء فئتنا (class) الخاصة.

يكون كتابة فئات مخصصة (custom classes) مفيدًا عندما تريد استخدام كائنات (objects) مختلفة
بسلوك مماثل في برنامجك.
على سبيل المثال، يمكن أن تحتوي لعبة بطاقات على فئة Card، ويمكن أن يحتوي تطبيق ويب
على فئة User، ويمكن أن يحتوي تطبيق جداول بيانات على فئة Row.

دعنا نكتب برنامجًا يتعامل مع الحيوانات.
أولاً، تقوم بإنشاء فئة Kittie يمكنه المواء:


```python
class Kittie:
    def meow(self):
        print("Meow!")
```

تمامًا كما يتم تعريف الدالة (function) بواسطة الكلمة المفتاحية `def`، يتم تعريف الفئات (classes)
بواسطة الكلمة المفتاحية `class`. ثم بالطبع عليك المتابعة بنقطتين رأسيتين
وإزاحة جسم الفئة (class body).
بشكل مشابه لكيفية إنشاء `def` لدالة (function)، تنشئ `class` فئتاً (class) وتعينها إلى
اسم الفئة (في مثالنا إلى `Kittie`).

من المتعارف عليه تسمية الفئات (classes) بحرف كبير أول حتى لا
يتم الخلط بينها وبين المتغيرات "العادية" بسهولة.


> [note]
> الفئات الأساسية (`str` و `int` وما إلى ذلك)
> لا تبدأ بحرف كبير بسبب تاريخي
> أسباب - في الأصل كانت دوال (functions) حقًا.

في جسم الفئة (class body)، تقوم بتعريف طرق (methods)، والتي تبدو مثل الدوال (functions).
الفرق هو أن طرق الفئة (class methods) لديها `self` كـ وسيط (argument) أول،
والذي سنشرحه لاحقًا - المواء يأتي أولاً:

```python
# Creation of the object
# إنشاء الكائن
kittie = Kittie()

# Calling the method
# استدعاء الطريقة
kittie.meow()
```

في هذه الحالة، عليك أن تكون حذرًا جدًا بشأن الأحرف الكبيرة:
`Kittie` (بحرف K كبير) هو الفئة (class) - وصف لكيفية تصرف القطط الصغيرة.
`kittie` (بحرف k صغير) هو الكائن (object) (مثيل - *instance*) من فئة Kittie:
متغير (variable) يمثل قطة صغيرة.
يتم إنشاء هذا الكائن (object) عن طريق استدعاء الفئة (class) (تمامًا كما
يمكننا إنشاء نص (string) عن طريق استدعاء `()str`).

مواء!

## الخصائص (Attributes)

الكائنات (objects) التي يتم إنشاؤها من فئات مخصصة (custom classes) لديها ميزة واحدة
لا تسمح بها فئات مثل `str`: القدرة على تعريف *خصائص* (attributes) الفئة -
معلومات يتم تخزينها بواسطة مثيل (instance) الفئة (class).
يمكنك التعرف على الخصائص (attributes) بواسطة النقطة بين مثيل الفئة (class instance) واسم خاصيته.


```python
smokey = Kittie()
smokey.name = 'Smokey'

misty = Kittie()
misty.name = 'Misty'

print(smokey.name)
print(misty.name)
```

في البداية قلنا أن الكائنات (objects) تربط السلوك بالبيانات.
يتم تعريف السلوك في الفئة (class)، ويتم تخزين البيانات في الخصائص (attributes).
يمكننا التمييز بين القطط الصغيرة، على سبيل المثال، بأسمائها بسبب الخصائص (attributes).

> [note]
> باستخدام نقطة بعد كائن (object) الفئة (class)، يمكنك الوصول إلى طرق (methods) الفئة
> وكذلك خصائصه (attributes).
> ماذا يحدث إذا كان لخاصية (attribute) نفس اسم طريقة (method)؟
> جربها!
>
> ```python
> misty = Kittie()
> misty.meow = 12345
> misty.meow()
> ```

## المعامل self  (Parameter self)

الآن سنعود بإيجاز إلى الطرق (methods)، وبشكل خاص، سنعود
إلى المعامل (parameter) `self`.

لكل طريقة (method) حق الوصول إلى أي كائن (object) محدد تعمل عليه فقط بسبب
المعامل (parameter) `self`.
الآن بعد أن سميت قططك الصغيرة، يمكنك استخدام المعامل (parameter) `self` لإضافة الاسم إلى المواء.


```python
class Kittie:
    def meow(self):
        print("{}: Meow!".format(self.name))

smokey = Kittie()
smokey.name = 'Smokey'

misty = Kittie()
misty.name = 'Misty'

smokey.meow()
misty.meow()
```

ماذا حدث للتو؟ الأمر `smokey.meow` استدعى *طريقة* (method) تقوم عند استدعائها بتعيين الكائن (object)
`smokey` كـ وسيط (argument) أول للدالة (function) `meow`.

> [note]
> هكذا تختلف *الطريقة* (method) عن *الدالة* (function):
> تتذكر الطريقة (method) الكائن (object) الذي تعمل عليه.

وذلك الوسيط (argument) الأول الذي يحتوي على كائن (object) محدد من الفئة (class) الذي تم إنشاؤه للتو يسمى
عادةً `self`.
يمكنك بالطبع تسميته بشكل مختلف، لكن المبرمجين الآخرين لن يحبوك. :)

هل يمكن لمثل هذه الطريقة (method) أن تأخذ أكثر من وسيط (argument) واحد؟
يمكنها ذلك - في هذه الحالة، سيتم استبدال `self` كـ وسيط (argument) أول،
وسيتم أخذ بقية الوسائط (arguments) من كيفية استدعائك للطريقة (method).
على سبيل المثال:

```python
class Kittie:
    def meow(self):
        print("{}: Meow!".format(self.name))

    def eat(self, food):
        print("{}: Meow meow! I like {} very much!".format(self.name, food))

smokey = Kittie()
smokey.name = 'Smokey'
smokey.eat('fish')
```

## الطريقة `__init__` (Method `__init__`)

هناك مكان آخر يمكنك فيه تمرير وسائط (arguments) إلى الفئة (class):
عندما تقوم بإنشاء كائن (object) جديد (استدعاء الفئة).
يمكنك بسهولة حل المشكلة التي قد تراها في الكود السابق:
بعد إنشاء كائن (object) القطة الصغيرة، يجب عليك إضافة اسم حتى تتمكن الطريقة (method)
`meow` من العمل.

يمكنك أيضًا إنشاء فئات (classes) عن طريق تمرير معاملات (parameters) عند استدعائها:

```python
smokey = Kittie(name='Smokey')
```
تستخدم بايثون الطريقة `__init__` (تسطيران سفليان، `init`، تسطيران سفليان) لهذا الخيار.
تشير هذه التسطيرات إلى أن اسم هذه الطريقة (method name) مميز بطريقة ما. الطريقة `__init__`
يتم استدعاؤها بالفعل مباشرة عند إنشاء الكائن (object)، أو بعبارة أخرى - عند
تتم تهيئته (`init` تعني *التهيئة* - initialization).
لذا يمكنك كتابتها هكذا:

```python
class Kittie:
    def __init__(self, name):
        self.name = name

    def meow(self):
        print("{}: Meow!".format(self.name))

    def eat(self, food):
        print("{}: Meow meow! I like {} very much!".format(self.name, food))

smokey = Kittie('Smokey')
smokey.meow()
```

والآن لا توجد إمكانية لإنشاء قطة صغيرة بدون اسم،
وستعمل `meow` طوال الوقت.

هناك العديد من الطرق (methods) الأخرى التي تحتوي على تسطيرات سفلية، على سبيل المثال، `__str__`
يتم استدعاء الطريقة (method) عندما تحتاج إلى تحويل الكائن (object) إلى نص (string):

```python
class Kittie:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return '<Kittie named {}>'.format(self.name)

    def meow(self):
        print("{}: Meow!".format(self.name))

    def eat(self, food):
        print("{}: Meow meow! I like {} very much!".format(self.name, food))

smokey = Kittie('Smokey')
print(smokey)
```

## تمرين: قطة (Exercise: Cat)

الآن بعد أن عرفت كيفية إنشاء فئة القطة الصغيرة، حاول إنشاء فئة للقطط.

* يمكن للقطة أن تموء باستخدام الطريقة `meow`.
* لدى القطة 9 أرواح عند إنشائها (لا يمكن أن يكون لديها أكثر من 9 وأقل من 0 أرواح).
* يمكن للقطة أن تقول ما إذا كانت على قيد الحياة (لديها أكثر من 0 أرواح) باستخدام الطريقة `alive`.
* يمكن للقطة أن تفقد أرواحًا (الطريقة `takeoff_life`).
* يمكن إطعام القطة باستخدام الطريقة `eat` التي تأخذ وسيطًا واحدًا بالضبط - طعامًا محددًا (نص).
    إذا كان الطعام `fish`، فستكتسب القطة روحًا واحدة (إذا لم تكن ميتة بالفعل أو
    ليس لديها الحد الأقصى من الأرواح).

{% filter solution %}
```python
class Cat:
    def __init__(self):         # Init function does not have to take number of lives
        self.lives_number = 9   # as parameter 'cause that number is always the same.

    def meow(self):
        print("Meow, meow, meeeoooow!")

    def alive(self):
        return self.lives_number > 0

    def takeoff_life(self):
        if not self.alive():
            print("You can't kill a cat that is already dead, you monster!")
        else:
            self.lives_number -= 1

    def eat(self, food):
        if not self.alive():
            print("It's pointless to give food to dead cat!")
            return
        if food == "fish" and self.lives_number < 9:
            self.lives_number += 1
            print("The cat ate a fish and gained 1 life!")
        else:
            print("The cat is eating.")
```
{% endfilter %}

وهذا كل شيء عن الفئات (classes) الآن.
[في المرة القادمة](../inheritance/) سنتعلم عن الوراثة (inheritance).
وعن الكلاب الصغيرة أيضًا. :)
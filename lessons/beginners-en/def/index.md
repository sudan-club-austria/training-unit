
 # الدوال (functions)

في أحد [الدروس]({{ lesson_url('beginners-en/functions') }}) السابقة
كنا نعمل مع دوال كتبها شخص آخر - كانت
مضمنة بالفعل في Python - `print` أو قمنا باستيرادها من وحدة - `turtle` على سبيل المثال.

```python
from math import pi

print(pi)
```

اليوم سوف نتعلم كيفية برمجة دوال خاصة بنا
وهو ما سيكون مفيدًا عندما نحتاج إلى تشغيل المهام بشكل متكرر.

الأمر ليس صعبًا:


```python
def find_perimeter(width, height):
    "Returns the rectangle's perimeter of the given sides"
    return  2 * (width  +  height)

print (find_perimeter(4 ,  2))

```

## كيف يمكن فعل ذلك؟

*تعرف* الدالة باستخدام الأمر `def`. مباشرة بعد ذلك
يجب عليك كتابة اسم الدالة ، والأقواس (التي قد تحتوي على
*قيم (arguments)*) ثم ، بالطبع ، *فاصلة منقوطة*.


لقد قلنا بالفعل أنه بعد الفاصلة المنقوطة ، كل شيء
ينتمي إلى الدالة (في حالتنا) يجب ان يفصل بالمساحات (indented) .
يُطلق على الكود المفصول بالمساحات  *جسم الدالة* ويحتوي على
الأوامر التي تؤديها الدالة.
يمكن أن يبدأ الجسم بـ *تعليق توثيق* أو ما يسمى *docstring* والذي يصف ما
تفعله الوظيفة.

يمكن للدالة إرجاع قيمة باستخدام الأمر `return`. المزيد عن ذلك لاحقا.

```python
def print_score(name, score):
    print(name, 'score is', score)
    if score > 1000:
        print('World record!')
    elif score > 100:
        print('Perfect!')
    elif score > 10:
        print('Passable.')
    elif score > 1:
        print('At least something. ')
    else:
        print('Maybe next time. ')

print_score('Your', 256)
print_score('Denis', 5)
```

عندما تستدعي دالة ، يتم تعيين القيم التي تكتبها بين قوسين
إلى المتغيرات المقابلة في أقواس تعريف الدالة.

لذلك عندما تستدعي دالتنا الجديدة مع `print_score('Your', 256)` ،
تخيل أنه ، داخليًا ، يعين القيم مثل هذا:


```python
name = 'Your'
score = 256

print(name, 'score is', score)
if score > 1000:
    ... #etc.

```
## الإرجاع (Return)

يُنهي أمر `return` الدالة على الفور ويرجع القيمة المحسوبة
خارج الدالة. يمكنك استخدام هذا الأمر فقط في الدوال!

يتصرف بشكل مشابه للأمر `break` الذي ينهي الحلقات.

```python
def yes_or_no(question):
    "Returns True or False, depending on the user's answers."
    while True:
        answer = input(question)
        if answer == 'yes':
            return True
        elif answer == 'no':
            return False
        else:
            print('What do you want!! Just  type "Yes" or "No".')

if yes_or_no('Do you want to play a game?'):
    print('OK, but you have to program it first.')
else:
    print('That is sad.' )

```

> [note]
> مثل `if` و `break` ، `return` هو أمر Python *، وليس دالة*.
> لهذا السبب لا يوجد `return` أقواس بعده.

حاول كتابة دالة ترجع مساحة الشكل البيضاوي بأبعاد معينة.
الصيغة هي <var>A</var> = π<var>a</var><var>b</var> ،
حيث <var>a</var> و <var>b</var> هما أطوال المحاور.
ثم قم باستدعاء الدالة وطباعة النتيجة.

{% filter solution %}
```python
from math import pi

def ellipse(a, b):
    return pi * a * b

print('The ellipsis area with 3 cm and 5 cm axes length is', ellipse(3, 5),'cm2.')

```
{% endfilter %}


### الإرجاع أو الطباعة؟ (Return or print?)

يمكن أيضًا كتابة البرنامج الأخير مثل هذا:

```python
from math import pi

def ellipse(a, b):
    print('The area is', pi * a * b) # Caution, 'print' instead of 'return'!

ellipse(3, 5)

```

يعمل البرنامج بهذه الطريقة أيضًا. لكنه يخسر إحدى المزايا الرئيسية
التي تتمتع بها الدوال - عندما تريد استخدام القيمة بشكل مختلف عن `print` لها.

الدالة التي *تعيد* نتيجتها يمكن استخدامها كجزء من حسابات أخرى:


```python
def elliptical_cylinder(a, b, height):
    return ellipse(a, b) * height

print(elliptical_cylinder(3, 5, 3))
```


ولكن إذا كانت دالة الشكل البيضاوي لدينا *تطبع* النتيجة فقط ، فلن نتمكن بذلك
 من حساب مساحة الاسطوانة البيضاوية.

السبب في أن `return` أفضل من `print` هو أنه يمكن إعادة استخدام الدالة
في العديد من المواقف المختلفة. عندما لا نريد في الواقع
معرفة النتائج الوسيطة ، لا يمكننا استخدام الدوال مع `print`.

يشبه ذلك الإدخال: إذا قمت بكتابة `input` الثابت في دالة ، يمكنني استخدامه
فقط في المواقف التي يوجد فيها مستخدم مع لوحة مفاتيح موجودة.
لهذا السبب من الأفضل دائمًا تمرير القيم إلى دالة ، واستدعاء
`input` خارج الدالة:

```python
from  math import pi

def ellipse(a, b):
    """This reusable function returns only the result - the ellipse's area with a and b axes"""
    #This is only the calculation
    return pi * a * b

#print and input are "outside" the reusable function!
x = float(input('Enter length of 1st axis: '))
y = float(input('Enter length of 2nd axis: '))
print('The ellipsis area is', ellipse(x, y),'cm2.')
```

`input` خارج الدالة:

بالطبع هناك استثناءات: يمكن كتابة دالة تولد مباشرةً
نصًا باستخدام `print` ، أو دالة تعالج معلومات النص.
ولكن عندما تحسب الدالة شيئًا ما ، فمن الأفضل عدم وجود
`print` و `input` بداخلها.


## لا شيء (None)

عندما لا ينتهي تشغيل الدالة بـ `return` صريح ،
القيمة التي تعيدها هي تلقائيًا `None`.

`None` هي قيمة موجودة بالفعل "داخل" Python (مثل `True` و `False`).
إنها حرفيًا "لا شيء ، لا شيء".

```python
def nothing():
    "This function isn't doing anything."

result = nothing()
print(result) # returns None
print(result is None) # returns True
```

## المتغيرات المحلية (Local variables)

تهانينا! يمكنك الآن تعريف دالتك الخاصة!
الآن يجب أن نشرح ما هي المتغيرات المحلية(local) والعالمية(global).

يمكن للدالة استخدام متغيرات من "الخارج":

```python
pi = 3.1415926  # a variable defined outside the function

def circle_area(radius):
    return pi * radius ** 2

print(circle_area(100))
```

ولكن كل متغير(variable) و قيمة(argument) يتم تعريفها في جسم الدالة هي
*جديدة تمامًا* ولا تشارك أي شيء مع المتغيرات "الخارجية".

المتغيرات التي يتم تعريفها داخل جسم الدالة تسمى *المتغيرات المحلية* ،
لأنها تعمل فقط محليًا داخل الدالة.

على سبيل المثال ، لن يعمل ما يلي كما تتوقع:

```python
x = 0  # Assign value to global variable x

def set_x(value):
    x = value  # Assign value to local variable x

set_x(40)
print(x)
```

إذا قامت دالة بتعريف متغير محلي بنفس الاسم ، فسيكون لهذا المتغير المحلي فقط
قيمة داخل الدالة.

لنلقي نظرة على مثال.
قبل تشغيل البرنامج التالي ، حاول تخمين كيف سيتصرف.
ثم قم بتشغيله ، وإذا فعل شيئًا مختلفًا عن
ما كنت تتوقعه ، حاول أن تشرح السبب.
هناك خدعة! :)

```python
from math import pi
area = 0
a = 30

def ellipse_area(a, b):
    area = pi * a * b  # Assign value to 'area`
    a = a + 3  # Assign value to 'a`
    return area

print(ellipse_area(a, 20))
print(area)
print(a)
```


الآن حاول الإجابة على الأسئلة التالية:

* هل المتغير `pi` محلي أم عالمي؟
* هل المتغير `area` محلي أم عالمي؟
* هل المتغير `a` محلي أم عالمي؟
* هل المتغير `b` محلي أم عالمي؟


{% filter solution %}
* `pi` عالمي - لم يتم تعريفه داخل الدالة وهو
متاح في البرنامج بأكمله.
* `area` - لاحظ أن هناك متغيرين بهذا الاسم! واحد عالمي
والآخر محلي داخل الدالة `ellipse_area`.
* `a` - لاحظ أيضًا وجود متغيرين بهذا الاسم. هذا هو المقصود بالخدعة:
كتابة `a = a + 3` ليس لها معنى. يتم تعيين قيمة للمتغير المحلي
`a` ، ولكن تنتهي الدالة مباشرة بعد ذلك ، والمتغير `a` لن يكون
متاحًا بعد ذلك ، و لهذا لن يتم استخدامه أبدًا.
* `b` محلي فقط - إنه قيمة(argument) لدالة `ellipse_area`.

{% endfilter %}

إذا قمت بتعريف دالة بعدد معين من *القيم* ، فإن استدعاء
الدالة تحتاج إلى تمرير جميع هذه القيم أيضًا. سيحدث ما يلي إذا تم تمرير القليل جدًا
من القيم.

```python
def say_name_5(first_name, last_name):
    for i in range(5):
        print(first_name.upper() + " " + last_name.upper())

say_name_5("Eva", "Blasco")

say_name_5("Eva")
# TypeError: say_name_5() missing 1 required positional argument: 'last_name'
```



ولكن في هذه الحالة ، يجب ألا نضطر إلى إدخال كل من الاسم الأول واسم العائلة.
هناك أشخاص معروفون بدون اسم عائلة ، في هذه الحالة لن نتمكن من استخدام
الدالة الا بحل بديل - مثل تعيين اسم العائلة إلى نص فارغ `""`.

### الافتراضيات (Defaults)

من الممكن (على الرغم من أنه لا معنى له دائمًا) إضافة قيم *افتراضية* للقيم
التي سيتم استخدامها إذا لم يحدد استدعاء الدالة هذه القيم.

لتحديد القيمة الافتراضية ، نستخدم بناء الجملة `argument=value` في تعريف الدالة:

```python
def say_name_5(first_name="", last_name=""):
    if (first_name != "" or last_name != ""):
        for i in range(5):
            print(first_name.upper() + " " + last_name.upper())
    else:
        print("Warning: Use this function with at least a first name")

say_name_5("Eva")
say_name_5()

```

تظهر مشكلة أيضًا في حالة استدعائنا لدالة و استخدام قيم اكثر مماتسمح به الدالة:

```python
say_name_5("Eva", "Blasco", "of Royal Court!")

# TypeError: say_name_5() takes 2 positional arguments but 3 were given
```

## التكرار (Recursion)

*التكرار* هو تقنية برمجة ،
عندما تستدعي دالة نفسها.

مثل هذا التكرار سينتهي في مكالمة لا نهائية.
عندما تدخل هذا البرنامج:

```python
def recursive_function():
     result = 1+2
     recursive_function()
     return result

recursive_function()
```

كيف يعمل؟

* يعرف Python دالة `recursive_function`
* يستدعي الدالة `recursive_function`:
   * يحسب النتيجة
   * يستدعي الدالة `recursive_function`:
     * يحسب النتيجة
     * يستدعي الدالة `recursive_function`:
       * يحسب النتيجة
       * يستدعي الدالة `recursive_function`:
         * يحسب النتيجة
       * يستدعي الدالة `recursive_function`:
           * ...
             * ...
                * بعد مئات من التكرارات ، يلاحظ Python أن هذا
                  يؤدي إلى لا شيء ، وينتهي بخطأ.

تتوافق رسالة الخطأ مع هذا:

```
Traceback (most recent call last):
   File "/tmp/test.py", line 4, in <module>
     recursive_function()
   File "/tmp/test.py", line 2, in recursive_function
     return recursive_function()
   File "/tmp/test.py", line 2, in recursive_function
     return recursive_function()
   File "/tmp/test.py", line 2, in recursive_function
     return recursive_function()
   [Previous line repeated 996 more times]
RecursionError: maximum recursion depth exceeded
```

## التداخل المتحكم فيه (Controlled nesting)

كيف تستخدم التكرار عمليا؟

يمكن فهم ذلك باستخدام مثال "الغوص".

تخيل غواصًا يستكشف أعماق البحر بالطريقة التالية:

* كيف يتم "استكشاف البحر" عند عمق معين:
   * أنظر حولي
   * إذا كنت بالفعل في عمق كبير جدًا ، فأنا خائف. لن أستكشف المزيد.
   * غير ذلك:
     * أغوص 10 م أقل
     * *سأستكشف البحر* على عمق جديد
     * أغوص مرة أخرى في 10 م

أو في Python:

```python
def explore(depth):
     print(f'Looking around at a depth of {depth} m')
     if depth >= 30:
         print('Enough! I have seen it all!')
     else:
         print(f'I dive more (from {depth} m)')
         explore(depth + 10)
         print(f'Surfacing (at {depth} m)')

explore(0)
```

```
* يحدد بايثون الدالة "explore"
* يستدعي الدالة "explore" بعمق 0:
* يطبع "I'm looking around at a depth of 0 m"
* يتحقق من أن "0 ≥ 30" (وهو ليس صحيحًا)
* يطبع "I dive more (from 0 m)"
* يستدعي الدالة "explore" بعمق 10 أمتار:
* يكتب "I look around at a depth of 10 m"
* يتحقق من أن "10 ≥ 30" (وهو ليس صحيحًا)
* يكتب "I dive more (from 10 m)"
* يستدعي الدالة "explore" بعمق 20 مترًا:
* يتحقق من أن "20 ≥ 30" (وهو ليس صحيحًا)
* يكتب "I dive more (from 30 m)"
* يستدعي الدالة "explore" بعمق 20 مترًا:
* يتحقق من أن "20 ≥ 30" (وهو ليس صحيحًا)
* يكتب "I dive more (from 30 m)"
* يستدعي الدالة "explore" بعمق 20 مترًا:
* وظيفة `explore` بعمق 30 مترًا:
* تتحقق من أن `30 ≥ 30` (وهو صحيح! أخيرًا!)
* تطبع ``كفى! لقد رأيت كل شيء!''
* وتنتهي
* تطبع ``Surfacing (at 20 m)''
* تطبع ``Surfacing (at 10m)''
* تطبع ``Surfacing (at 0 m)''
```

## عاملي (Factorial)

الخوارزميات التكرارية مستوحاة في الاساس من الرياضيات. عاملي <var>x</var> ، أو
ناتج ضرب جميع الأعداد من 1 إلى <var>x</var> ، مكتوبًا كـ <var>x</var>! ،
يعرفه علماء الرياضيات على النحو التالي:

* 0! = 1
*  اذا كانت قيمة <var>x</var> موجبة : <div style=" direction: ltr"><var>!x</var>! = <var>x</var> · (<var>x</var> - 1) </div>
أو في Python:


```python
def factorial(x):
     if x == 0:
         return 1
     elif x > 0:
         return x * factorial(x - 1)

print(factorial(5))
print(1 * 2 * 3 * 4 * 5)
```

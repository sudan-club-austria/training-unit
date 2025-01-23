

إذا كنت ترغب في إجراء بعض الحسابات باستخدام الرقم π (pi) ، كيف ستكتبه؟
3.14159265 ؟

يحتوي Python على العديد من الخصائص المبنية مسبقا. لا تحتاج إلى إعادة العملية كل مرة ،
ما عليك سوى معرفة مكان البحث.

يمكننا الوصول إلى *π* عن طريق استيراد (import) مكتبة (module) `math`.


```python
from math import pi

print(pi)
```

كما ترى ، فإن π مخفي بعض الشيء. مقارنةً بـ `print` أو `if` ، والتي يحتاجها الجميع ،
لا يحتاج الجميع إلى `math`. دعونا نكتفي بهذه االمكتبة (module) لفترة أطول قليلاً.
## التعبيرات (Expressions)

في الرياضيات ، لدينا العديد من العمليات المختلفة التي يتم تنفيذها كرموز ، مثل + أو -. يتم استخدام نفس الرموز في Python.

* 3 + 4
* <var>a</var> - <var>b</var>

يصعب الأمر قليلاً مع الضرب والقسمة لأنه لا يمكنك كتابة تعبير رياضي معتاد
على لوحة المفاتيح الخاصة بك:

* 3 · 4
* ¾

اخترع علماء الرياضيات المزيد والمزيد من الرموز المعقدة
والتي لا يمكن بسهولة نسخها بواسطة المبرمجين:


* <var>x</var>²
* <var>x</var> ≤ <var>y</var>
* sin θ
* Γ(<var>x</var>)
* ∫<var>x</var>
* ⌊<var>x</var>⌋
* <var>a</var> ★ <var>b</var>
* <var>a</var> ⨁ <var>b</var>

هناك حتى لغات برمجة تحتاج إلى لوحة مفاتيح خاصة. لأن برامجهم لا يمكن كتابتها بسهولة
وهي غير قابلة للقراءة.

> [note]
> على سبيل المثال ، هذا برنامج مكتوب بلغة APL:
>
> >
>     ⍎’⎕’,∈Nρ⊂S←’←⎕←(3=T)∨M∧2=T←⊃+/(V⌽”⊂M),(V⊖”⊂M),(V,⌽V)⌽”(V,V←1¯1)⊖”⊂M’


هناك عدد قليل نسبيًا من المشغلات (operators) في Python.
وقد عرفنا بالفعل نصفهم تقريبًا!
بعض المشغلات عبارة عن كلمات.
إليك جميعها:

<div>
    <code>==</code> <code>!=</code>
    <code>&lt;</code> <code>&gt;</code>
    <code>&lt;=</code> <code>&gt;=</code>
    <code class="text-muted">|</code> <code class="text-muted">^</code>
    <code class="text-muted">&amp;</code>
    <code class="text-muted">&lt;&lt;</code> <code class="muted">&gt;&gt;</code>
    <code>+</code> <code>-</code>
    <code>*</code> <code class="text-muted">@</code> <code>/</code>
    <code>//</code> <code>%</code>
    <code class="text-muted">~</code>
    <code>**</code>
    <code class="text-muted">[ ]</code> <code class="text-muted">( )</code>
    <code class="text-muted">{ }</code>
    <code class="text-muted">.</code>
</div>

<div>
    <code class="muted">lambda</code>
    <code class="muted">if else</code>
    <code>or</code> <code>and</code> <code>not</code>
    <code class="muted">in</code> <code class="muted">not in</code>
    <code class="muted">is</code> <code class="muted">is not</code>
</div>

من الواضح الآن أن بعض العمليات التي نريد القيام بها في البرنامج
لا يمكن التعبير عنها بواسطة هذه المشغلات (operators).

كيف تتعامل مع هذا؟

إحدى الطرق التي ذكرناها بالفعل هي تعريف العملية بالكلمات.

* <var>x</var> = sin <var>a</var>

ويمكننا كتابة ذلك على لوحات المفاتيح الخاصة بنا!
علينا فقط إضافة أقواس (احيانا يقوم المحرر (editor) بذلك نيابة عنا) لجعلها
واضح لما تطبق العملية:

```python
x = sin(a)
```

ولكن أولاً وقبل كل شيء ، يجب عليك *استيراد (import)* `sin` ،
بنفس الطريقة التي استوردت بها `pi` بالفعل.
لذلك سيبدو البرنامج الكامل على النحو التالي:

```python
from math import sin

x = sin(1)  # (in radian)
print(x)
```

> [warning] استيراد الملفات و اسمائها (Import and files names)
>
> عندما نريد استيراد (import) المكتبات ، يتعين علينا الانتباه بشكل إضافي
> كيف نسمي ملفات البرنامج الخاصة بنا.
> إذا قمت باستيراد الوحدة `math` إلى برنامجك ، فلا يمكن أن يكون لملفك اسم `math.py` نفسه.
>
> لماذا؟ لأنه إذا كنت تستورد وحدة ، فسيبحث Python أولاً
> في المجلد الذي تقوم بتشغيل البرنامج منه.
> سيجد الملف `math.py` وسيحاول استيراد دالة `sin` من هناك.
> وبالطبع لن يجدها.


## استدعاء الدوال (Call functions)

نستدعي الدالة (function) حسب *اسمها*.

يبدو الاسم وكأنه متغير (variable) - في الواقع ، إنه *متغير (variable)* ، الفرق الوحيد هو أنه بدلاً من رقم أو سلسلة ،
لدينا دالة (function) مخزنة في الداخل.

بعد اسم الدالة (function) ، لدينا أقواس نضع فيها *الوسيطة*
(أو *الإدخال*) للدالة (function). هذه هي المعلومات التي ستعمل بها وظيفتنا.
في مثالنا ، ستقوم `()sin` بحساب <em>الجيب</em>

*القيمة المرجعة* للدالة (function) هي قيمة يمكن تعيينها إلى متغير.

```
        function name
                 │
                ╭┴╮
            x = sin(1)
            ▲      ╰┬╯
            │     argument
            │
            ╰── return value
```

يمكننا ايضا استخدامها في عملية حسابية:

```python
a = sin(1) + cos(2)
```

او من الممكن استخدامها كشرط تحت `if`:

```python
if sin(1) < 3:
```

او حتى استخدامها كقيمة داخل دالة (function) اخرى :

```python
print(sin(1))
```

و هكذا


### القيم (Arguments)

يمكننا تمرير عدة قيم (Arguments) إلى بعض الدوال. مثال على ذلك هي `print` ،
التي تطبع جميع القيم المدخلة اليها على التوالي. نفصل بين القيم بفاصلة:

```python
print(1, 2, 3)
```

```python
print("One plus two equals", 1 + 2)
```
بعض الدوال لا تحتاج إلى أي قيمة ، والدالة print هي مثال آخر على ذلك.
ولكن لا يزال يتعين علينا كتابة الأقواس ، حتى لو كانت فارغة. خمن ماذا ستفعل print بدون قيم؟

```python
print()
```

{% filter solution %}
ستقوم الدالة print بدون قيم بطباعة سطر فارغ.

يتبع ذلك التعريف تمامًا - ستكتب الدالة print كل
قيمها على سطر.
{% endfilter %}

عند استدعاء الدوال (Call functions)
كن حذرًا عند كتابة الأقواس ، وإلا فلن يتم استدعاء الدالة.
لن تحصل على قيمة الإرجاع ، ولكن الدالة نفسها! دعنا نجرب الأمثلة التالية:

```python
from math import sin
print(sin(1))
print(sin)
print(sin + 1)
```

### القيم المسماة مسبقا (Named arguments)

يمكن لبعض الوظائف أيضًا العمل مع القيم *المسماة مسبقا*.
يتم كتابتها بطريقة مشابهة لإسناد متغير ، باستخدام علامة مساواة ،
ولكن داخل الأقواس:

على سبيل المثال ، تنتهي وظيفة `print` بطباعة حرف سطر جديد في نهاية السطر بشكل افتراضي ،
ولكن يمكننا تغيير ذلك باستخدام القيمة المسماة `end` ، وطباعة شيء آخر.

> [note]
> يتعين علينا كتابة هذا في ملف .py لتشغيله لأننا لن نتمكن من ذلك
> لرؤيتها بشكل صحيح في لوحة التحكم التفاعلية.


```python
print('1 + 2', end=' ')
print('=', end=' ')
print(1 + 2, end='!')
print()
```

## دوال مفيدة (Useful functions)

أخيرًا ، سنلقي نظرة على بعض الدوال الأساسية المضمنة.
يمكنك أيضًا تنزيل ورقة الغش هذه
<a href="https://github.com/muzikovam/cheatsheets/blob/master/basic-functions/basic-functions-en.pdf">cheatsheet</a>.


### المدخلات والمخرجات (Input and output)

نحن نعرف هذه الدوال بالفعل.
تقوم `print` بكتابة القيم غير المسماة والمفصولة بمسافات في الإخراج.
سيقوم بكتابة قيمة مسماة `end` في نهاية السطر (الافتراضي (default) هو سطر جديد).
وقيمة مسماة أخرى `sep` تحدد ما سيتم كتابته بين كل قيمة (الافتراضي (default) هو مسافة).


> [note]
> نوصي بتشغيل المثال التالي
> من ملف ، وليس من وحدة تحكم Python.

```python
print(1, "two", False)
print(1, end=" ")
print(2, 3, 4, sep=", ")
```


**الدالة الأساسية للإدخال هي `input` بشكل واضح.**
ستقوم بطباعة السؤال (أو أي شيء تكتبه) ،
جمع الإدخال من المستخدم ، وإعادته
كـ نص (string).

```python
input('Enter input: ')
```

### تحويل النوع (Type casting)

في حالة عدم رغبتنا في العمل فقط مع النصوص ، فهناك مجموعة من
الدوال التي يمكنها تحويل النصوص إلى أرقام والعكس صحيح.
ولكن ماذا تفعل عندما لا تريد العمل مع نص ولكن ، على سبيل المثال ، مع رقم؟
هناك مجموعة من الدوال التي يمكن أن تساعدنا في تحويل النصوص إلى أرقام والعكس صحيح.
كل واحد من الأنواع الثلاثة *للمتغيرات* التي نعرفها حاليًا
لديه دالة تأخذ قيمة  وتعيدها كـ
قيمة من نوعها الخاص.
بالنسبة إلى *الأعداد الصحيحة* ، توجد الدالة `()int` ، وبالنسبة إلى *الأعداد العشرية* ، هناك
`float` ، وبالنسبة إلى *النصوص* ، هناك `()str`.


```python
int(x)              # conversion to integer
float(x)            # conversion to real number
str(x)              # conversion to string
```

امثلة:

```python
3 == int('3') == int(3.0) == int(3.141) == int(3)
8.12 == float('8.12') == float(8.12)
8.0 == float(8) == float('8') == float(8.0)
'3' == str(3) == str('3')
'3.141' == str(3.141) == str('3.141')
```
ولكن ليست كل التحويلات ممكنة:

```python
int('blablabla')    # error!
float('blablabla')  # error!
int('8.9')          # error!
```

سنخبرك بكيفية التعامل مع الأخطاء في وقت آخر.


### الدوال الرياضية (Mathematical functions)

الرياضيات مفيدة في بعض الأحيان لذلك دعونا نلقي نظرة على كيفية العمل
مع الأرقام في Python (:

هناك دالة رياضية واحدة متاحة دائمًا:

```python
round(number)    # rounding
```

يتم استيراد الكثير من الدوال الأخرى من مكتبة(module) `math` :

```python
from math import sin, cos, tan, sqrt, floor, ceil

sin(angle)       # sine
cos(angle)       # cosine
tan(angle)       # tangent
sqrt(number)     # square root

floor(angle)    # rounding down
ceil(angle)     # rounding up
```

### المساعدة (Help)

هناك بعض الدوال الأخرى التي تساعد المبرمجين:
يمكنك الحصول على مساعدة حول دالة معينة من البرنامج نفسه
(أو وحدة تحكم (console) Python) باستخدام دالة المساعدة (help function).
غالبًا ما يكون مفيدًا حتى للمبتدئين ، ولكن إذا لم يكن كذلك - فاستخدم Google.

سيتم عرض المساعدة ، حسب نظام التشغيل الخاص بك ،
إما في المتصفح أو مباشرة في المحطة (terminal).
إذا كانت المساعدة طويلة جدًا بالنسبة للمحطة(terminal) ، فيمكنك استعراض الصفحات باستخدام
  (<kbd>↑</kbd>, <kbd>↓</kbd>,
<kbd>PgUp</kbd>, <kbd>PgDn</kbd>) ويمكنك الخروج من خلال الضغط على المفتاح <kbd>Q</kbd> (مثل *إنهاء*).

يمكنك الحصول على مساعدة لـ `print` مثلا هكذا:

```python
help(print)
```

يمكنك أيضًا الحصول على المساعدة للمكتبة (module) بأكملها:

```python
import math

help(math)
```

### Random

أخيرًا وليس آخرًا ، سنلقي نظرة على دالتين من
`random` مفيدة جدًا للألعاب.

```python
from random import randrange, uniform

randrange(a, b)   # random integer from a to b-1
uniform(a, b)     # random float from a to b
```

احذر من أن <code>randrange(a, b)</code> لا ترجع القيمة `b` أبدًا.
عندما نحتاج إلى الاختيار بشكل عشوائي بين 3 خيارات ، فاننا نستخدم `randrange(0,3)`
الذي يقترح <code>0</code> أو <code>1</code> أو <code>2</code>:


```python
from random import randrange

number = randrange(0, 3)  # number - 0, 1, or 2
if number == 0:
    print('Circle')
elif number == 1:
    print('Square')
else:  # 2
    print('Triangle')
```

> [note]
> تذكر أنه عندما تريد استيرادالمكتبة `random` ، لا يمكنك تسمية ملفك الخاص `random.py`.


### والمزيد

هناك العديد من الدوال الأخرى المضمنة في بايثون نفسها ،
على الرغم من أنك ربما لا تفهمها في البداية.
يمكن العثور عليها جميعًا في وثائق Python ، على سبيل المثال:
<a href="https://docs.python.org/3/library/functions.html">الدوال المضمنة</a>,
<a href="https://docs.python.org/3/library/math.html">مكتبة الرياضيات</a>.
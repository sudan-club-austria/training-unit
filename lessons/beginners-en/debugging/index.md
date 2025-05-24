# ما هي الأخطاء البرمجية (Bugs)؟

الخطأ البرمجي (software bug) هو أي خطأ يتسبب في سلوك غير مرغوب فيه و
ينتج عنه نتائج غير صحيحة أو غير متوقعة.

يُرجح أن المصطلح نشأ من الهندسة الميكانيكية، حيث قد تتسلل **الحشرات (insects)**
إلى الآلات وتتسبب في أعطال ميكانيكية. ذكر إديسون
هذه الحالات في عام 1870. استمر المصطلح وانتقل إلى **هندسة البرمجيات (software engineering)**.

---

# ما هو تصحيح الأخطاء (Debugging)؟

مصطلح **تصحيح الأخطاء (debugging)** يعني *إيجاد* و *إزالة* الأخطاء في أنظمة البرمجيات.
ولهذا الغرض، تتوفر لدينا مجموعة واسعة من الأدوات التي تساعدنا في
العثور على الأخطاء والسياق الذي تحدث فيه.

---

# أنواع الأخطاء (Types of bugs)

## أخطاء بناء الجملة (Syntax Errors)

ينشأ هذا النوع من الأخطاء من **كود المصدر غير الصحيح نحويًا (syntactically incorrect source code)**. عادة ما تكون
هذه الأخطاء واضحة جدًا عند تنفيذ كود المصدر، وبالتالي يمكن
إصلاحها بسهولة تامة.

```python
>>> for x in in z:
  File "<stdin>", line 1
    for x in in z:
             ^^
SyntaxError: invalid syntax
```

## الأخطاء الحسابية (Arithmetic)

**الأرقام ذات الفاصلة العائمة (Floating point numbers)** غير دقيقة بطبيعتها، وقد تعطي أحيانًا
نتائج غير متوقعة. يجب أخذ ذلك في الاعتبار عند التعامل مع
الكسور كما في المثال التالي:

```python
>>> 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 == 1.0
False
```

## تصميم خاطئ (Wrong design)

في بعض الحالات، يكون التنفيذ (الكود) صحيحًا، ولكن **التصميم الأساسي (underlying design)**
معيب.

## تسرب الذاكرة (Memory leaks)

**تسرب الذاكرة (Memory leaks)** هي حالات أخطاء يتم فيها استهلاك المزيد والمزيد من الذاكرة عن طريق
إنشاء كائنات لا يتم تدميرها أبدًا، وبالتالي تتطلب ذاكرة لا يتم
تحريرها أبدًا. في مرحلة ما لن يتبقى ذاكرة وسيتعطل البرنامج.

```python
>>> mylist = list(range(1_000_000))
>>> while True:
...     mylist = mylist * 2
...     print(len(mylist))
...
2000000
4000000
8000000
16000000
32000000
64000000
128000000
256000000
512000000
1024000000
Killed
```
يمكن أن تكون تسربات الذاكرة دقيقة جدًا ويصعب ملاحظتها أحيانًا وقد تظهر
فقط في ظروف محددة مثل أوقات التشغيل الطويلة جدًا.

---

# العثور على الأخطاء (Finding bugs)

كما ذكرنا سابقًا، تظهر الأخطاء عادةً بسلوك غير متوقع
ونتائج خاطئة. عملية تصحيح الأخطاء هي تحديد مكان الأخطاء في سياقها
المحدد، لذلك من المفيد جدًا رؤية هذا السياق. يتكون السياق من:

* **المتغيرات (variables)** (المتغيرات المحلية والعالمية)
* **"مجمِّع الاستدعاءات" (call stack)**: مجمِّع استدعاءات الدوال في موقع محدد

لإظهار السياق والتفاعل معه، يمكننا استخدام أدوات معينة:

## تصحيح الأخطاء بأسلوب "الطباعة" ("Print-style" debugging)

هذا النمط من تصحيح الأخطاء شائع، حيث يمكن تنفيذه بسهولة عن طريق إضافة
عبارات `print` وعبارات مماثلة في الكود لإظهار الحالة الحالية
للبرنامج. وبالتالي، من السهل القيام به وله حاجز منخفض جدًا للدخول.

```python
import traceback

GLOBAL_VAR = 0

def a(a_arg):
    b(a_arg + 1)

def b(b_arg):
    my_variable = b_arg + 2
# we print out all our function arguments, local and global variables
    print(b_arg)
    print(my_variable)
    print(GLOBAL_VAR)

    traceback.print_stack()

a(10)
```

ومع ذلك، يأتي هذا النمط من البرمجة مع عيوب كبيرة:

* يجب عليك **تعديل كود المصدر (source code)** لتصحيح الأخطاء. غالبًا ما تُنسى عبارات الطباعة هذه
    وتبقى في كود المصدر لفترة طويلة جدًا.
* ليس من الممكن **التفاعل مع السياق (context)** أثناء تصحيح الأخطاء، يجب إيقاف البرنامج
    وتغييره وبدء تشغيله مرة أخرى.
* يمكن أن يصبح تتبع متغيراتك **فوضويًا** جدًا، حيث يجب طباعة اسم المتغير
    وقيمته، غالبًا قبل وبعد موقع معين.

## الاختبار (Testing)

كتابة الاختبارات وتشغيلها بانتظام يمكن أن يكون مفيدًا جدًا في تحديد مكان الأخطاء.
خاصة **اختبارات "الوحدة" (unit tests)** (أي: الاختبارات التي تختبر فئات (classes) أو دوال (functions))
يمكن أن تقلل من سياق فئة أو دالة لمعرفة ما إذا كانت تعمل كما
هو مقصود وخالية من الأخطاء.

```python
def area_rectangle(a, b):
    if not isinstance(a, (int, float)) or not isinstance(b, (int, float)):
        raise ValueError("Expected a number")
    if a < 0:
        raise ValueError("Invalid side length")
    if b < 0:
        raise ValueError("Invalid side length")
    return a * b

# we test the normal use of the function
def test_area_rectangle_normal():
    assert area_rectangle(2, 3) == 6

# we test some invalid arguments
def test_area_rectangle_types():
    with pytest.raises(ValueError) as e_info:
        area_rectangle(None, "str")

# we test some edge cases
def test_area_rectangle_negative():
    with pytest.raises(ValueError) as e_info:
        area_rectangle(2, -3)
```

## استخدام المصحح (Using a debugger)

**المصححات (Debuggers)** هي أدوات تمكننا من التفاعل مع برنامج *قيد التشغيل* بدون
الحاجة إلى تعديله. يمكننا إيقاف البرنامج مؤقتًا عند **نقاط توقف (break points)** محددة
حيث يمكننا فحص وتعديل السياق، وكذلك الانتقال *لأعلى* أو
*لأسفل* مجمع الاستدعاءات الحالي.

توجد أنواع مختلفة من المصححات، بعضها مدمج في بايثون
نفسها، وبعضها مدمج في محرر الأكواد، وبعضها متاح حتى كصفحة ويب.

سوف نناقش الآن الأكثر شيوعًا:

### PDB - مصحح بايثون (the Python De-Bugger)

PDB هو جزء من **مكتبة بايثون القياسية (python standard library)**، وبالتالي فهو متاح دائمًا.
يعتمد على النص ومخصص للاستخدام من سطر الأوامر.

يمكن استدعاؤه بعدة طرق:
* إما عن طريق استخدام استدعاءات `()breakpoint` في الكود الخاص بك
* أو عن طريق بدء نص بايثون الخاص بك بطريقة مختلفة قليلاً:
    `python -m pdb yourscript.py`

دعنا نستخدم النص التالي للتصحيح، ونحفظه باسم `test.py`:

```python
def myfunc(myarg):
    myinnerfunc(myarg)
    myinnerfunc(myarg - 1)


def myinnerfunc(innerarg):
    return 1 / innerarg


myfunc(1)
```

عندما نقوم بتشغيله بشكل طبيعي نحصل على هذه النتيجة:

```bash
$ python test.py
Traceback (most recent call last):
  File "test.py", line 10, in <module>
    myfunc(1)
  File "test.py", line 3, in myfunc
    myinnerfunc(myarg - 1)
  File "test.py", line 7, in myinnerfunc
    return 1 / innerarg
ZeroDivisionError: division by zero
```

نريد الآن تصحيح الملف باستخدام PDB:

```bash
$ python -m pdb test.py
> test.py(1)<module>()
-> def myfunc(myarg):
(Pdb)
```

يمكنك الآن رؤية أن البرنامج لم يبدأ بعد، ولكنك تحصل على موجه `(Pdb)`
الذي يسمح لك بإعداد الشروط المسبقة ونقاط التوقف في الكود الخاص بك
باستخدام الأوامر. يمكنك الحصول على قائمة بالأوامر عن طريق كتابة `help`:

```
(Pdb) help

Documented commands (type help <topic>):
========================================
EOF    c          d        h         list      q        rv       undisplay
a      cl         debug    help      ll        quit     s        unt
alias  clear      disable  ignore    longlist  r        source   until
args   commands   display  interact  n         restart  step     up
b      condition  down     j         next      return   tbreak   w
break  cont       enable   jump      p         retval   u        whatis
bt     continue   exit     l         pp        run      unalias  where

Miscellaneous help topics:
==========================
exec  pdb
```

يمكنك الحصول على وصف لأمر معين باستخدام `<help <cmd`:

```
(Pdb) help b
b(reak) [ ([filename:]lineno | function) [, condition] ]
        Without argument, list all breaks.

        With a line number argument, set a break at this line in the
        current file.  With a function name, set a break at the first
        executable line of that function.  If a second argument is
        present, it is a string specifying an expression which must
        evaluate to true before the breakpoint is honored.

        The line number may be prefixed with a filename and a colon,
        to specify a breakpoint in another file (probably one that
        hasn't been loaded yet).  The file is searched for on
        sys.path; the .py suffix may be omitted.
```

الأوامر التالية مهمة لنا في البداية:

* `b(reak)`: يسمح لنا بتعيين نقطة توقف (breakpoint)، وهي نقطة في برنامجك حيث
    نريد التوقف للفحص. يمكننا استخدام اسم دالة أو رقم سطر
    هنا. اختياريًا، يمكننا إضافة شرط، والذي سيحدد ما إذا كان يجب
    تشغيل نقطة التوقف أم لا.
* `c(ontinue)`: نريد متابعة التنفيذ العادي للبرنامج حتى نصل إلى
    نقطة التوقف التالية.
* `s(tep)`: أثناء الإيقاف المؤقت، قم بتنفيذ السطر التالي في برنامجك. إذا كانت
    دالة، ادخل إلى تلك الدالة واستمر في التنفيذ هناك.
* `n(ext)`: قم أيضًا بتنفيذ السطر التالي في برنامجك، ولكن لا تدخل إلى
    دالة. بدلاً من ذلك، يتم تشغيل الدالة بالكامل وتُرجع النتائج.
    يستمر تصحيح الأخطاء بعد ذلك.
* `w(here)`: أظهر مجمع الاستدعاءات الحالي وأين نقوم بتصحيح الأخطاء حاليًا.
* `u(p)`: انتقل لأعلى في مجمع الاستدعاءات (أي: الدالة التي استدعت).
* `d(own)`: انتقل لأسفل في مجمع الاستدعاءات. يعمل فقط عندما استخدمنا `up` من قبل.

نريد الآن تصحيح دالتنا، لذلك نضع نقطة توقف في دالتنا الداخلية:
```
(Pdb) b myinnerfunc
Breakpoint 1 at test.py:6
```

يمكننا الآن بدء البرنامج، وسيتوقف عند `myinnerfunc` الخاصة بنا:
```
(Pdb) c
> test.py(7)myinnerfunc()
-> return 1 / innerarg
```

يمكننا الآن التحقق من مكاننا الحالي في مجمع استدعاءات برامجنا:

```
(Pdb) w
  /usr/lib/python3.10/bdb.py(598)run()
-> exec(cmd, globals, locals)
  <string>(1)<module>()
  test.py(10)<module>()
-> myfunc(1)
  test.py(2)myfunc()
-> myinnerfunc(myarg)
> test.py(7)myinnerfunc()
-> return 1 / innerarg
```

ويمكننا طباعة متغيراتنا:

```
(Pdb) innerarg
1
```

يمكننا الآن الانتقال لأعلى في مجمع الاستدعاءات، لفحص المتغيرات في الدالة المستدعية:

```
(Pdb) up
> test.py(2)myfunc()
-> myinnerfunc(myarg)
```

من أجل رؤية سياقنا، يمكننا سرد (طباعة) كود المصدر في ذلك
الموقع وطباعة المتغير المحلي `myarg`:

```
(Pdb) l
  1     def myfunc(myarg):
  2  ->     myinnerfunc(myarg)
  3         myinnerfunc(myarg - 1)
  4
  5
  6 B   def myinnerfunc(innerarg):
  7         return 1 / innerarg
  8
  9
 10     myfunc(1)
[EOF]
(Pdb) myarg
1
```

يمكننا بعد ذلك الانتقال *لأسفل* في مجمع الاستدعاءات مرة أخرى:

```
(Pdb) d
> test.py(7)myinnerfunc()
-> return 1 / innerarg
```

يمكننا الآن اتخاذ خطوة التنفيذ *التالية* في البرنامج، والتي تحسب
النتيجة وتعيدها. يمكننا رؤية ذلك من خلال `--Return--` والنتيجة
المُعادة (`1.0<-`)، ويمكننا أيضًا رؤية أننا عدنا إلى الدالة العليا
`myfunc`:

```
(Pdb) n
--Return--
> test.py(7)myinnerfunc()->1.0
-> return 1 / innerarg
```

نظرًا لأننا نعلم أن الخطأ يحدث فقط عندما نكون في الاستدعاء الثاني للدالة `myinnerfunc`، يمكننا استخدام الأمر `continue` لمتابعة نفس نقطة التوقف (breakpoint) ولكن في المرة الثانية التي نستدعيها. يمكننا بعد ذلك أيضًا طباعة المتغيرات مرة أخرى:

```
(Pdb) c
> test.py(7)myinnerfunc()
-> return 1 / innerarg
(Pdb) innerarg
0
```

إذا قمنا الآن بتنفيذ السطر التالي، فسنثير الخطأ الأولي، وهو `ZeroDivisionError`. ومع ذلك، يمكننا ببساطة تجاوز المتغير  `innerarg` بقيمة أخرى
```
(Pdb) innerarg = 10
```

عندما ننفذ السطر التالي الآن، يمكن حساب القيمة وتُرجع النتيجة::

```
(Pdb) n
--Return--
> test.py(7)myinnerfunc()->0.1
-> return 1 / innerarg
```



### استخدام مصحح رسومي (Using a graphical debugger)

تسمح العديد من **بيئات التطوير المتكاملة (IDEs)** (مثل Visual Studio Code) بنهج **تصحيح أخطاء (debugging)** أكثر ملاءمة، مدمجة مباشرة في بيئة التطوير المتكاملة. تظل المفاهيم هي نفسها إلى حد كبير، ولكن يمكن استخدامها بطريقة أكثر ملاءمة، مباشرة حيث نكون نكتب الكود.

ستتعامل الأمثلة التالية مع الإعداد والتصحيح في Visual Studio Code.

لتصحيح ملف بايثون (Python)، يجب فتحه في المحرر. ثم يجب فتح **عرض التصحيح (debugging view)** (رمز المثلث مع الخطأ الصغير).

{{ figure( img=static('debugging-view.png'), alt='The Debugging view', ) }}

بعد ذلك، حدد "Python Debugger" ثم "Python File".

{{ figure( img=static('setup-1.png'), alt='Setup 1', ) }}
{{ figure( img=static('setup-2.png'), alt='Setup 2', ) }}

الآن يمكن أن يبدأ التصحيح فعليًا. بسهولة، يمكن تعيين **نقاط التوقف (breakpoints)** مباشرة في محرر النصوص بالنقر بجوار رقم السطر حيث تريد أن تكون نقطة التوقف. يمكن رؤية نقطة توقف نشطة كنقطة حمراء. سيؤدي النقر عليها إلى إزالتها مرة أخرى، وبنقر بالزر الأيمن يمكننا إضافة شرط لتشغيل نقطة التوقف.

{{ figure( img=static('breakpoint.png'), alt='Setting a breakpoint', ) }}
{{ figure( img=static('breakpoint-stop.png'), alt='Stopping at a breakpoint', ) }}

عندما نقوم بتشغيل الكود الخاص بنا، يمكننا بسهولة فحص **سياق برنامجنا (context of our running program)** قيد التشغيل، مما يوضح لنا المتغيرات (variables) وقيمها (حيث يمكننا أيضًا تعديلها):

{{ figure( img=static('context.png'), alt='The debugging context', ) }}

بشكل ملائم، يمكننا رؤية **مجمع الاستدعاءات (call stack)** (يمكننا ببساطة الانتقال لأعلى/لأسفل بالنقر على العنصر في المجمع) ويمكننا أيضًا رؤية قائمة بجميع نقاط التوقف، والتي يمكن بعد ذلك تمكينها/تعطيلها. توجد أيضًا نقاط توقف لجميع الاستثناءات (exceptions) التي تم إثارتها أو الاستثناءات غير الملتقطة (uncaught exceptions)، والتي يمكن أن تساعد أيضًا.

عند تصحيح الأخطاء، تكون هذه النافذة الصغيرة لعناصر التحكم متاحة للسماح بالتنقل في الكود:

{{ figure( img=static('controls.png'), alt='The debugging controls', ) }}

المثلث الأزرق يسمح بالمتابعة إلى نقطة التوقف التالية (نفس `c(continue)` في PDB). السهم الموجود فوق النقطة ينفذ السطر التالي، ولكنه لا يدخل إلى دالة (نفس `n(ext)`). السهم المتجه لأسفل إلى النقطة يقوم بالخطوة التالية، ولكنه يدخل أيضًا إلى دالة (نفس `s(tep)`). بينما يقوم السهم المتجه لأعلى بتشغيل الدالة حتى نهايتها حتى تعود. الخطأ الأخضر لإعادة التشغيل يعيد تشغيل البرمجة والمربع الأحمر يوقف البرنامج.

---

### الخلاصة (Conclusion)

**تصحيح الأخطاء (Debugging)** هو نشاط ضروري للتخلص من **الأخطاء (bugs)** في برامجنا، سواء استخدمنا **تصحيح الأخطاء بأسلوب `print()` (print()-style debugging)** أو استخدمنا **أداة مخصصة (dedicated tool)**.

الأدوات المخصصة أكثر تعقيدًا، ولكنها أقوى بكثير في مساعدتنا على فهم المشكلات والسياقات المحددة التي تظهر فيها.
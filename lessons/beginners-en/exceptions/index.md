# الاستثناءات (Exceptions)

لقد تحدثنا بالفعل عن [رسائل الخطأ]({{ lesson_url('beginners-en/print') }}).
عند وقوع خطأ، تتذمر بايثون، وتخبرنا بمكان الخطأ (السطر)،
وتنهي البرنامج. ولكن هناك الكثير مما يمكننا تعلمه عن
رسائل الخطأ (المعروفة أيضًا باسم *الاستثناءات* - exceptions).

## طباعة الأخطاء:

دعنا نكرر كيف تطبع بايثون خطأً موجودًا في دالة متداخلة.

```python
def outer_function():
    return inner_function(0)

def inner_function(divisor):
    return 1 / divisor

print(outer_function())
```

عندما نقوم بتشغيل الكود، يتوقف بسبب خطأ ورسالة مثل:

```pycon
Traceback (most recent call last):
  File "example.py", line 7, in <module>
    print(outer_function())
  File "example.py", line 2, in outer_function
    return inner_function(0)
  File "example.py", line 5, in inner_function
    return 1 / divisor
ZeroDivisionError: division by zero
```

لا يمكن لبايثون أن تعرف مكان الخطأ الأصلي الذي يحتاج إلى إصلاح، لذا فهي تعرض
لك كل شيء في رسالة الخطأ.

إما أننا لا يجب أن نستدعي `in_func` بالوسيط `0`.

أو يجب كتابة `in_function` للتعامل مع حالة أن المقسوم يمكن أن يكون `0`
ويجب أن تفعل شيئًا آخر غير محاولة القسمة على صفر.

## رفع استثناء (Raising an exception)

في بايثون، يتم رفع *استثناء* (exception) بواسطة الأمر `raise`.
يتبع الأمر اسم الاستثناء الذي نريد رفعه
ووصف قصير اختياري لما حدث خطأ (بين قوسين).

```python
MAX_ALLOWED_VALUE = 20

def verify_number(number):
    if number < 0 or number >= MAX_ALLOWED_VALUE:
        raise ValueError(f"The number {number} is not in the allowed range!")
    print(f"The number {number} is OK!")

verify_number(5)
verify_number(25)
```

ما هي الاستثناءات المتاحة في بايثون؟
توفر بايثون تسلسلًا هرميًا للاستثناءات القياسية (المضمنة - built-in). هذا
مجرد مجموعة فرعية منها:

```plain
BaseException
 ├── SystemExit                     raised by function exit()
 ├── KeyboardInterrupt              raised after pressing Ctrl+C
 ╰── Exception
      ├── ArithmeticError
      │    ╰── ZeroDivisionError    zero division
      ├── AssertionError            command `assert` failed
      ├── AttributeError            non-existing attribute, e.g. 'abc'.len
      ├── ImportError               failed import
      ├── LookupError
      │    ├── IndexError           non-existing index, e.g. 'abc'[999]
      │    ╰── KeyError             non-existing dictionary key
      ├── NameError                 used a non-existing variable name
      │    ╰── UnboundLocalError    used a variable that wasn't initiated
      ├── OSError
      │    ╰── FileNotFoundError    requested file does not exist
      ├── SyntaxError               wrong syntax – program is unreadable/unusable
      │    ╰── IndentationError     wrong indentation
      │         ╰── TabError        combination of tabs and spaces
      ├── TypeError                 wrong type, e.g. "a" + 1
      ╰── ValueError                wrong value, e.g. int('xyz')
```

> [note] ماذا يعني هذا التسلسل الهرمي؟
>
> التسلسل الهرمي للاستثناءات يشبه شجرة عائلة مع النوع الأكثر عمومية
> من الاستثناء كجذر، وكل فرع يصبح أكثر تحديدًا.
> على سبيل المثال، `KeyError` هو أيضًا `LookupError` و `Exception` ولكنه
> ليس، على سبيل المثال، `SyntaxError`.
>
> في الوقت الحالي، يكفي القول أن الاستثناءات هي **فئات** (classes) و
> أن الاستثناءات **الفرعية** (child) الأكثر تحديدًا **ترث** (inherit) خصائص
> **الأصل** (parent) العام الأكثر عمومية. أي أن `Exception` هي الفئة الأصل
> لـ `LookupError` و `LookupError` هي الفئة الأصل لـ
> استثناء `KeyError`. لذلك فإن `KeyError` له خصائص
> استثناءات `LookupError` و `Exception`.

للحصول على القائمة الكاملة للاستثناءات المضمنة، راجع [وثائق بايثون](https://docs.python.org/3/library/exceptions.html).

## معالجة الاستثناءات (Handling Exceptions)

لماذا يوجد الكثير من الاستثناءات المضمنة؟ لأنه بهذه الطريقة يمكننا بسهولة أكبر
*التقاط* (catch) استثناءات حالات خطأ محددة.

ليس من المرغوب دائمًا أن يقتل استثناء برنامجنا. ولا يمكننا أيضًا
(أو لا نريد) تغطية جميع حالات الخطأ المحتملة في الكود
التي يتم رفع الاستثناءات منها.

دعني أريك مثالاً:

```python
def prompt_number():
    answer = input('Enter some number: ')
    if not answer:
        return None
    try:
        number = int(answer)
    except ValueError:
        print('That is not a number! I will continue with 0')
        number = 0
    return number

print("Press ENTER to stop the script.")
while True:
    number = prompt_number()
    if number is None:
        break
    print(f"Entered number: {number}")
```

قم بتشغيل الكود وجرب مدخلات مختلفة. ماذا يحدث إذا كان الإدخال ليس
عددًا صحيحًا؟

لا يتسبب الإدخال غير الصالح في حدوث خطأ، بل يتم استبداله بـ `0`.

إذن كيف يعمل هذا؟

نستدعي الدالة `()int` داخل كتلة `try`.
إذا لم يكن هناك خطأ، يتم تنفيذ هذه الدالة، وتُرجع قيمة
يتم تعيينها للمتغير `number` وتترك كتلة `try`.

في حالة رفع استثناء `ValueError` بواسطة `()int` بسبب إدخال غير صالح
القيمة، يتم التقاط هذا الاستثناء ويستمر التنفيذ
في كتلة `except ValueError`. هناك، يتم طباعة رسالة و
يتم تعيين `0` للمتغير `number`.

في هذه الحالة، نقوم بالتقاط استثناء `ValueError` تحديدًا.
يمكننا تحقيق نفس الشيء عن طريق التقاط استثناء عام `Exception`، لأنه، كما يمكنك
أن ترى في التسلسل الهرمي أعلاه، `ValueError` هو نوع محدد من `Exception`.

## لا تلتقطهم جميعًا\! (Don't catch'em all\!)

حاول أن تكون انتقائيًا قدر الإمكان عند التقاط الاستثناءات المتوقعة.
ليست هناك حاجة لالتقاط معظم الأخطاء.

> [note]
> عند حدوث خطأ غير متوقع، من **الأفضل بكثير** إنهاء البرنامج
> بدلاً من الاستمرار بقيم خاطئة.
> عند حدوث خطأ غير متوقع، نريد أن نعرف عنه بمجرد
> ظهوره. مع القيم الخاطئة، ستحدث أشياء سيئة لاحقًا في الكود على أي حال
> وسيكون السبب الحقيقي **صعبًا** للتتبع.

على سبيل المثال، التقاط استثناء `KeyboardInterrupt`
يمكن أن يكون له تأثير جانبي يتمثل في عدم إمكانية إنهاء البرنامج إذا احتجنا إلى ذلك
(باستخدام الاختصار \<kbd\>Ctrl\</kbd\>+\<kbd\>C\</kbd\>).

استخدم الأمر `try/except` فقط في الحالات التي
تتوقع فيها بعض الاستثناءات، أي أنك تعرف بالضبط ما يمكن أن يحدث
ولماذا، وأنت قادر على إصلاح حالة الخطأ في كتلة `except`.

مثال نموذجي سيكون قراءة الإدخال من المستخدم. إذا قام المستخدم
بإدخال كلام غير مفهوم، فمن الأفضل أن تسأل مرة أخرى حتى
يقوم المستخدم بإدخال شيء ذي معنى:

```pycon
>>> def fetch_number():
...     while True:
...         answer = input("Type a number: ")
...         try:
...             return int(answer)
...         except ValueError:
...             print("Oi! This is rubbish, mate! Do it again!")
>>> fetch_number()
Type a number: nan
Oi! This is trash, mate! Do it again!
Type a number: 42
42
```

## بنود أخرى (Other clauses)

بالإضافة إلى `except`، هناك بندان آخران - كتلتان يمكن
استخدامهما مع `try`، وهما `else` و `finally`.

سيتم تشغيل الأول `else` إذا لم يتم رفع أي استثناء في كتلة `try`.
ويتم تشغيل `finally` في كل مرة ويتم تنفيذه حتى في حالة وجود استثناء غير معالج
ويمكن استخدامه حتى بدون أي بند `except`. يستخدم في الغالب لعمليات التنظيف.

يمكن أن يكون لديك أيضًا عدة كتل `except`. سيتم تشغيل واحدة فقط منها.
الأول الذي يمكنه معالجة الاستثناء المرفوع.

> [note]
> قم دائمًا بالتقاط الاستثناءات الأكثر تحديدًا قبل الاستثناءات العامة.

```python
try:
    do_something()
except ValueError:
    print("This will be printed if there's a ValueError.")
except NameError, KeyError:
    print("This will be printed if there's a NameError or KeyError.")
except Exception as e:
    print("This will be printed if there's some other exception.")
    print(e)
    # (apart from SystemExit a KeyboardInterrupt, we don't want to catch those)
except TypeError:
    print("This will never be printed")
    # ("except Exception" above already caught the TypeError)
else:
    print("This will be printed if there's no error in try block")
finally:
    print("This will always be printed; even if there's e.g. a 'return' in the 'try' block.")
```

## مهمة (Task)

دعنا نضيف معالجة الاستثناءات والتحقق الصحيح من الإدخال الى برنامج حساب مساحة المربع
من [درس المقارنات]({{ lesson_url('beginners-en/comparisons') }}).

قم بتعديل الكود بحيث حتى يقوم المستخدم بإدخال قيمة غير سالبة
سيستمر البرنامج في طلب الإدخال مرة أخرى.

{% filter solution %}

```python
def input_side():
    while True:
        raw_input = input("Enter the side of a square in centimeters: ")
        try:
            side = float(raw_input)
        except ValueError:
            print(f"{raw_input} is not a number!")
        else:
            if side <= 0:
                print(f"{raw_input} is a negative number!")
            else:
                break
    return side
side = input_side()
print(f"The perimeter of a square with a side of {side} cm is {side * 4} cm.")
print(f"The area of a square with a side of {side} cm is {side ** 2} cm2.")

```

{% endfilter %}
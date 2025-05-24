# واجهة سطر الأوامر في بايثون (Command line interface in Python)
=======================================

في هذا الدرس، سنوضح لك كيفية إنشاء أداة **واجهة سطر الأوامر (Command Line Interface - CLI)** الخاصة بك باستخدام بايثون (Python) ومكتبة **`argparse`**. يعني هذا بشكل أساسي معالجة **قيم البرنامج (program argument processing)**.

## واجهة سطر الأوامر (Command line interface)

... هي إحدى طرق التفاعل مع أو التحكم في برنامج (ليس فقط نصوص بايثون!) كمستخدم - **تفاعل (interface)** معه من داخل الكمبيوتر نفسه حيث تم تثبيته (وليس عبر الإنترنت).
يمكن أن يكون هذا المستخدم هو أنت كمنشئ للكود أو شخص آخر تمنحه حق الوصول إليه.

### الدافع (Motivation)

في [درس الاختبار (testing lesson)]({{ lesson_url('beginners-en/testing') }})، أوضحنا أنه في بعض الأحيان تحتاج إلى استدعاء برنامج بايثون بشكل مستقل باستخدام **قيم (arguments)** مختلفة لتشغيل عمليات حسابية بقيم مختلفة.

إن السماح للمختبر أو المستخدم بتمرير هذه **القيم (arguments)** من سطر الأوامر (والذي يعني عدم تحريرها يدويًا داخل نص بايثون) هو خيار رائع.

يتنوع سلوك البرنامج عادةً - فهو يعتمد على التعليمات
التي تقدمها له ك**قيم (arguments)**.

### مثال (Example)

إذا كنت ترغب في معرفة القيم التي يسمح بها برنامج موجود، فإن القيمة (argument) التي يجب استخدامها هي **`help`**. يعمل هذا لمعظم البرامج على جهاز الكمبيوتر الخاص بك (إذا قام مؤلفها بإنشاء صفحة مساعدة). عادةً ما يكون هناك أيضًا قيمة سطر أوامر **`help-`** أو **`help--`** والتي تعرض أيضًا الاستخدام المتوقع للأداة لأي مستخدم.

#### `git`

كمثال لأداة تعمل على كل من لينكس (Linux) وويندوز (Windows) بنفس الطريقة تقريبًا، يمكنك أخذ [git]({{ lesson_url('git-en/basics') }}) المحبوبة.

جرب تشغيل هذا في ال (terminal) الخاصة بك:

```console
git --help
```

ولأي أمر فرعي (subcommand) أيضًا:

```console
git log --help
```

الآن بعد أن عرفت أن البرامج تقبل عادةً القيم وأنها موثقة في ``help``، يمكنك البدء في استخدام ``git`` بعدة طرق.
على سبيل المثال، يمكنك تخصيص إخراج `git log` بشكل كبير في بعض مستودعات Git الموجودة:

```console
git log --oneline --graph --decorate --cherry-mark --boundary
```

> [note]
> **ملاحظة حول معالجة قيم سطر الأوامر "الخام" (raw command line argument handling)**
>
> لقراءة قيم سطر الأوامر (command line arguments)، يمكننا استخدام المتغير `sys.argv`، والذي يعطينا قائمة من النصوص (list of strings)، واحد لكل **قيمة (argument)** تم تمريرها:
> ```python
> # arguments.py
> import sys
>
> for arg in sys.argv:
>     print(arg)
> ```
> عندما ننفذ هذا البرنامج مع القيم التي تم تمريرها، يمكننا رؤيتها مطبوعة.
> ومع ذلك، هذا ليس مريحًا جدًا عندما نريد بناء برامج CLI فعلية بخيارات (options) و**قيم (arguments)**. ولكن هناك أدوات جيدة يمكننا استخدامها بدلاً من ذلك!

### `Argparse`

كيف يمكننا إنشاء CLI في بايثون؟ اليوم، سنعرض استخدام أداة **`argparse`**. إنها جزء من **المكتبة القياسية (standard library)**، لذلك لا تحتاج إلى تثبيت أي شيء إضافي.

يمكنك العثور على الوثائق الرسمية هنا: [argparse](https://docs.python.com/3/library/argparse.html)

ودليل تعليمي مفيد جدًا يمر بمعظم الوظائف التي قد تواجهها:
[argparse-tutorial](https://docs.python.org/3/howto/argparse.html#argparse-tutorial)

بالإضافة إلى ذلك، توجد مكتبة **`click`** شائعة الاستخدام جدًا، والتي ستحتاج إلى تثبيتها عبر `pip`
وتستخدم بناء جملة **مُزخرف (decorator syntax)**، الذي لم نراه بعد، لذلك يمكن أن يظل كدراسة ذاتية.

#### الاستخدام الأساسي لـ `argparse` (argparse basic usage)

عادةً عندما نرسل كود بايثون الخاص بنا إلى شخص آخر، لا نتوقع منهم قراءة الكود بأكمله، بل يجب أن تكون قراءة المساعدة كافية لهم لاستخدامه وتغيير المعلمات.

بالنسبة لأدوات Python CLI، ستحصل على المساعدة بهذه الطريقة، والتي ترى أنها هي نفسها كما في `git`:

```console
python3 hello.py --help
```

إليك كيفية إنشاء تطبيق سطر أوامر بايثون بمفاتيح:

لكن أولاً، لنبدأ بدالة تحيي المستخدم لعدد معين من المرات ويمكنها اختياريًا إضافة مسافة بادئة للتحية.

لنحفظ الكود التالي في ملف `hello.py`.

```python
def hello(count, name, indent=False):
    """Simple program that greets 'name' for a total of 'count' times and optionally indents."""
    for _ in range(count):
        if indent:
            print("    ", end="")
        print(f"Hello {name}!")

count = 5
name = "Baloola"
indent = True
hello(count, name, indent)
```

وشغّله كالمعتاد كـ `python hello.py`.

الآن نريد أن تكون **القيم (arguments)** `count` و `name` و `indent` متاحة كخيارات CLI وتأتي من قيم سطر الأوامر (command line arguments) عندما تبدأ النص البرمجي.

```python
import argparse

parser = argparse.ArgumentParser(description='argparse greeting')
parser.add_argument('-n', '--name', help='a name to repeat', required=True)
parser.add_argument('-c', '--count', help='how many times', required=True, type=int)
parser.add_argument("--indent", action="store_true", help=("name will be indented by 4 spaces"))

def hello(count, name, indent=False):
    """Simple program that greets 'name' for a total of 'count' times and optionally indents."""
    for _ in range(count):
        if indent:
            print("    ", end="")
        print(f"Hello {name}!")

args = parser.parse_args()
hello(args.count, args.name, args.indent)
```

الخطوة الأولى في استخدام `argparse` هي إنشاء (object) يدعى **`ArgumentParser`** مع بعض الوصف.
ثم تقوم بملء `ArgumentParser` بمعلومات حول **قيم البرنامج (program arguments)**، ويتم ذلك عن طريق إجراء استدعاءات لطريقة **`()add_argument`**.
يتم تخزين هذه المعلومات واستخدامها عند استدعاء **`()parse_args`**.

يمكنك تعيين المعلمات على أنها مطلوبة (required) عن طريق إضافة خيار **`required=True`**.
من الممكن أيضًا تحديد **`type` (النوع)** الخاص بها، والذي سيحاول تحويل المتغير إلى نوع البيانات المعلن عنه.
للسماح بالتخزين البسيط للأعلام المنطقية **`True/False`  **، يمكنك استخدام المعامل **`action="store_true"`**.

```console
python3 hello.py
python3 hello.py --help
python3 hello.py --name PyLady
python3 hello.py --count 5
python3 hello.py --count 5 --name PyLady
python3 hello.py --count 5 --name PyLady --indent
```

هذا بالفعل برنامج أول قوي جدًا أليس كذلك؟

---

## القيم الموضعية (Positional arguments)

يمكنك بالطبع تعريف **قيم (arguments)** تكون **موضعية (positional)** بنفس الطريقة التي تحدد وتستخدم بها قيم الدالة. سيتوقع التحليل أن تكون جميع القيم بالترتيب الذي حددتها به.

لتجربتها، استبدل السطرين الأولين بـ **قيم (arguments)** `name` و `count` بالأسطر التالية:

```python
parser.add_argument("name", help='a name to repeat')
parser.add_argument("count", help='how many times', type=int)
```

من الآن فصاعدًا، سيكون الترتيب الذي تقدم به **قيمتي (arguments)** `name` و `count` مهمًا. لا يزال من الممكن تقديم القيم المسماة قبل أو بعد القيم الموضعية.

```console
python3 hello.py Hashim 5 --indent
```

مثال على استدعاء خاطئ سيكون:

```console
python3 hello.py 5 Hashim
```

والذي يجب أن يؤدي إلى الخطأ التالي:

```
hello.py: error: argument count: invalid int value: 'Hashim'
```

---

## خيارات أخرى (Other options)

تبدأ أسماء المفاتيح (switch names)، وفقًا لاتفاقية يونكس (Unix convention)، بالعلامات الواصلة (hyphens): واصلة واحدة `-`
للاختصارات ذات الحرف الواحد، وواصلتين `--` للأسماء متعددة الأحرف.
يمكن أن يحتوي المفتاح الواحد على أكثر من اسم - **خيار قصير (short option)** و **خيار طويل (long option)**.

يوضح هذا المثال كيفية القيام بذلك عادةً على سبيل المثال لإعداد **التسجيل (logging)** - على الرغم من أنه لا ينطبق على مثالنا البسيط.

```python
parser.add_argument(
        "-v", "--verbosity", type=int, default=3, choices=[0, 1, 2, 3, 4],
        help=(
            "Set verbosity of log output "
            "(4=DEBUG, 3=INFO, 2=WARNING, 1=ERROR, 0=CRITICAL). (default: 3)"
        ),
    )
```

ستقوم أسماء المعلمات التي تحتوي على **واصلات (hyphens)** بداخلها بتحويلها تلقائيًا إلى أسماء متغيرات
مع **تسطير سفلي (underscores)**، حيث لا يمكن أن يكون هناك **واصلة `-` (hyphen)** في اسم المتغير في بايثون.

```python
parser.add_argument(
        "--extreme-universe",
        action="store_true", help=("Computations will return all results to the power of 2.")
    )
args = parser.parse_args()
print(args.extreme_universe)

```

إذا استخدمت المزيد من الخيارات ذات الواصلتين، فأنت بحاجة إلى الوصول إلى القيم من ال(object) **`args`**
عبر الخيار الأول، كما في هذا المثال:

```python
parser.add_argument('-n', '--name', '--firstname', help='a name to repeat', required=True)
hello(args.count, args.name, args.indent)
```

```console
# both work
python3 hello.py --name Hashim --count 5
python3 hello.py --firstname Hashim --count 5
```

كانت هذه مقدمة قصيرة للعمل مع **واجهة سطر الأوامر (CLI)**.
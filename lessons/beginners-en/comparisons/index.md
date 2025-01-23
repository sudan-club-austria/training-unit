# المقارنات (Comparisons)

هل لا تزال تتذكر ما هو **المعامل (operator)**؟

في واجباتنا المنزلية ، تعلمنا بعض المعاملات الحسابية الأساسية.
إذا أضفنا معامل (operator) أساسي آخر (`//` للقسمة الصحيحة) ، فستبدو قائمتنا كما يلي:

<table class="table">
    <tr>
        <th>الرمز</th>
        <th>مثال</th>
        <th>وصف</th>
    </tr>
    <tr>
        <td><code>+</code>, <code>-</code>, <code>*</code>, <code>/</code></td>
        <td><code>1 + 1</code></td>
        <td>المعاملات الاساسية</td>
    </tr>
    <tr>
        <td><code>-</code></td>
        <td><code>-5</code></td>
        <td>النفي (negation)</td>
    </tr>
    <tr>
        <td><code>//</code>; <code>%</code></td>
        <td><code>7 // 2</code>; <code>7 % 2</code></td>
        <td>القسمة الصحيحة ، الباقي من القسمة</td>
    </tr>
    <tr>
        <td><code>**</code></td>
        <td><code>3 ** 2</code></td>
        <td>الأس (3 أس 2)</td>
    </tr>
</table>

يحتوي Python أيضًا على أنواع أخرى من المعاملات (operators). تُستخدم عوامل المقارنة (relational) لمقارنة القيم.
جرب ما تفعله!

(يمكنك تجربتها باستخدام `()print` في الكود الخاص بك ،
أو يمكنك تجربة سطر أوامر `python`).

<table class="table">
    <tr>
        <th>الرمز</th>
        <th>مثال</th>
        <th>وصف</th>
    </tr>
    <tr>
        <td><code>==</code>, <code>!=</code></td>
        <td><code>1 == 1</code>, <code>1 != 1</code></td>
        <td>يساوي ، لا يساوي</td>
    </tr>
    <tr>
        <td><code>&lt;</code>, <code>&gt;</code></td>
        <td><code>3 &lt; 5</code>, <code>3 &gt; 5</code></td>
        <td>أكبر من ، أقل من</td>
    </tr>
    <tr>
        <td><code>&lt;=</code>, <code>&gt;=</code></td>
        <td><code>3 &lt;= 5</code>, <code>3 &gt;= 5</code></td>
        <td>أكبر أو يساوي ، أقل أو يساوي</td>
    </tr>
</table>

تسمى قيم المقارنة **قيم منطقية (boolean)**
(نسبة ل[جورج بول](http://en.wikipedia.org/wiki/George_Boole)).
يتم استخدامها في كل مرة نريد فيها معرفة ما إذا كان شيء ما `صواب` أو `خاطئ`.
التعبيرات المنطقية هي بالضبط هذان : `صواب` و `خاطئ`.

مثل جميع القيم ، يمكن تعيين `صواب` و `خاطئ` للمتغيرات:

```python
true = 1 < 3  # we have to type it in lowercase now, because True is a reserved word in Python
print(true)

false = 1 == 3
print(false)
```

> [note]
> لاحظ أنه لاختبار المساواة ، يجب عليك استخدام علامتي تساوي: `3 == 3`.
> علامة تساوي واحدة تُعيِّن او تحفظ قيمة إلى متغير ، وعلامتا تساوي
> تقارن بين قيمتين (من المتغيرات).

يمكن استخدام <code>True</code> و <code>False</code>
مباشرة في البرنامج.
فقط انتبه إلى أن وضع الأحرف (capital).

```python
print(True)
print(False)
```

## الشروط (Conditions)



{% if var('pyladies') -%}
{% set rootname = 'pyladies' %}
{%- else -%}
{% set rootname = 'naucse-python' %}
{%- endif %}

اكتب ما يلي في ملف جديد (مثل `if.py`):

```python
side = float(input('Enter the side of a square in centimeters: '))
print("The perimeter of a square with a side of", side,"cm is ", side * 4,"cm.")
print("The area of a square with a side of", side,"cm is", side * side, "cm2.")
```

## ماذا يحدث عندما تدخل رقمًا سالبًا؟ هل النتيجة منطقية؟

كما نرى ، يقوم الكمبيوتر بما هو مطلوب منه بالضبط ولا يفكر في السياق. عليك أن تفعل ذلك من أجله.
سيكون من الجيد لو تمكن البرنامج من إخبار المستخدم الذي يدخل
رقمًا سالبًا أنهم أدخلوا قيمة غير منطقية.
كيف نفعل ذلك؟

دعونا نحاول تعيين متغير (variable) يكون `صواب (True)` عندما يدخل المستخدم رقمًا موجبًا.

{% filter solution %}
    يمكنك تعيين المتغير variable على النحو التالي:

    ```python
    side = float(input('Enter the side of a square in centimeters: '))
    positive_number = side > 0
    ```
{% endfilter %}

ثم سنخبر البرنامج باستخدام هذا المتغير variable.
لهذا الغرض ، سنستخدم عبارات `if` و `else`.


```python
side = float(input('Enter the side of a square in centimeters: '))
positive_number = side > 0


if positive_number:
    print("The perimeter of a square with a side of", side,"cm is", side * 4,"cm.")
    print("The area of a square with a side of", side,"cm is", side * side, "cm2.")
else:
    print("The side must be a positive number!")

print("Thank you for using the geometric calculator.")

```

إذن بعد `if` ، يوجد *شرط* وهو
التعبير الذي سنستخدمه لاتخاذ القرار.
بعد الشرط يجب أن تكتب نقطتين (:).
و من ثم تكتب بعد النقطتين الأوامر التي سيتم تنفيذها إذا كان الشرط `صواب True`.
تذكر، بعد كل نقطتين في بايثون، عليك إزاحة الأسطر التالية بمقدار 4 مسافات.

ثم على نفس مستوى `if` ، اكتب `else` متبوعًا بـ `colon :`. الأسطر التالية
تحتوي على الأوامر التي يتم تنفيذها إذا كان الشرط `خاطئ False` ، ويجب أن تحتوي على مسافة (indent) أيضًا. <br>

يمكنك بعد ذلك كتابة كود آخر ، و بدون مسافة (indent) وسيتم تنفيذه في كل مرة ، لأن
ال `if` statement `code block` قد انتهت بالفعل

> [note]
> لا يلزم أن تكون المسافة البادئة 4 مسافات ، يمكنك استخدام
> 2 أو حتى 11 ، أو يمكنك استخدام زر ال Tab . المقصود هو أن
> ضمن كتلة كود واحدة ، يجب أن تكون المسافة البادئة هي نفسها.
> لذلك إذا كنت تعمل على مشروع مع شخص آخر ، فأنه
> يجب ألإتفاق على المسافة للبرنامج
> لتتمكن من تشغيله بشكل صحيح. معظم الناس
> من مجتمع Python يتفقون على 4 مسافات.

## عبارات شرطية أخرى (Other conditional statements)

في بعض الأحيان لا تكون عبارة `else` ضرورية.
بحيث لا يفعل السطر البرمجي التالي أي شيء إضافي إذا لم يكن الرقم اكبر من الصفر.

```python
number = int(input('Enter a number, to which I will add 3: '))
if number < 0:
    print('Negative number detected!')
print(number, '+ 3 =', number + 3)
```

في بعض الأحيان تكون هناك حاجة إلى عدة شروط. لهذا الموقف ، لدينا عبارة `elif`
(مزيج من `else` و `if`). تكون بين `if` و `else`.
يمكنك تكرار كلمة `elif` بعد أول `if` ، ولكن
سيتم تنفيذ فرع واحد فقط ، بالتحديد: الأول
حيث تتحقق الشروط (إنها `صواب True`).


```python
age = int(input('How old are you? '))
if age >= 150:
    print('And from which planet are you?')
elif age >= 10:
    # This branch will not be executed for "200", for example.
    print('We can offer: Cofee, Tea, or sharboot.')
elif age >= 1:
    print('We can offer: Milk, Ovaltine, or water')
elif age >= 0:
    print('Unfortunately, we are out of baby formula.')
else :
    # If no condition is met from above, the age had to be negative.
    print('Visitors from the future are not welcomed here!')
```

## مثال : ملابس الشتاء (Winter clothing)

الجزء التالي من التعليمات البرمجية متقدم بعض الشيء ولن نناقشه بالكامل الآن. حاليا تحتاج فقط إلى فهم أنها ستقوم بتحميل درجة الحرارة الحالية في مدينة فيينا من الإنترنت و حفظها إلى متغير variable:

```python
from urllib.request import urlopen
url = "https://wttr.in/Wien?format=%t"
temperature = int(urlopen(url).read().decode().strip("°C"))
```

الان اكتب برنامجًا يستخدم `if` و `elif` و `else` والذي يطبع ما إذا كنت ستحتاج إلى سترة ، أو سترة خفيفة أو معطف شتوي اعتمادًا على درجة الحرارة الحالية:

{% filter solution %}

    ```python
    from urllib.request import urlopen
    url = "https://wttr.in/Wien?format=%t"
    temperature = int(urlopen(url).read().decode().strip("°C"))

    if temperature >= 20:
        print("No jacket needed, enjoy the warm temperature")
    elif temperature >= 10:
        print("Light jacket recommended")
    else:
        print("It's freezing, you'll need a winter coat")
    ```
{% endfilter %}


## مثال: حجر ورقة مقص (Rock paper scissors)

يمكن ادراج عدة عبارات `if` - داخل عبارة `if` و إزاحتها 4 مسافات (indentation)
وهذا ما يسمى بال nested `if`


```python
pc_choice = 'rock'
user_choice = input('rock, paper, or scissors?')

if user_choice == 'rock':
    if pc_choice == 'rock':
        print('Draw.')
    elif pc_choice == 'scissors':
        print ('You win!')
    elif pc_choice == 'paper':
        print ('Computer won!')
elif user_choice == 'scissors':
    if pc_choice == 'rock':
        print('Computer won!')
    elif pc_choice == 'scissors':
        print('Draw.')
    elif pc_choice == 'paper':
        print('You win!')
elif user_choice == 'paper':
    if pc_choice == 'rock':
        print('You win!')
    elif pc_choice == 'scissors':
        print('Computer won!')
    elif pc_choice == 'paper':
        print('Draw.')
else:
    print('I do not understand.')

```

**تهانينا!!!** <br>
الآن نريد ان نجعل اختيار الكمبيوتر يعمل بشكل عشوائي. نحتاج إلى تغيير قيمة `pc_choice`. سنناقش كيفية القيام بذلك في المرة القادمة.

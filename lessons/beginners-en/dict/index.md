# القواميس

نوع بيانات أساسي آخر سنقدمه هو *القاموس*، أو باختصار، `dict`.

القاموس هو هيكل بيانات يتكون من أزواج متعددة من *مفتاح/قيمة*،
يربط *المفاتيح* بقيمها المقابلة. غرضه الرئيسي هو العثور بسرعة وكفاءة على قيمة لمفتاح معين.

تفرض بايثون قيودًا على ما يمكن أن تكون عليه *مفاتيح* القاموس.
يجب ألا تتكرر المفاتيح (لا يمكن لمفتاح واحد أن يرتبط بقيمتين مختلفتين)
ويجب ألا تكون قابلة للتغيير (القيم *القابلة للتعديل*، مثل القوائم والقواميس
لذلك غير مسموح بها). مفاتيح السلاسل النصية هي الأكثر شيوعًا، على الرغم من استخدام أنواع أخرى مثل الأرقام والمجموعات أيضًا.

يمكن أن تكون *القيم* المستهدفة، كما في حالة، على سبيل المثال، القوائم، أي شيء
يمكن تعيينه لمتغير. يمكن أن تتكرر القيم ويمكن أن تشير مفاتيح متعددة إلى نفس القيمة.

![a dictionary](static/dict.png)

يوجد قاموس بثلاثة مفاتيح، ولكل منها قيمة:

```pycon
>>> me = {'name': 'Marketa', 'city': 'Prague', 'numbers': [20, 8]}
```

لاحظ الأقواس المعقوفة `{}` والنقطتين الرأسيتين `:` بين كل مفتاح وقيمة.
يتم فصل أزواج المفتاح/القيمة بفواصل `,`.

> [note]
> **هل القواميس مرتبة؟**
> ابتداءً من [Python 3.7](https://docs.python.org/3/whatsnew/3.7.html)
> رسميًا (وعمليًا منذ
> [Python 3.6](https://docs.python.org/3/whatsnew/3.6.html#new-dict-implementation))
> أصبحت القواميس تضمن الحفاظ على ترتيب أزواج المفتاح/القيمة بحسب ترتيب إدخالها.  
> قبل ذلك، لم يكن هناك ضمان لترتيب القيم، وهو ما قد تجده مذكورًا في بعض الكتب القديمة.


يمكنك الحصول على القيم من القاموس بطريقة مشابهة للقوائم، ولكن بدلاً من استخدام الفهرس، عليك استخدام المفتاح.

```pycon
>>> me['name']
'Marketa'
```

إذا حاولت الوصول إلى مفتاح غير موجود، بايثون لن تقبل بذلك:

```pycon
>>> me['age']
Traceback (most recent call last):
  File "<stdin>", line 1, in &lt;module&gt;
KeyError: 'age'
```

يمكنك تغيير قيم المفاتيح:

```pycon
>>> me['numbers'] = [20, 8, 42]
>>> me
{'name': 'Marketa', 'city': 'Prague', 'numbers': [20, 8, 42]}
```

... أو إضافة مفاتيح وقيم:

```pycon
>>> me['language'] = 'Python'
>>> me
{'name': 'Marketa', 'city': 'Prague', 'numbers': [20, 8, 42], 'language': 'Python'}
```

... أو حذف مفاتيح وقيم باستخدام الأمر `del` (نفس الأمر المستخدم للقوائم):

```pycon
>>> del me['numbers']
>>> me
{'name': 'Marketa', 'city': 'Prague', 'language': 'Python'}
```

تحتوي القواميس في بايثون على عدد من الطرق المفيدة التي يجدر معرفتها.

إحدى هذه الطرق هي طريقة `get` التي تسمح لك بالحصول على قيمة لمفتاح عندما يكون المفتاح موجودًا أو إرجاع قيمة افتراضية عندما لا يكون موجودًا:

```pycon
>>> record.get('name') # key exits and value is returned
'Peggy'
>>> record.get('age') # key does not exist and None is returned instead
>>> record.get('age', 'n/a') # key does not exist and 'n/a' is returned instead
'n/a'
```

طريقة أخرى مفيدة هي `pop`، والتي تزيل مفتاحًا من القاموس وتعيد قيمته. يُنتج `pop` خطأً في حالة عدم وجود قيمة، إلا إذا تم توفير قيمة افتراضية:

```pycon
>>> record.pop('name') # 'name' is removed from dictionary
'Peggy'

>>> record.pop('name')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'name'

>>> record.pop('name', None)  # None is returned

>>> record.pop('name', 'n/a') # 'n/a' is returned
```

تقوم طريقة `update` بتحديث قاموس من قاموس آخر (تعيد كتابة الموجود وتضيف مفاتيح جديدة):

```pycon
>>> record
{'city': 'Prague', 'name': 'Lucy'}

>>> record.update({'name': 'Peggy', 'hobby': 'Python programming'})
'Lucy'

>>> record
{'city': 'Prague', 'name': 'Peggy', 'hobby': 'Python programming'}

```

## جدول البحث

أحد استخدامات القواميس بخلاف تجميع البيانات هو ما يسمى بـ
*جدول البحث*.
يخزن قيمًا من نفس النوع.

هذا مفيد على سبيل المثال مع دليل الهاتف.
لكل اسم يوجد رقم هاتف واحد.
أمثلة أخرى هي قواميس تحتوي على خصائص الطعام، أو ترجمات الكلمات.


```python
phones = {
    'Tyna': '153 85283',
    'Lubo': '237 26505',
    'Andreea': '385 11223',
    'Fabian': '491 88047',
    'Vitoria': '491 88047',
    'Oliwia': '491 88047',
}

colours = {
    'pear': 'green',
    'apple': 'red',
    'melon': 'green',
    'plum': 'purple',
    'radish': 'red',
    'cabbage': 'green',
    'carrot': 'orange',
}
```

قم بتحديث رقم لوبو ليكون مطابقًا لرقم فابيان حيث أنهما يتشاركان الهواتف مؤقتًا الآن.

{% filter solution %}
```python
phones["Lubo"] = phones["Fabian"]
print(phones)
```
{% endfilter %}

## التكرار (Iteration)

عند المرور عبر قاموس باستخدام `for`، ستحصل على المفاتيح فقط:

```pycon
>>> func_descript = {'len': 'length', 'str': 'string', 'dict': 'dictionary'}
>>> for key in func_descript:
...     print(key)
str
dict
len
```

إذا كنت ترغب في الوصول إلى القيم، فسيتعين عليك استخدام طريقة `values`:

```pycon
>>> for value in func_descript.values():
...     print(value)
string
dictionary
length
```

ولكن في معظم الحالات، ستحتاج إلى كليهما - المفاتيح والقيم.
لهذا الغرض، تحتوي القواميس على طريقة `items`.

```pycon
>>> for key, value in func_descript.items():
...     print('{}: {}'.format(key, value))
str: string
dict: dictionary
len: length
```

> [note]
> توجد أيضًا طريقة `()keys` التي تُرجع المفاتيح فقط.
>
> تُرجع `()keys` و `()values` و `()items` كائنات خاصة (objects)
> يمكن استخدامها في حلقات `for` (نقول أن هذه الكائنات "قابلة للتكرار")،
> وتتصرف كمجموعة.
> هذا موصوف جيدًا في [الوثائق](https://docs.python.org/3/library/stdtypes.html#dictionary-view-objects).

في حلقة `for`، لا يمكنك إضافة مفاتيح إلى قاموس ولا حذفها:

```pycon
>>> for key, value in func_descript.items():
...     func_descript[key.upper()] = value.upper()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
RuntimeError: dictionary changed size during iteration

>>> for key in func_descript:
...     del func_descript[key]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
RuntimeError: dictionary changed size during iteration
```

يمكن التغلب على هذا القيد بسهولة عن طريق استخدام نسخة من عنصر التكرار:

```pycon
>>> for key, value in list(func_descript.items()):
...     func_descript[key.upper()] = value.upper()
>>> func_descript
{'len': 'length', 'str': 'string', 'dict': 'dictionary', 'LEN': 'LENGTH', 'STR': 'STRING', 'DICT': 'DICTIONARY'}

>>> for key in list(func_descript):
...     del func_descript[key]
>>> func_descript
{}
```

ومع ذلك، يمكنك تغيير قيم المفاتيح الموجودة بالفعل.

قم بتحديث قاموس `phones` بحيث تحتوي جميع الأرقام على '+43'.

{% filter solution %}
```python
for person in phones:
    phones[person] = f'+43{phones[person]}'
print(phones)
```
{% endfilter %}


باستخدام حلقة `for`، تأكد من حذف `keys_to_delete` التالية من قاموس `phones`..

```python
keys_to_delete = ['Lubo', 'Tyna', 'Oliwia']
```

{% filter solution %}
```python
for to_delete in keys_to_delete:
    # need to check if is present - cannot delete a key which does not exist in dictionary
    if to_delete in phones.keys(): # or to_delete in phones:
        del phones[to_delete]
print(phones)
```
{% endfilter %}


## كيفية إنشاء قاموس

يمكن إنشاء القواميس بطريقتين.
تستخدم الطريقة الأولى الأقواس المعقوفة `{}`.
الطريقة الأخرى هي باستخدام الكلمة الأساسية `dict`.
يعمل هذا بشكل مشابه لـ `str` أو `int` أو `list`، لذا سيقوم
بتحويل بعض الكائنات المحددة إلى قاموس.

```pycon
>>> {}  # empty dictionary
{}
```

```pycon
>>> dict()  # empty dictionary
{}
```

```python
colours = {
    'pear': 'green',
    'apple': 'red',
    'melon': 'green',
    'plum': 'purple',
    'radish': 'red',
    'cabbage': 'green',
    'carrot': 'orange',
}
```

يمكنك ملء قاموس جديد من قاموس واحد أو أكثر من القواميس الموجودة:
```python
new_colours = {
    **colours,          # ** unpacks dictionary into key-value pairs
    'celery': 'green',
    'squash': 'yellow',
    'plum': 'purple',
}
```

من الممكن تحويل قاموس إلى *قاموس آخر*.
لن يكون هذا القاموس الجديد مرتبطًا بالقاموس
القديم بأي شكل من الأشكال.

```python
colour_riped = dict(colours)
for key in colour_riped:
    colour_riped[key] = 'blackish-brownish-' + colour_riped[key]
print(colours['apple'])
print(colour_riped['apple'])
```

يمكننا أيضًا تحويل تسلسل من *الأزواج* (على سبيل المثال، قائمة من الصفوف)
(التي تعمل كـ *مفتاح* و *قيمة*) إلى قاموس:

```pycon
>>> data = [(1, 'one'), (2, 'two'), (3, 'three')]
>>> dict(data)
{1: 'one', 2: 'two', 3: 'three'}

>>> data = [[1, 'one'], [2, 'two'], [3, 'three']]
>>> dict(data)
{1: 'one', 2: 'two', 3: 'three'}
```


## القواميس ومعاملات الكلمات المفتاحية للدالة - `*args` `**kwargs`

يسمح لك `*args` و `**kwargs` بتمرير وسائط متعددة أو وسائط كلمات مفتاحية إلى دالة.

إذا كنت لا تعرف عدد الوسائط التي سيتم تمريرها إلى الدالة، أو إذا كنت لا تهتم حقًا،
فأضف `*` قبل اسم المعامل في تعريف الدالة.

يسمح لنا `**kwargs` بتمرير عدد متغير من وسائط الكلمات المفتاحية إلى دالة بايثون.
في الدالة، نستخدم علامة النجمتين المزدوجتين قبل اسم المعامل للدلالة على هذا النوع من الوسائط.

يتم تجميع `args` في دالة دائمًا كصفوف، بينما يتم تجميع `kwargs` كقواميس.


```pycon
>>> def test(*args, **kwargs):
...     print("args:", args)
...     print("kwargs:", kwargs)

>>> test(1, 2, 3, a="Hi Bob!", b=True)
args: (1, 2, 3)
kwargs: {'a': 'Hi Bob!', 'b': True}
```

مثال على الاستخدام الواقعي لـ `*args` يمكن أن يكون على سبيل المثال:

```pycon
>>> def my_sum(*args):
...     result = 0
...     for x in args:
...         result += x
...     return result

>>> print(my_sum(1, 2, 3))
6
```

## تمرين

لدينا هذا القاموس الذي يحتوي على معلومات الوصول إلى الكمبيوتر لمستخدمين اثنين وجدول بحث آخر يحتوي على معلومات المدن.
```python
users = {
  'aeinstein': {
    'first': 'albert',
    'last': 'einstein',
    'location': 'princeton',
    'email': 'albgenious1@princeton.org',
  },
  'mcurie': {
    'first': 'marie',
    'last': 'curie',
    'location': 'paris',
  },
}

cities = {
  'paris': {
    'country': 'France',
    'population': 2161,
  },
  'london': {
    'country': 'Great Britain',
    'population': 8960,
  },
  'princeton': {
    'country': 'United States of America',
    'population': 28,
  }
}
```
اطبع المعلومات التالية عن كل مستخدم إذا كانت متوفرة لديه:
`'اسم المستخدم'`، `'الاسم الكامل'` (الاسم الأول والأخير مع كتابة الحرف الأول كبيرًا)، `'البريد الإلكتروني'`، `'المدينة'` التي يعيش فيها و `'الدولة'` التي يعيش فيها.

{% filter solution %}
```python
for username, properties in users.items():
    fullname = f'{properties["first"][0].upper()}{properties["first"][1:]} {properties["last"][0].upper()}{properties["last"][1:]}'
    # or properties["first"].capitalize()
    if "email" in properties:
        email = properties["email"]
    else:
        email = None
    city = properties["location"]
    if properties["location"] in cities:
        country = cities[properties["location"]]["country"]
    else:
        country = None
    print(f'''
    User with username: "{username}"
    is named: "{fullname}",
    has email: "{email}",
    lives in "{city}",
    which is located in "{country}"
    ''')
```
{% endfilter %}


## وهذا كل شيء الآن

إذا كنت ترغب في معرفة جميع الحيل
حول القواميس، يمكنك إلقاء نظرة على [ورقة الغش](https://github.com/ehmatthes/pcc/releases/download/v1.0.0/beginners_python_cheat_sheet_pcc_dictionaries.pdf).

إذا كنت ترغب في إزالة الغموض عن `*args` و `**kwargs` وتعلم المزيد مما يمكننا تضمينه في المحاضرة، فألق نظرة [هنا](https://realpython.com/python-kwargs-and-args/).

يمكن العثور على وصف كامل هنا في
[وثائق](https://docs.python.org/3/library/stdtypes.html#mapping-types-dict) بايثون.

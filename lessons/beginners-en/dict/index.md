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
> توجد أيضًا طريقة `keys()` التي تُرجع المفاتيح فقط.
>
> تُرجع `keys()` و `values()` و `items()` كائنات خاصة
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

You can fill a new dictionary from one or more existing ones:
```python
new_colours = {
    **colours,          # ** unpacks dictionary into key-value pairs
    'celery': 'green',
    'squash': 'yellow',
    'plum': 'purple',
}
```

It is possible to convert a dictionary into *another dictionary*.
This new dictionary won't be in any way connected to the
old one.

```python
colour_riped = dict(colours)
for key in colour_riped:
    colour_riped[key] = 'blackish-brownish-' + colour_riped[key]
print(colours['apple'])
print(colour_riped['apple'])
```

We can also convert a sequence of *pairs* (e.g., list of tuples)
(which work as *key* and *value*) into a dictionary:

```pycon
>>> data = [(1, 'one'), (2, 'two'), (3, 'three')]
>>> dict(data)
{1: 'one', 2: 'two', 3: 'three'}

>>> data = [[1, 'one'], [2, 'two'], [3, 'three']]
>>> dict(data)
{1: 'one', 2: 'two', 3: 'three'}
```


## Dictionaries and function keyword arguments - *args **kwargs

`*args` and `**kwargs` allow you to pass multiple arguments or keyword arguments to a function.

If you do not know how many arguments will be passed into your function, or you do not really care,
add a `*` before the parameter name in the function definition.

`**kwargs` allows us to pass a variable number of keyword arguments to a Python function.
In the function, we use the double-asterisk before the parameter name to denote this type of argument.

`args` are collected in a function always as tuples, while `kwargs` are collected as dictionaries.


```pycon
>>> def test(*args, **kwargs):
...     print("args:", args)
...     print("kwargs:", kwargs)

>>> test(1, 2, 3, a="Hi Bob!", b=True)
args: (1, 2, 3)
kwargs: {'a': 'Hi Bob!', 'b': True}
```

Example of real-life usage of `*args` could be for example:

```pycon
>>> def my_sum(*args):
...     result = 0
...     for x in args:
...         result += x
...     return result

>>> print(my_sum(1, 2, 3))
6
```

## Exercise

We have this dictionary of computer access information of two users and another lookup table with cities information.
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
Print out following information about each user if they have it:
Their `'username'`, `'full name'` (first and last with first letter capitalized), `'email'`, `'city'` they live in and `'country'` they live in.

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


## And that's all for now

If you would like to know all the tricks
about dictionaries you can look at the [cheatsheet](https://github.com/ehmatthes/pcc/releases/download/v1.0.0/beginners_python_cheat_sheet_pcc_dictionaries.pdf).

If you want to demystify the `*args` and `**kwargs` and learn more than we could fit in the lecture, have a look [here](https://realpython.com/python-kwargs-and-args/).

A complete description can be found here in the
Python [documentation](https://docs.python.org/3/library/stdtypes.html#mapping-types-dict).

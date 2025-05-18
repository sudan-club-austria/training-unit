# JSON

هناك أيضًا لغات برمجة (programming languages) أخرى غير بايثون.

لا يمكن للغات الأخرى العمل مع كود بايثون.
إذا كنت ترغب في "التحدث" مع هذه البرامج -
تزويدها ببعض معلومات المعالجة
أو للحصول على نتائج منها -
عليك تمرير المعلومات في شكل مبسط.


## الأنواع (Types)

معظم لغات البرمجة لديها بعض الأرقام، وبعض أنواع القوائم،
مجموعة متنوعة من النصوص وبعض الاختلافات في القواميس
(أو عدة طرق لإنشاء القواميس).
ولديهم طريقة لكتابة `True` و `False` و `None`.

عادة ما تكون هذه الأنواع الأساسية كافية لنقل المعلومات
في شكل مقروء، على الرغم من عدم وجود مكافئات دقيقة في جميع اللغات
(لدى بايثون نوعان أساسيان من الأرقام - `int` و `float`).
لذلك سنركز عليها.


## ترميز البيانات (Data encoding)

مشكلة أخرى هي نقل البيانات:
حتى تتمكن من كتابة البيانات على القرص أو نقلها
عبر الإنترنت، يجب تحويلها إلى تسلسل من *بايتات* (bytes) (أرقام من 0 إلى 255).
بتبسيط: عليك تحويلها إلى نص (string).

هناك الكثير من الطرق لترميز البيانات إلى نص.
تحاول كل طريقة إيجاد التوازن الصحيح بين
سهولة القراءة للأشخاص/الحواسيب، وطول السجل،
الأمان والخيارات وقابلية التوسع.
نحن نعرف بالفعل بناء الجملة الخاص ببايثون:

```python
{
    'name': 'Ali',
    'city': 'Omdurman',
    'languages': ['Arabic', 'English', 'Python'],
    'age': 29,
}
```

طريقة أخرى لكتابة البيانات هي [YAML](http://www.yaml.org/):

```yaml
name: Ali
city: Omdurman
languages:
   - Arabic
   - English
   - Python
age: 29
```

أخيرًا، هناك أيضًا [JSON](http://json.org/)
(Javascript Object Notation)،
والذي، لبساطته، انتشر بشكل كبير:

```json
{
  "Name": "Ali",
  "City": "Omdurman",
  "Languages": ["Arabic", "English", "Python"],
  "Age": 29
}
```

> [note]
> ضع في اعتبارك أنه على الرغم من أن JSON يبدو مشابهًا للكود
> في بايثون، إلا أنه تنسيق آخر له قواعده الخاصة.
> لا تخلط بينهما!
>
> في البداية لا أوصي بكتابة JSON يدويًا؛
> دع الحاسوب يقرر مكان كتابة
> الفواصل وعلامات الاقتباس.

## JSON في بايثون (JSON in Python)

ترميز الكائنات في JSON بسيط: هناك وحدة (module) `json`،
التي تسترد طريقتها `loads` البيانات من النص:

```python
import json

json_string = """
    {
      "name": "Ali",
      "city": "Omdurman",
      "languages": ["Arabic", "English", "Python"],
      "age": 29
    }
"""

data = json.loads(json_string)
print(data)
print(data['city'])
```

ثم هناك طريقة `dumps`، التي تفك ترميز البيانات المعطاة
وتُرجع نصًا (string).

النص الذي تُرجعه `dumps(data)` مناسب للحاسوب
المعالجة.
إذا كنت ترغب في قراءته، فمن الأفضل تعيين `ensure_ascii = False`
(بحيث لا يتم ترميز الأحرف المشددة بـ `\`)
و `indent = 2` (مسافة بادئة بمسافتين).

```pycon
>>> print(json.dumps(data, ensure_ascii = False, indent = 2))
{
  "name": "Ali",
  "city": "Omdurman",
  "languages": [
    "Arabic",
    "English",
    "Python"
  ],
  "age": 29
}
```
## تمرين (Exercise)

اكتب كودًا لطباعة قيمة راتب حسن الكلي  (المرتب بالاضافة للنثرية bonus) من نص JSON التالي.

حاول ألا تعتمد على حقيقة أن ترتيب حسن هو الأول في القائمة)


```python
sampleJson = """{
  "company":{
    "employees":[
      {
        "name":"Hassan",
        "payable":{
          "salary":7000,
          "bonus":800
        }
      },
      {
        "name":"Fatima",
        "payable":{
          "salary":5500,
          "bonus":1000
        }
      }
    ]
  }
}"""
```

{% filter solution %}
```python
import json

sampleJson = """{
  "company":{
    "employees":[
      {
        "name":"Hassan",
        "payable":{
          "salary":7000,
          "bonus":800
        }
      },
      {
        "name":"Fatima",
        "payable":{
          "salary":5500,
          "bonus":1000
        }
      }
    ]
  }
}"""
content = json.loads(sampleJson)
employees = content.get("company", {}).get("employees", [])
for employee in employees:
    name = employee.get('name')
    if name == "Hassan":
      payable = employee.get("payable", {})
      total = payable.get("salary", 0) + payable.get("bonus", 0)
      print(f"{name} has a total salary with bonus: {total}")
```
{% endfilter %}


وصف كامل لوحدة `json` -
بما في ذلك دوال الكتابة/القراءة مباشرة إلى/من الملفات -
موجود في [الرابط](https://docs.python.org/3/library/json.html).
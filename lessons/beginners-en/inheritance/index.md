# الوراثة (Inheritance)

نعرف بالفعل ما هي الفئات (classes)، وقد رأينا الفئة (class) للقطط الصغيرة
كمثال:

```python
class Kittie:
    def __init__(self, name):
        self.name = name

    def meow(self):
        print("{}: Meow!".format(self.name))

    def eat(self, food):
        print("{}: Meow meow! I like {} very much!".format(self.name, food))
```

الآن قم بإنشاء فئة (class) مماثلة للكلاب:

```python
class Doggie:
    def __init__(self, name):
        self.name = name

    def woof(self):
        print("{}: Woof!".format(self.name))

    def eat(self, food):
        print("{}: Woof woof! I like {} very much!".format(self.name, food))
```

معظم الكود هو نفسه!
إذا كان عليك كتابة فئة (class) للكتاكيت والبط والأرانب،
ستكون مهمة مملة للغاية بدون Ctrl+C.
ولأن المبرمجين كسالى لكتابة نفس الجزء من
الكود عدة مرات (والأهم من ذلك صيانته)، فقد أنشأوا
آلية لتجنب ذلك. كيف؟

القطط الصغيرة والكلاب حيوانات (animals).
لذا يمكنك إنشاء فئة (class) لجميع الحيوانات (animals)، وكتابة
كل ما ينطبق على جميع الحيوانات فيه.
وفي الفئات (classes) الخاصة بكل حيوان، يمكنك فقط
كتابة التفاصيل.
هذه هي الطريقة التي تتم بها الأمور في بايثون:

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def eat(self, food):
        print("{}: I like {} very much!".format(self.name, food))


class Kittie(Animal):
    def meow(self):
        print("{}: Meow!".format(self.name))


class Doggie(Animal):
    def woof(self):
        print("{}: Woof!".format(self.name))


smokey = Kittie('Smokey')
doggo = Doggie('Doggo')
smokey.meow()
doggo.woof()
smokey.eat('mouse')
doggo.eat('bone')
```

كيف يعمل هذا؟
باستخدام الأمر `class Kittie(Animal)` أنت
تخبر بايثون أن الفئة (class) `Kittie` *ترث* (inherits)
سلوكًا من الفئة (class) `Animal`.
في لغات البرمجة الأخرى يقولون
أن `Kittie` *مشتق من* (derived from) `Animal`
أو أنه *يمتد* (extends) `Animal`.
تسمى الفئات المشتقة (derived classes) *فئات فرعية* (subclasses) والفئة الرئيسية
هي *فئة أساسية* (superclass).

عندما تبحث بايثون عن طريقة/دالة (method/function) (أو سمة أخرى - attribute)،
على سبيل المثال `smokey(eat)`، ولم تجدها في الفئة نفسها
ستبحث في الفئة الأساسية (superclass). لذا فإن كل ما تم
تعريفه لـ Animal ينطبق على Kittie (إلا إذا
أخبرت بايثون بخلاف ذلك).


## تجاوز الطرق و `super()` (Overwriting methods and `super()`)

إذا لم يعجبك بعض سلوك الفئة الأساسية (superclass)، يمكنك
تعريف طريقة (method) بنفس الاسم في الفئة الفرعية (subclass):

```python
class Kittie(Animal):
    def eat(self, food):
        print("{}: I don't like {} at all!".format(self.name, food))


smokey = Kittie('Smokey')
smokey.eat('dry food')
```

> [python]
> إنه مشابه لما فعلناه في الدرس السابق مع
> `misty.meow = 12345`. تبحث بايثون عن السمات (attributes) في الكائن (object)،
> ثم في الفئة (class)، ثم في الفئة الأساسية (superclass) (ثم في الفئة الأساسية للفئة الأساسية).

في بعض الأحيان قد تحتاج إلى بعض السلوك من الطريقة الأصلية
في الطريقة المتجاوزة (overwritten method). يمكنك استدعائها باستخدام الدالة الخاصة  `()super`،
التي تسمح باستدعاء الطرق (methods) في فئة أساسية (superclass).

```python
class Kittie(Animal):
    def eat(self, food):
        print("({} is looking at {} for a while)".format(self.name, food))
        super().eat(food)

smokey = Kittie('Smokey')
smokey.eat('dry food')
```

ضع في اعتبارك أنه يجب عليك تمرير كل ما تحتاجه طريقة  `()super` هذه
(بصرف النظر عن `self`، الذي يتم تمريره تلقائيًا).
يمكنك استخدام هذا - يمكنك تمرير قيم مختلفة
عما تلقته الدالة الأصلية (في هذه الحالة، فئة `snake` سيتلقى
الاسم `Stanley`، لكنك تريد تغييره إلى `Ssstanley`):

```python
class snake(Animal):
    def __init__(self, name):
        name = name.replace('s', 'sss')
        name = name.replace('S', 'Sss')
        super().__init__(name)


stanley = snake('Stanley')
stanley.eat('mouse')
```

كما ترى، يمكنك استخدام  `()super` حتى مع الطرق الخاصة
مثل `__init__`.


## تعدد الأشكال (Polymorphism)

لم يخترع المبرمجون الوراثة (inheritance) لمجرد أنهم كسالى
لكتابة نفس الكود عدة مرات. هذا بالطبع سبب وجيه،
لكن الفئات الأساسية (superclasses) لها أيضًا ميزة أخرى
مهمة: عندما نعلم أن `Kittie` و `Doggie`
وأي فئة مشابهة أخرى هي حيوانات (animals)، يمكننا إنشاء قائمة
من الحيوانات (animals)، لكننا لا نهتم بنوع هذه الحيوانات
تحديدًا:

{# XXX: last 4 lines are new and should be highlighted #}
```python
class Animal:
    def __init__(self, name):
        self.name = name

    def eat(self, food):
        print("{}: I like {} very much!".format(self.name, food))


class Kittie(Animal):
    def meow(self):
        print("{}: Meow!".format(self.name))


class Doggie(Animal):
    def woof(self):
        print("{}: Woof!".format(self.name))

animals = [Kittie('Smokey'), Doggie('Doggo')]

for animal in animals:
    animal.eat('meat')
```

هذا سلوك مهم جدًا للفئات الفرعية (subclasses):
عندما يكون لديك `Kittie`، يمكنك استخدامه في أي مكان
حيث يتوقع البرنامج `Animal`، لأن كل قطة صغيرة
*هي* حيوان (animal).

> [note]
> هذا نهج جيد عندما لا تعرف أي فئة يجب أن تكون
> موروثة في أي فئة.
> كل *قطة صغيرة* (kittie) أو *كلب صغير* (doggie) هو *حيوان* (animal)،
> كل *كوخ* (cabin) أو *منزل* (house) هو *مبنى* (building).
> في هذه الأمثلة، يكون التوريث منطقيًا.
>
> ولكن في بعض الأحيان يفشل نهجنا - على سبيل المثال إذا قلنا
> كل *سيارة* (car) هي *عجلة قيادة* (steering wheel)، فإننا نعلم أن
> لا ينبغي لنا استخدام الوراثة (inheritance).
> حتى لو كان بإمكاننا "تدوير" كل من السيارات وعجلات القيادة، فهذا يعني شيئًا مختلفًا،
> وبالتأكيد لا يمكننا استخدام السيارات في كل مكان نرغب فيه
> استخدام عجلات القيادة. لذا في هذه الحالة يجب أن نقول لأنفسنا:
> كل قطة صغيرة (kittie) *لديها* اسم وكل سيارة (car) *لديها* عجلة قيادة (steering wheel)، لذا يجب علينا
> إنشاء فئتين مختلفتين، وفي فئة السيارة، نقوم
> باستخدام عجلة القيادة كمتغير افتراضي:
>
> ```python
> class Car:
>     def __init__(self):
>         self.wheel = Wheel()
> ```
>
> (وعندما يغضب منك بعض المبرمجين لأنك
> تخرق [مبدأ ليسكوف للاستبدال](https://en.wikipedia.org/wiki/Liskov_substitution_principle)
> فذلك بسبب هذه المشكلة.)

## التعميم (Generalization)

عندما تنظر إلى الدوال (functions) `meow` و `woof`، ربما ستكتشف
أنه يمكن تسميتها بشكل أفضل، بحيث يمكن استخدامها لكل حيوان، بشكل مشابه
لـ `eat`.

{# XXX: Every instance of "speak" should be highlighted #}
```python
class Animal:
    def __init__(self, name):
        self.name = name

    def eat(self, food):
        print("{}: I like {} very much!".format(self.name, food))


class Kittie(Animal):
    def speak(self):
        print("{}: Meow!".format(self.name))


class Doggie(Animal):
    def speak(self):
        print("{}: Woof!".format(self.name))

animals = [Kittie('Smokey'), Doggie('Doggo')]

for animal in animals:
    animal.speak()
    animal.eat('meat')
```

كما يوضح هذا المثال، فإن كتابة فئات أساسية (superclasses) يمكننا من خلالها بسهولة توريث
الطرق (methods) ليس بالأمر السهل. ليس الأمر سهلاً بالتأكيد عندما نريد إنشاء
فئة فرعية (subclass) في برنامج مختلف عن البرنامج الذي يوجد فيه الفئة الأساسية (superclass).
لذا لهذا السبب يجب عليك توريث الفئات (classes) داخل التعليمات البرمجية الخاصة بك:
لا نوصي بتوريث الفئات (classes) التي كتبها شخص آخر،
إلا إذا ذكر مؤلف الفئة الأساسية (superclass) صراحةً (وبشكل أساسي كيف) يمكنك التوريث من فئته.

وهذا كل شيء عن الفئات (classes) الآن. أنت الآن تعرف ما يكفي لإنشاء
حديقة الحيوانات الخاصة بك :)
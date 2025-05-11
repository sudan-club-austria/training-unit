## الاختبارات السلبية (Negative tests)

تسمى الاختبارات التي تتحقق من أن البرنامج يعمل بشكل صحيح
في ظل ظروف صحيحة *الاختبارات الإيجابية* (positive tests).
يؤدي الاستثناء الذي يتم رفعه أثناء الاختبار الإيجابي إلى فشل الاختبار.

تسمى الاختبارات التي تتحقق من السلوك للإدخالات غير الصالحة *الاختبارات السلبية* (negative tests).
الغرض من الاختبار السلبي هو التحقق من المعالجة السليمة
لحالات الخطأ. غالبًا ما يكون رفع استثناء هو السلوك المتوقع
للتعليمات البرمجية المختبرة.

على سبيل المثال، يجب أن تثير الدالة `computer_move` خطأً
(على سبيل المثال، `ValueError`) عندما تكون اللوحة ممتلئة.

> [note]
> من الأفضل بكثير رفع استثناء بدلاً من عدم فعل أي شيء
> والسماح للبرنامج بالتعثر في مكان آخر بصمت.
> يمكنك استخدام مثل هذه الدالة في برنامج أكثر تعقيدًا
> وتأكد من أنها سترفع خطأً مفهوماً
> عند استدعائها في ظروف سيئة.
> يساعدك الخطأ في إصلاح المشكلة الفعلية. كلما اكتشفت
> خطأً مبكرًا، كان إصلاحه أسهل.

استخدم عبارة `with` والدالة `raises`
لاختبار ما إذا كان الكود الخاص بك يثير الاستثناء المتوقع.
يتم استيراد الدالة `raises` من وحدة `pytest`.


> [note]
> لم نتحدث بعد عن عبارة `with` ومديري السياق (context managers).
> لكن لا تقلق، ستتعلم عنها لاحقًا. فقط تحقق من كيفية استخدامها
> لاختبار ما إذا كان يتم رفع استثناء.

```python
import pytest

import tic_tac_toe

def test_move_failure():
    with pytest.raises(ValueError):
        tic_tac_toe.computer_move('oxoxoxoxoxoxoxoxoxox')
```

هيا نحاول الآن تعديل الدالة الخاصة بالحصول على محيط المستطيل
بحيث تثير ValueError إذا كان أي من الجانبين أصغر من أو يساوي الصفر.
أضف اختبارًا للوظيفة الجديدة.


{% filter solution %}

```python
import pytest

def find_rectangle_perimeter(width, height):
    """ Calculate perimeter of a rectangle from the given sides.
    """
    if width < 0 or height < 0:
        raise ValueError("Rectangle sides must be non-negative.")
    return  2 * (width + height)

def test_find_perimeter_exception_negative():
    """ Tests of negative integer values as input
    """
    with pytest.raises(ValueError):
        find_rectangle_perimeter(-3, 5)
```
{% endfilter %}

## تجهيزات Pytest (Pytest fixtures)

``Fixtures`` في pytest هي مكونات (component) قابلة لإعادة الاستخدام تقوم بإعداد حالات محددة (مثل اتصالات قاعدة البيانات (database connections)، وبيانات الاختبار(test data)).

### الميزات الرئيسية (Key Features)

* قابلية إعادة الاستخدام (Reusability): عرّف تجهيزًا مرة واحدة واستخدمه عبر العديد من دوال الاختبار.
* تحديد النطاق (Scoping): يمكن تحديد نطاق التجهيزات (متاحة) على مستويات مختلفة مثل الدالة، أو الفئة، أو الوحدة، أو الجلسة.
* التنظيف التلقائي (Automatic Cleanup): يمكن إعداد التجهيزات لتنظيف الموارد تلقائيًا بعد انتهاء الاختبار.
* حقن التبعية (Dependency Injection): يمكن لدوال الاختبار استخدام التجهيزات عن طريق تضمينها كـ وسائط (arguments). (لا يمكن إضافة وسائط "عادية" إلى دوال الاختبار، فقط مراجع للتجهيزات).

يمكنك بسهولة إنشاء واستخدام ``fixture`` في pytest بالطريقة التالية:

```python
import pytest

@pytest.fixture
def sample_data():
    return [1, 2, 3, 4]
def test_sum(sample_data):
    assert sum(sample_data) == 10
```

بشكل افتراضي، يتم استدعاء ``fixture`` مرة واحدة لكل دالة اختبار - معامل ``scope="function"`` للتجهيز.

لأغراض استخدام الموارد، قد يكون من المفيد إنشاء تجهيز مرة واحدة فقط لكل ``وحدة`` (module) كاملة:

```python
import pytest
# A fixture to provide a configuration dictionary
@pytest.fixture(scope="module")
def config_data():
    config = {
        "api_endpoint": "http://api.example.com",
        "retry_attempts": 5,
        "timeout": 10
    }
    return config
# Example test using the fixture
def test_api_endpoint(config_data):
    assert config_data["api_endpoint"] == "http://api.example.com"
# Another test using the same fixture
def test_retry_attempts(config_data):
    assert config_data["retry_attempts"] == 5
```

يكون هذا النهج مفيدًا عندما لا يتضمن الإعداد موارد خارجية تتطلب تنظيفًا صريحًا بعد الاختبارات.
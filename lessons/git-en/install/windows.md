## تثبيت Git على Windows

انتقل إلى [git-scm.org](https://git-scm.com/download/win) ، وقم بتنزيل **Git Standalone Installer 64-bit Git for Windows Setup** وقم بتثبيته.
عند التثبيت ، باستخدام المثبت (wizard) اختر الخيارات التالية:

* Run Git from the Windows Command Prompt
* Checkout Windows-style, commit Unix-style line endings

لا تقم بتغيير أي خيارات أخرى ، يمكن تركها كما هي.
يرجى التأكد من أن خيار **Git Credential Manager Core** ["تم تحديده"](https://github.com/git-ecosystem/git-credential-manager/blob/release/docs/install.md#git-for-windows-star) ، لتثبيت الأداة الإضافية افتراضيًا مع تثبيت Git.

{{ figure( img=static('windows-git-cred-manager.png'), alt='Git installation credential manager allow', ) }}


ثم قم بإعداد محرر(editor) Git الخاص بك.
إذا كان لديك نافذة محطة (terminal) مفتوحة ، فقم بإغلاقها وافتح نافذة جديدة.
(يؤدي التثبيت إلى تغيير إعدادات النظام التي يجب تحميلها مرة أخرى.)

في ال(terminal) الجديد ، أدخل:

```console
> git config --globaﻻشسهؤسl core.editor notepad
> git config --global format.commitMessageColumns 80
> git config --global gui.encoding utf-8
```

الآن تابع بقية الإعدادات في [الإعدادات العامة في تثبيت Git]({{ lesson_url('git-en/install') }}).
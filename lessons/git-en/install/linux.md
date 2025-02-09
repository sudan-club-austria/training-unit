## تثبيت Git على Ubuntu/Debian

```console
sudo apt-get install git nano pass
```

إذا كنت تستخدم توزيعًا آخر ، فإننا نتوقع أنك تعرف بالفعل
كيفية تثبيت البرامج. تابع وقم بتثبيت *git* و *pass* و *nano*.

بعد تثبيت git ، اختر محرر Git الخاص بك.
إذا كنت لا تحب Vim (أو لا تعرف ما هو)
أدخل هذا الأمر لاختيار محرر أكثر سهولة في الاستخدام يسمى Nano:

```console
git config --global core.editor nano
```

بعد هذه الخطوة ، يرجى تثبيت [Git Credential Manager](https://github.com/GitCredentialManager/git-credential-manager) عن طريق تنزيل  **gcm-linux.(version).deb** من [الإصدارات الرسمية لـ gcm](https://github.com/GitCredentialManager/git-credential-manager/releases/latest).

بعد ذلك قم بالتثبيت وضبط الاعدادات باستخدام الأوامر:

```console
sudo dpkg -i <path-to-package>
git-credential-manager-core configure
git config --global credential.credentialStore gpg
```

بعد ذلك ، نحتاج إلى إنشاء مخزن بيانات اعتماد آمن. قم بتشغيل الأمرين التاليين لإنشاء واستخدام زوج مفاتيح GPG جديد

```console
gpg --gen-key
pass init <gpg-id> # حيث <gpg-id> هو اسم المستخدم الذي تم إنشاؤه في الخطوة 1
```

الآن تابع بقية الإعداد في [الإعدادات العامة في تثبيت Git]({{ lesson_url('git-en/install') }}).
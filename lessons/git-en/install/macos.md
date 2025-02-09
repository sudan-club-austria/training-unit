## تثبيت Git على macOS

حاول تشغيل `git` على سطر الأوامر.
إذا كان مثبتًا بالفعل ، فسيُظهر لك كيفية استخدامه.
وإلا ، فقم بتثبيته باستخدام Homebrew:

```console
brew install git
```

لا يزال من الضروري إعداد محرر Git الخاص بك (أدخل `nano` ،
حتى إذا قمت بتثبيت -على سبيل المثال- VS Code ).
يمكنك القيام بذلك باستخدام هذا الأمر:

```console
git config --global core.editor nano
```

بعد ذلك قم بتثبيت وتكوين [Git Credential Manager](https://github.com/git-ecosystem/git-credential-manager/blob/release/docs/install.md#macos) باستخدام الأمر:

```console
brew install --cask git-credential-manager
```

الآن تابع بقية الإعداد في [الإعدادات العامة في تثبيت Git]({{ lesson_url('git-en/install') }}).
# action-translate-readme

* [الإنجليزية](README.md)
* [README.zh-TW المفرد الصينية التقليدية](README.zh-TW.md)
* [README.zh-CN المفرد الصينية المبسطة](README.zh-CN.md)
* [الفرنسية](README.French.md)
* [العربية](README.Arabic.md)


# مقدمة

* نعلم جميعًا أن كتابة توثيق README يمكن أن تستغرق وقتًا طويلاً ، ولكن الآن هناك حل يمكن أن يوفر لك نصف وقتك. هذا هو `action-translate-readme` لدينا.

* ترجم إصدارات اللغات المختلفة لـ README عبر `gpt3.5`.

* تقدم جميع الملفات المترجمة تلقائيًا (commit ، push) من خلال **Github Actions (CI / CD)**.

* على سبيل المثال: عندما تكتب أو تعدل الإصدار الإنجليزي من README ، يتم إنشاء إصدارات مترجمة تلقائيًا ، مثل الصينية التقليدية والصينية المبسطة والفرنسية وغيرها.

ملاحظة: يتم تنفيذ المترجم للإصدار v1 من خلال حزم خارجية على `Linux` ؛ يتم تنفيذ الإصدار v2 من خلال واجهة برمجة تطبيقات openai المجانية المسماة [`g4f`](https://github.com/xtekky/gpt4free)


# كيفية الإستخدام؟

1. انقر على أيقونة :star: لإضافة هذا المشروع إلى مستودع Github الخاص بك.

2. إعداد `Github Token` الخاص بك:

* [قم بإنشاء **`Github Secret Token`** جديد](https://github.com/settings/tokens/new)
  * الإعدادات
  * إعدادات المطور
  * الرموز الشخصية الفردية - `Tokens (classic)`
  * إنشاء رمز مميز جديد
  * اختر النطاقات: `repo` و `workflow`
  * **احتفظ** بالرمز السري الخاص بك (لا تفقده ، ستحتاج إلى لصقه لاحقًا)

  <img src="https://github.com/Lin-jun-xiang/action-translate-readme/assets/63782903/b7487b49-817c-4925-b94a-bdb7b025a0c2" width="60%" />

* إنشاء **`repository secret`** جديد
  * في مستودعك - `الإعدادات`
  * `Security و variables`
  * `Actions`
  * `New repository secret`
  * املأ العلامة بـ `token` واسمه (على سبيل المثال ، `Action_Bot`)

  <img src="https://github.com/Lin-jun-xiang/action-translate-readme/assets/63782903/27dc7bcd-633f-431e-98e8-387b97ecd47c" width="60%" />

3. أنشئ مثال عملك في الدليل `.github/workflows/your_action.yml`. يمكنك فقط نسخ الشفرة التالية:

```
# .github/workflows/translate.yml
اسم: ترجمة Readme

على:
    push:
        branches: ['**']

وظائف:
    ترجمة:
        runs-on: ubuntu-latest
        steps:
            - الاسم: الخروج
              uses: actions/checkout@v3
              with:
                fetch-depth: 3

            - name: Auto Translate
              uses: Lin-jun-xiang/action-translate-readme@v2 # Based on the tag
              with:
                token: ${{ secrets.Action_Bot }} # Based on step2 name
                g4f_provider: g4f.Provider.DeepAi # You can change this provider
                langs: "en,zh-TW,zh-CN,French,Arabic" # You can define any langs
```

يوجد ثلاثة معلمات تستحق الاهتمام الخاص في `.yml`:

* `token`: الرمز المميز الذي تم إنشاؤه في المستودع استنادًا إلى الخطوة 2.
* `g4f_provider`: موفر gpt ، يرجى الرجوع إلى [الرابط](https://github.com/xtekky/gpt4free/tree/main#gpt-35--gpt-4) لمزيد من المعلومات.
* `langs`: إصدارات اللغة التي سيتم إنشاؤها. تأكد من تفريق اللغات المختلفة بـ `,`. على سبيل المثال:
  * `"en"`: ترجمة الإصدار الإنجليزي فقط.
  * `"en,zh-TW"`: ترجمة الإنجليزية والصينية التقليدية.
  * `"French,Arabic"`: ترجمة الفرنسية والعربية.

4. الآن يمكنك تحديث  `README.md` ، وسيتم إنشاء إصدار مترجم تلقائيًا!

---

# نموذج توضيحي

![](./img/auto-translation.gif)

---

# نتائج مستند الاختبارات

* تحقق من [مستند الاختبار](https://github.com/Lin-jun-xiang/vscode-extensions-best/tree/main).
* استخدم أداتنا لتحديث مستند الاختبار.

<a href="#top">العودة للأعلى</a>
--------------------------------
# action-translate-readme

* [英文](README.md)
* [繁体中文README.md](README.zh-TW.md)
* [简体中文README.md](README.zh-CN.md)
* [法文](README.French.md)
* [阿拉伯语](README.Arabic.md)


# 简介

* 我们都知道编写README文档可能耗费大量时间，但现在有一种解决方案可以为您节省一半时间。这就是我们的`action-translate-readme`。

* 通过`gpt3.5`翻译不同语言版本的README。

* 通过 **Github Actions(CI/CD)** 自动提交(提交、推送)翻译的文件。

* 例如：当您**编写**或**修改**README的英文版本时，会自动生成翻译版本，比如繁体中文、简体中文、法语等。

注意：v1版本的翻译器是通过第三方软件包在Linux上实现的；v2版本的翻译器是通过名为[`g4f`](https://github.com/xtekky/gpt4free)的免费的openai api实现的。


# 如何使用？

1. 点击 :star: 图标将此项目添加到您的Gihub存储库中。

2. 配置您的`Github Token`：

* [创建一个新的**`Github秘密令牌`**](https://github.com/settings/tokens/new)
  * 设置
  * 开发者设置
  * 个人访问令牌 - `Tokens(classic)`
  * 生成一个新令牌
  * 选择范围: `repo` 和 `workflow`
  * **保存**您的秘密令牌(不要丢失它，您需要粘贴它)

  <img src="https://github.com/Lin-jun-xiang/action-translate-readme/assets/63782903/b7487b49-817c-4925-b94a-bdb7b025a0c2" width=" 60%" />

* 创建一个新的 **`存储库秘密`**
  * 在您的存储库中 - `设置`
  * `安全和变量`
  * `操作`
  * `新的存储库秘密`
  * 用`token`填写标签并命名(例如`Action_Bot`)

  <img src="https://github.com/Lin-jun-xiang/action-translate-readme/assets/63782903/27dc7bcd-633f-431e-98e8-387b97ecd47c" width=" 60%" />

3. 在目录`.github/workflows/your_action.yml`中创建您的操作示例。您只需复制以下代码：

```
# .github/workflows/translate.yml
name: Translate Readme

on:
    push:
        branches: ['**']

jobs:
    translate:
        runs-on: ubuntu-latest
        steps:
            - name: Checkout
              uses: actions/checkout@v3
              with:
                fetch-depth: 3

            - name: Auto Translate
              uses: Lin-jun-xiang/action-translate-readme@v2 # 基于标签
              with:
                token: ${{ secrets.Action_Bot }} # 基于步骤2的名称
                g4f_provider: g4f.Provider.DeepAi # 您可以更改此提供者
                langs: "en,zh-TW,zh-CN,French,Arabic" # 您可以定义任何语言版本
```

在 `.yml` 中需要特别注意的三个参数：

* `token`: 在第2步中在repo中创建的token。
* `g4f_provider`: gpt的提供者，请参见此[链接](https://github.com/xtekky/gpt4free/tree/main#gpt-35--gpt-4)了解更多信息。
* `langs`: 要生成的语言版本。一定要使用`,`分隔不同的语言。例如:
  * `"en"`：仅翻译英语版本。
  * `"en,zh-TW"`：翻译英语和繁体中文。
  * `"French,Arabic"`：翻译法语和阿拉伯语。

4.  现在您可以更新`README.md`，它将自动生成一个翻译版本! 

---

# 演示

![](./img/auto-translation.gif)

---

# 测试文档的结果

* 查看[test document](https://github.com/Lin-jun-xiang/vscode-extensions-best/tree/main)。
* 使用我们的工具更新测试文件。

<a href="#top">回到页首</a>
--------------------------------
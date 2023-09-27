# action-translate-readme

* [English](README.md)
* [Traditional Chinese README.md](README.zh-TW.md)
* [Simplified Chinese README.md](README.zh-CN.md)
* [French](README.French.md)
* [Arabic](README.Arabic.md)


# 介紹

* 我們都知道編寫 README 文檔可能很耗時間，但現在有一個可以節省時間的解決方案——`action-translate-readme`.

* 通過 `gpt3.5` 翻譯不同語言版本的 README。

* 通過 **Github Actions (CI/CD)** 自動提交（commit,push）翻譯文件。

* 例如：當你 **編寫** 或 **修改** 英文版的 README 文件時，自動生成翻譯版本，如繁體中文、簡體中文、法文等。

注意：v1 版本的翻譯器是在 `Linux` 上通過第三方軟件包實現的；v2 版本是通過名為 [`g4f`](https://github.com/xtekky/gpt4free) 的免費 openai api 實現的。

# 如何使用？

1. 點擊 :star: 標誌將此項目添加到您的 Github 存儲庫中。

2. 設置您的 `Github Token`：

* [創建新的 **`Github Secret Token`**](https://github.com/settings/tokens/new)
  * 設置
  * 開發人員設置
  * 每個訪問令牌 - `Tokens（經典）`
  * 生成新的令牌
  * 選擇範圍：`repo` 和 `workflow`
  * **保留**您的秘密令牌（不要丟失它，您需要稍後粘貼它）

  <img src="https://github.com/Lin-jun-xiang/action-translate-readme/assets/63782903/b7487b49-817c-4925-b94a-bdb7b025a0c2" width=" 60%" />

* 創建新的 **`存儲庫密碼`**
  * 在您的存儲庫中 - `設置`
  * `安全性和變量`
  * `操作`
  * `新的存儲庫密碼`
  * 填寫標籤為 `token`，並將其命名（例如 `Action_Bot`）

  <img src="https://github.com/Lin-jun-xiang/action-translate-readme/assets/63782903/27dc7bcd-633f-431e-98e8-387b97ecd47c" width=" 60%" />

3. 在目錄 `.github/workflows/your_action.yml` 中創建您的操作示例。您只需複製以下代碼：

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
              uses: Lin-jun-xiang/action-translate-readme@v2 # 基於標籤
              with:
                token: ${{ secrets.Action_Bot }} # 基於步驟 2 中的名稱
                g4f_provider: g4f.Provider.DeepAi # 您可以更改此提供程序
                langs: "en,zh-TW,zh-CN,French,Arabic" # 您可以定義任何語言版本
```

注意 `.yml` 中有三個需要特別注意的參數：

* `token`: 根據步驟 2 創建的令牌。
* `g4f_provider`: gpt 的提供者，請參考此[鏈接](https://github.com/xtekky/gpt4free/tree/main#gpt-35--gpt-4)以了解更多信息。
* `langs`: 要生成的語言版本。請務必使用 `,` 分隔不同的語言。例如：
  * `"en"`：僅翻譯英文版。
  * `"en,zh-TW"`: 翻譯英文和繁體中文。
  * `"French,Arabic"`：翻譯法語和阿拉伯語。

4. 現在您可以更新 `README.md`，它會自動生成翻譯版本！

---

# 演示

![](./img/auto-translation.gif)

---

# 測試文檔結果

* 查看 [測試文檔](https://github.com/Lin-jun-xiang/vscode-extensions-best/tree/main)。
* 使用我們的工具更新測試文檔。

<a href="#top">返回頂部</a>
--------------------------------
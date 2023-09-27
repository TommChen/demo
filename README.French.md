# action-translate-readme

* [English](README.md)
* [Traditional Chinese README.md](README.zh-TW.md)
* [Simplified Chinese README.md](README.zh-CN.md)
* [French](README.French.md)
* [Arabic](README.Arabic.md)


# Introduction

* Nous savons tous que la rédaction de la documentation README peut être longue, mais maintenant il existe une solution qui peut vous faire gagner la moitié de votre temps. C'est notre `action-translate-readme`.

* Traduisez différentes versions de langues README via `gpt3.5`.

* Soumettre automatiquement (commit, pousser) les fichiers traduits via **Github Actions (CI/CD)**.

* Par exemple : lorsque vous **écrivez** ou **modifiez** la version anglaise du README, les versions traduites, telles que le chinois traditionnel, le chinois simplifié, le français, etc., sont automatiquement générées.

Remarque : Le traducteur de la version v1 est mis en œuvre via des paquets tiers sur `Linux`; La version v2 est mise en œuvre via l'API openai gratuite appelée [`g4f`](https://github.com/xtekky/gpt4free)


# Comment utiliser?

1. Cliquez sur l'icône :star: pour ajouter ce projet à votre dépôt Github.

2. Configurez votre `GitHub Token` :

* [Créez un nouveau **`GitHub Secret Token`**](https://github.com/settings/tokens/new)
  * Paramètres
  * Paramètres du développeur
  * Jetons d'accès personnels - `Tokens(classic)`
  * Générer un nouveau jeton
  * Choisissez les étendues : `repo` et `workflow`
  * **Conservez** votre secret token (ne le perdez pas, vous devrez le coller plus tard)

  <img src="https://github.com/Lin-jun-xiang/action-translate-readme/assets/63782903/b7487b49-817c-4925-b94a-bdb7b025a0c2" width=" 60%" />

* Créez un nouveau **`repository secret`**
  * Dans votre dépôt - `paramètres`
  * `Sécurité et variables`
  * `Actions`
  * `Nouveau repository secret`
  * Remplissez l'étiquette avec `token` et nommez-la (par exemple `Action_Bot`)

  <img src="https://github.com/Lin-jun-xiang/action-translate-readme/assets/63782903/27dc7bcd-633f-431e-98e8-387b97ecd47c" width=" 60%" />

3. Créez votre exemple d'action dans le répertoire `.github/workflows/your_action.yml`. Vous pouvez simplement copier le code suivant :

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
              uses: Lin-jun-xiang/action-translate-readme@v2 # Basé sur l'étiquette
              with:
                token: ${{ secrets.Action_Bot }} # Basé sur le nom d'étape 2
                g4f_provider: g4f.Provider.DeepAi # Vous pouvez changer ce fournisseur
                langs: "en,zh-TW,zh-CN,French,Arabic" # Vous pouvez définir n'importe quel langage
```

Il y a trois paramètres auxquels il faut prêter une attention particulière dans `.yml` :

* `token`: Le token créé dans le dépôt en fonction de l'étape 2.
* `g4f_provider`: Le fournisseur GPT, veuillez vous référer au [lien](https://github.com/xtekky/gpt4free/tree/main#gpt-35--gpt-4) pour plus d'informations.
* `langs`: Les versions de langue à générer. Veillez à séparer différentes langues par `,`. Par exemple :
  * `"en"`: Traduire uniquement la version anglaise.
  * `"en,zh-TW"`: Traduire en anglais et chinois traditionnel.
  * `"French,Arabic"`: Traduire en français et en arabe.

4. Maintenant, vous pouvez mettre à jour `README.md`, et il générera automatiquement une version traduite!

---

# Démonstration

![](./img/auto-translation.gif)

---

# Résultats du document de test

* Consultez le [document de test](https://github.com/Lin-jun-xiang/vscode-extensions-best/tree/main).
* Utilisez notre outil pour mettre à jour le document de test.

<a href="#top">Retour en haut</a>
--------------------------------
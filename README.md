# Mirror Git repository

🕶️ Mirror a Git source to another Git destination

<p align=center>
  <img width=400 src="https://i.imgur.com/vU2bVL5.png">
</p>

<div align=center>

<!-- prettier-ignore -->
[Try me workflow](https://github.com/actions4git/mirror/blob/main/.github/workflows/try-me.yml)
| [Try me mirror](https://github.com/actions4git/mirror-try-me)

</div>

## Usage

![GitHub Actions](https://img.shields.io/static/v1?style=for-the-badge&message=GitHub+Actions&color=2088FF&logo=GitHub+Actions&logoColor=FFFFFF&label=)
![Git](https://img.shields.io/static/v1?style=for-the-badge&message=Git&color=F05032&logo=Git&logoColor=FFFFFF&label=)

```yml
# octocat/.github or another third repository
# .github/workflows/mirror-mingw-regex-to-octocat-mingw-regex.yml
name: Mirror mingw/regex to octocat/mingw-regex
on:
  schedule:
    - cron: "36 */6 * * *"
  workflow_dispatch:
jobs:
  mirror-mingw-regex-to-octocat-mingw-regex:
    runs-on: ubuntu-latest
    steps:
      - run: git clone --bare https://git.code.sf.net/p/mingw/regex .
      - run: git push --mirror "https://x:$TOKEN@github.com/octocat/mingw-regex.git"
        env:
          TOKEN: ${{ secrets.MINGW_REGEX_TOKEN }}
```

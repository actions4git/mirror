# mirror
🕶️ Mirror a Git source to another Git destination

<!-- prettier-ignore -->
[Try me workflow](https://github.com/actions4git/mirror/blob/main/.github/workflows/try-me.yml)
| [Try me mirror](https://github.com/actions4git/mirror-try-me)

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
      - uses: actions4git/setup-git@v1
        with:
          token: ${{ secrets.MINGW_REGEX_TOKEN }}
      - run: git clone --bare https://git.code.sf.net/p/mingw/regex .
      - run: git push --mirror https://github.com/octocat/mingw-regex.git
```

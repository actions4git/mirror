# mirror
🕶️ Mirror a Git source to another Git destination

```yml
# octocat/.github or another third repository
# .github/workflows/mirror-mingw-regex-to-octocat-mingw-regex.yml
name: Mirror mingw/regex to octocat/mingw-regex
on:
  schedule:
    - cron: "36 */6 * * *"
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

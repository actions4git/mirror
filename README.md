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

**🚀 Here's what you want:**

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

This will sync the [mingw/regex] SourceForge Git repository to a GitHub
repository. Make sure you [create a GitHub personal access token] with
permission to push to your mirrored repository.

⚠️ This workflow file should be in a third repository. **Not the destination of
the mirroring.** It's recommended to put it in your "meta" repository if you
have one like octocat-org/.github or octocat/.github. Why do this? So that
there's a clean `git clone` & `git push` with no fiddling with an extra
synchronization workflow file.

💡 Try to provide a meta description somewhere on your mirrored repository's
page to indicate that it's a mirror of another project and not the original
source. You don't want people opening Pull Requests against your mirror! 🤣

<!-- prettier-ignore-start -->
[mingw/regex]: https://sourceforge.net/p/mingw/regex/ci/master/tree/
[create a github personal access token]: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens
<!-- prettier-ignore-end -->

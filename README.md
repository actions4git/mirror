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
      - run:
          git push --mirror
          "https://x:$TOKEN@github.com/octocat/mingw-regex.git"
        env:
          TOKEN: ${{ secrets.MINGW_REGEX_TOKEN }}
```

This will sync the [mingw/regex] SourceForge Git repository to a GitHub
repository. Make sure you [create a GitHub personal access token] with
permission to push to your mirrored repository. You can

To get started mirroring, here's what you need to do:

1. Identify the `git clone` URL of the source repository that you want to mirror
   from. This is usually from an existing service like GitLab or SourceForge.
2. If needed, authenticate with the source when you clone it. Usually this isn't
   needed since most mirroring sources are public and don't need any
   authentication to clone them.
3. Figure out where you want to push the cloned source repository to. This is
   the destination of your mirroring operation. Normally this will be a GitHub
   repository, but it could be a non-GitHub repository too. Make sure that the
   repository **exists** and is pushable!
4. **Authenticate!** You need to somehow provide a token, password, or other
   authentication to push to a Git destination. For GitHub, that means putting a
   `x:<token>@` prefix in front of the `github.com` part of the push destination
   URL. For other services this may be different.

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

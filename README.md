# Mirror Git repository

🔄 Mirror GitLab, SourceForge, GitHub, and other Git repositories

<p align=center>
  <img width=400 src="https://i.imgur.com/zo0vBZj.png">
</p>

<p align=center>
  <a href="https://github.com/actions4git/mirror-try-me">Try me mirror</a>
</p>

## Usage

![GitHub Actions](https://img.shields.io/static/v1?style=for-the-badge&message=GitHub+Actions&color=2088FF&logo=GitHub+Actions&logoColor=FFFFFF&label=)
![Git](https://img.shields.io/static/v1?style=for-the-badge&message=Git&color=F05032&logo=Git&logoColor=FFFFFF&label=)

💡 Try to provide a meta description somewhere on your mirrored repository's
page to indicate that it's a mirror of another project and not the original
source. You don't want people opening Issues or merge requests against your
mirror! 🤣

### Mirror from GitHub to GitLab

![GitHub](https://img.shields.io/static/v1?style=for-the-badge&message=GitHub&color=181717&logo=GitHub&logoColor=FFFFFF&label=)
![GitLab](https://img.shields.io/static/v1?style=for-the-badge&message=GitLab&color=FC6D26&logo=GitLab&logoColor=FFFFFF&label=)

<!-- prettier-ignore -->
```yml
# octocat/my-project [source repository]
# .github/workflows/mirror.yml
name: Mirror
on:
  push:
  create:
  delete:
  schedule:
    - cron: "36 */6 * * *"
  workflow_dispatch:
jobs:
  mirror:
    concurrency:
      group: ${{ github.workflow }}
      cancel-in-progress: true
    runs-on: ubuntu-latest
    steps:
      - run: git clone --bare "https://github.com/$GITHUB_REPOSITORY" .
      - run: git push --mirror "https://x:$GITLAB_TOKEN@gitlab.com/myorg/my-project.git"
        env:
          GITLAB_TOKEN: ${{ secrets.MY_TOKEN }}
```

Make sure you [create a GitLab personal access token] with the permissions
needed to write to the myorg/my-project Git destination repository. Then make
sure you add the secret token value to the GitHub settings panel for the source
repository.

If you're using a non-public GitHub repository you may need to use [`gh auth
setup-git`] to configure your credentials properly.

### Mirror from GitLab to GitHub

![GitLab](https://img.shields.io/static/v1?style=for-the-badge&message=GitLab&color=FC6D26&logo=GitLab&logoColor=FFFFFF&label=)
![GitHub](https://img.shields.io/static/v1?style=for-the-badge&message=GitHub&color=181717&logo=GitHub&logoColor=FFFFFF&label=)

<!-- prettier-ignore -->
```yml
# octocat/.github [another third repository]
# .github/workflows/mirror.yml
name: Mirror
on:
  schedule:
    - cron: "36 */6 * * *"
  workflow_dispatch:
jobs:
  mirror:
    concurrency:
      group: ${{ github.workflow }}
      cancel-in-progress: true
    runs-on: ubuntu-latest
    steps:
      - run: git clone --bare https://gitlab.com/myorg/my-project.git .
      - run: git push --mirror "https://x:$GITHUB_TOKEN@github.com/octocat/my-project.git"
        env:
          GITHUB_TOKEN: ${{ secrets.MY_TOKEN }}
```

You'll need to [create a GitHub personal access token] with write permissions to
the contents of the octocat/my-project GitHub repository and then add the secret
GitHub token to your third repository that will manage the scheduled syncing.

### Mirror from SourceForge to GitHub

![SourceForge](https://img.shields.io/static/v1?style=for-the-badge&message=SourceForge&color=FF6600&logo=SourceForge&logoColor=FFFFFF&label=)
![GitHub](https://img.shields.io/static/v1?style=for-the-badge&message=GitHub&color=181717&logo=GitHub&logoColor=FFFFFF&label=)

<!-- prettier-ignore -->
```yml
# octocat/.github [another third repository]
# .github/workflows/mirror.yml
name: Mirror
on:
  schedule:
    - cron: "36 */6 * * *"
  workflow_dispatch:
jobs:
  mirror:
    concurrency:
      group: ${{ github.workflow }}
      cancel-in-progress: true
    runs-on: ubuntu-latest
    steps:
      - run: git clone --bare https://git.code.sf.net/p/myorg/my-project .
      - run: git push --mirror "https://x:$GITHUB_TOKEN@github.com/octocat/my-project.git"
        env:
          GITHUB_TOKEN: ${{ secrets.MY_TOKEN }}
```

You'll need to [create a GitHub personal access token] with write permissions to
the contents of the octocat/my-project GitHub repository and then add the secret
GitHub token to your third repository that will manage the scheduled syncing.

<!-- prettier-ignore-start -->
[create a github personal access token]: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens
[create a gitlab personal access token]: https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html#create-a-personal-access-token
[`gh auth setup-git`]: https://cli.github.com/manual/gh_auth_setup-git
<!-- prettier-ignore-end -->

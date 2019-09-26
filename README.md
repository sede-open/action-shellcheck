# GitHub Action: Run shellcheck with reviewdog

[![Docker Image CI](https://github.com/reviewdog/action-shellcheck/workflows/Docker%20Image%20CI/badge.svg)](https://github.com/reviewdog/action-shellcheck/actions)
[![Release](https://img.shields.io/github/release/reviewdog/action-shellcheck.svg?maxAge=43200)](https://github.com/reviewdog/action-shellcheck/releases)

This action runs [shellcheck](https://github.com/koalaman/shellcheck) with
[reviewdog](https://github.com/reviewdog/reviewdog) on pull requests to improve
code review experience.

[![github-pr-check sample](https://user-images.githubusercontent.com/3797062/65701219-e828b980-e0bb-11e9-9051-2a1f400fe5e5.png)](https://github.com/reviewdog/action-shellcheck/pull/1)
[![github-pr-review sample](https://user-images.githubusercontent.com/3797062/65700741-1c4faa80-e0bb-11e9-8cbd-9a99aeb38594.png)](https://github.com/reviewdog/action-shellcheck/pull/1)

## Inputs

### `github_token`

**Required**. Must be in form of `github_token: ${{ secrets.github_token }}`'.

### `level`

Optional. Report level for reviewdog [info,warning,error].
It's same as `-level` flag of reviewdog.

### `reporter`

Reporter of reviewdog command [github-pr-check,github-pr-review].
Default is github-pr-check.
github-pr-review can use Markdown and add a link to rule page in reviewdog reports.

### `path`

Optional. Base directory to run shellcheck. Same as `[path]` of `find` command. Default: `.`

### `pattern`

Optional. File patterns of target files. Same as `-name [pattern]` of `find` command. Default: `*.sh`

### `exclude`

Optional. Exclude patterns of target files. Same as `-not -path [exclude]` of `find` command.
e.g. `./git/*`

### `shellcheck_flags`

Optional. Flags of shellcheck command. Default: `--external-sources`

## Example usage

### [.github/workflows/reviewdog.yml](.github/workflows/reviewdog.yml)

```yml
name: reviewdog
on: [pull_request]
jobs:
  shellcheck:
    name: runner / shellcheck
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v1
      - name: shellcheck
        uses: reviewdog/action-shellcheck@v1
        with:
          github_token: ${{ secrets.github_token }}
          reporter: github-pr-review # Change reporter.
          path: "." # Optional.
          pattern: "*.sh" # Optional.
          exclude: "./.git/*" # Optional.
```

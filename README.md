# Create or Update Unique Comment Action

[![CI](https://github.com/ovsds/create-or-update-unique-comment-action/workflows/Check%20PR/badge.svg)](https://github.com/ovsds/create-or-update-unique-comment-action/actions?query=workflow%3A%22%22Check+PR%22%22)
[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-Create%20or%20Update%20Unique%20Comment-blue.svg)](https://github.com/marketplace/actions/create-or-update-unique-comment)

A GitHub action to create or update a unique comment on a PR or Issue.
If the comment already exists, it will update the comment.

This action is a composite of
[peter-evans/create-or-update-comment](https://github.com/peter-evans/create-or-update-comment) and
[peter-evans/find-comment](https://github.com/peter-evans/find-comment) actions.

## Usage

### Example

```yaml
jobs:
  create-or-update-unique-comment:
    permissions:
      contents: read

    steps:
      - name: Create comment
        uses: ovsds/create-or-update-unique-comment-action@v1
        with:
          issue-number: 1
          body: |
            Example comment body that contains unique part to identify the comment.
            And some more text that is dynamic.
          unique-body-includes: |
            Example comment body that contains unique part to identify the comment.
```

### Action Inputs

Action inputs are mostly the same as in
[create-or-update-comment](https://github.com/peter-evans/create-or-update-comment/tree/main?tab=readme-ov-file#action-inputs).

| Name                   | Description                                                                                                                                                                                         | Default            |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------ |
| `token`                | `GITHUB_TOKEN` (`issues: write`, `pull-requests: write`) or a `repo` scoped [PAT](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token). | `GITHUB_TOKEN`     |
| `repository`           | The full name of the repository in which to create or update a comment.                                                                                                                             | Current repository |
| `issue-number`         | The number of the issue or pull request in which to create a comment.                                                                                                                               |                    |
| `body`                 | The comment body. Cannot be used in conjunction with `body-path`.                                                                                                                                   |                    |
| `body-path`            | The path to a file containing the comment body. Cannot be used in conjunction with `body`.                                                                                                          |                    |
| `edit-mode`            | The mode when updating a comment, `replace` or `append`.                                                                                                                                            | `replace`          |
| `append-separator`     | The separator to use when appending to an existing comment. (`newline`, `space`, `none`)                                                                                                            | `newline`          |
| `reactions`            | A comma or newline separated list of reactions to add to the comment. (`+1`, `-1`, `laugh`, `confused`, `heart`, `hooray`, `rocket`, `eyes`)                                                        |                    |
| `reactions-edit-mode`  | The mode when updating comment reactions, `replace` or `append`.                                                                                                                                    | `replace`          |
| `comment-author`       | The author of the comment to search for.                                                                                                                                                            |                    |
| `unique-body-includes` | A string to search for in the body of comments, originally `body-includes`.                                                                                                                         |                    |
| `unique-body-regex`    | A regular expression to search for in the body of comments, originally `body-regex`.                                                                                                                |                    |
| `find-direction`       | Search direction, specified as `first` or `last`, originally `direction`.                                                                                                                           | `first`            |
| `find-nth`             | 0-indexed number, specifying which comment to return if multiple are found, originally `nth`                                                                                                        | 0                  |

### Action Outputs

| Name         | Description            |
| ------------ | ---------------------- |
| `comment-id` | The ID of the comment. |

## Development

### Global dependencies

- [Taskfile](https://taskfile.dev/installation/)
- [nvm](https://github.com/nvm-sh/nvm?tab=readme-ov-file#install--update-script)

### Taskfile commands

For all commands see [Taskfile](Taskfile.yaml) or `task --list-all`.

## License

[MIT](LICENSE)

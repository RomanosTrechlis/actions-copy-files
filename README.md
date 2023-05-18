# actions-copy-files

Action that copies files or directories from GitHub repository
to another.

## Inputs
### `source-files` (argument)
The files/directories to copy to the destination repository. Can have multiple space-separated filenames and globbing.

### `destination-username` (argument)
The name of the user or organization which owns the destination repository. E.g. `nkoppel`

### `destination-repository` (argument)
The name of the repository to copy files to, E.g. `push-files-to-another-repository`

### `destination-branch` (argument) [optional]
The branch name for the destination repository. Defaults to `master`.

### `destination-directory` (argument) [optional]
The directory in the destination repository to copy the source files into. Defaults to the destination project root.

### `commit-username` (argument) [optional]
The username to use for the commit in the destination repository. Defaults to `destination-username`

### `commit-email` (argument)
The email to use for the commit in the destination repository.

### `commit-message` (argument) [optional]
The commit message to be used in the output repository.

The string `ORIGIN_COMMIT` is replaced by `[destination url]@[commit]`.

### `GITHUB_TOKEN` (environment)
The GitHub api token which allows this action to push to the destination repository.
E.g.:
`GITHUB_TOKEN: ${{ secrets.GH_TOKEN }}`

Guide for create a PAT [here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

## Example

```yaml
on:
  push:

jobs:
  build:
    name: Copy JSON specs to ailabs-cli config Repo
    runs-on: ubuntu-latest
    steps:
      - name: Push JSON schema for YAML configuration of CLI
        uses: RomanosTrechlis/actions-copy-files@master
        env:
          GITHUB_TOKEN: ${{ secrets.GH_TOKEN }}
        with:
          source-files: config
          destination-username: 'RomanosTrechlis'
          destination-repository: 'repository'
          destination-directory: 'config/'
          commit-email: 'r.trechlis@gmail.com'
          commit-username: 'RomanosTrechlis'
```

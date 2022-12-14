# Highlight changes in NPM dependencies on Pull Requests

(this is an extension of https://github.com/hiwelo/new-dependencies-action)

In Pull Requests, this action highlight the addition of new NPM dependencies, 
the update or the removal of existing ones in one of the `package.json` of your repository.
It also provides the link to the package page on npmJS and to the source code page

This action is not only looking at the root-level `package.json` but potentially
any existing `package.json` in the project to be compatible with monorepo
projects.

To highlight new/updated/removed packages, this action compares the list of dependencies
registered in the current branch with the ones registered in the base branch.
This check only occurs for each `package.json` file added or updated with the
current pull request.

## Dependencies updates

Adding new, upgrading or removing dependencies in a project should never be a small change, 
and often it should trigger discussions between maintainers. This action can help you
making sure that you are not missing addition of new package, upgrades or removal in your NPM
`dependencies` and `devDependencies`.

## Usage

This _GitHub Action_ should run everytime a commit is pushed to the pull request
to check any potential addition or change in one of your `package.json`.

```yml
name: Inspect dependencies
on:
  - pull_request

jobs:
  check_dependencies:
    runs-on: ubuntu-latest
    steps:
      - name: Check for new and updated dependencies
        uses: rknj/dependencies-updates-action@v1.1.0
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          show_dev_dependencies: 'false'
          show_checklist: 'true'

```

### Build

Build the typescript and package it for distribution

```
$ npm run build && npm run pack
```

## Example (with the optional checklist)

- [ ] Did you check the impact on the platform?
- [ ] Did you check if these libraries are still supported?
- [ ] Did you check if there are security vulnerabilities?
- [ ] Did you check if the licenses are compatible with our products?

| Dependency | Description | Version | License | Source |
| ----------- | ------------------ | ------------------ | ------------------ | ------------------ |
| [i18next](https://www.npmjs.com/package/i18next) (Added) | i18next internationalization framework | 21.10.0 | MIT | [i18next](https://www.i18next.com) |
| [copy-to-clipboard](https://www.npmjs.com/package/copy-to-clipboard) (Updated) | Copy stuff into clipboard using JS with fallbacks | 3.3.2 | MIT | [copy-to-clipboard](https://github.com/sudodoki/copy-to-clipboard#readme) |
| [react-dom](https://www.npmjs.com/package/react-dom) (Removed) | React package for working with the DOM. | 18.2.0 | MIT | [react-dom](https://reactjs.org/) |

| Dev Dependency | Description | Version | License | Source |
| ----------- | ------------------ | ------------------ | ------------------ | ------------------ |
| [jest-junit](https://www.npmjs.com/package/jest-junit) (Removed) | A jest reporter that generates junit xml files | 14.0.1 | Apache-2.0 | [jest-junit](https://github.com/jest-community/jest-junit#readme) |

## License

This project is released under the MIT License.

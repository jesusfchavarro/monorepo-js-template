# monorepo-js-template

This is a monorepo templete for JS/TS projects. The be happy and make our life easier we will use some tools.

From now on we refer to the root project like workspace and the subprojects like packages

[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/jesusfchavarro/monorepo-js-template/pulls)

- [monorepo-js-template](#monorepo-js-template)
  - [Scripty](#scripty)
  - [Prettier](#prettier)
  - [ESlint](#eslint)
  - [Lerna](#lerna)
    - [`lerna boostrap`](#lerna-boostrap)
    - [[`lerna add [package]`](https://github.com/lerna/lerna/tree/main/commands/add#readme)](#lerna-add-package)
    - [[`lerna run [script]`](https://github.com/lerna/lerna/tree/main/commands/run#readme)](#lerna-run-script)
    - [`lerna clean`](#lerna-clean)
    - [Bonus: filter-options](#bonus-filter-options)
  - [conventional-changelog](#conventional-changelog)
    - [Commitlint](#commitlint)
    - [Commitizen](#commitizen)
  - [husky](#husky)
  - [lint-staged](#lint-staged)

## [Scripty](https://www.npmjs.com/package/scripty)

The NPM scripts are cool but can get messy over the time and to me it just make sense to have scripts in separate files instead of an unique json file. More if we have more than 1 package.json with repeated script/task.

We'll have the scripts for the workspace and scripts for the packages. For now we include the lint command as an useful example. The package's lint just run lint in the package and the workspace lint run the package's lint of all the packages.

All the scripts are going to be in the `scripts` folder.

## [Prettier](https://prettier.io/docs/en/install.html)

A tool to make our code prettier as you can imagine. You can install it as an NPM package or in your code editor/IDE. The `.prettierrc` file if for configuration and tell the editor how you want to format your code.

## [ESlint](https://eslint.org/docs/user-guide/getting-started)

A linter is the easiest way to avoid/solve silly errors and also helps to have a minimum code quality. The `.eslintrc` in the root directory is just a initial and recommended configuration. All the packages have their `.eslintrc` file that extends the root's file and allow a 'per package' configuration.

## [Lerna](https://github.com/lerna/lerna#readme)

This is a monorepo so we need monorepo's tools. With lerna we have all we need to start rigth away. For now you just have to know 4 commands:

### [`lerna boostrap`](https://github.com/lerna/lerna/tree/main/commands/bootstrap#readme)

Installs all the dependencies(at the root level for better optimization) and link any cross-dependencies.

### [`lerna add [package]`](https://github.com/lerna/lerna/tree/main/commands/add#readme)

Add a local or remote package as dependency to all the packages in the repo.

```sh
lerna add <package>[@version] [--dev] [--exact] [--peer]
```

### [`lerna run [script]`](https://github.com/lerna/lerna/tree/main/commands/run#readme)

Run an NPM script in each package. Useful to build, watch, test, lint, clean all the packages. For that try some convention with the naming and use scripty :3

The command `lerna exec` use almost the same things but with an arbitrary command.

```sh
lerna run lint
lerna exec -- yarn lint
lerna exec -- rm -rf ./node_modules
```

### [`lerna clean`](https://github.com/lerna/lerna/tree/main/commands/clean#readme)

Remove the `node_modules` directory from all packages.

### Bonus: [filter-options](https://www.npmjs.com/package/@lerna/filter-options)

Not a command but a option to some lerna's commands to filter the packages.

## [conventional-changelog](https://github.com/conventional-changelog/conventional-changelog)

If no one is watching my commits message are always like: `Fix: some minor bugs` or `Just another commit`. To improve that we include the [conventional commit format](https://www.conventionalcommits.org/en/v1.0.0/).

### [Commitlint](https://github.com/conventional-changelog/commitlint)

A linter for commits!! Let you check your commit message. With some git hooks we'll prevent some unhelpful messages.

### [Commitizen](https://github.com/commitizen/cz-cli)

A CLI tool to make our life easier commiting things. Just type:

```sh
yarn commit #or
git cz
```

PD: Commitizen will ask something like:

```sh
? What is the scope of this change (e.g. component or file name): (press enter to skip)
```

You only can use the name of a packages. If is something like a monorepo configuration or general documentation you should skip the question.

## [husky](https://typicode.github.io/husky/#/?id=monorepo)

We want to do things before we commit things to our repo. For that we could use [githooks](https://git-scm.com/docs/githooks) with husky.

To configure some new hook just add a file with the hook's name in the `.husky` folder.

To enable the git hooks please run this in your terminal

```sh
yarn husky install
```

## [lint-staged](https://github.com/okonet/lint-staged)

We already talk about prettier and ESLint. Now we'll ensure that the remote repo stick with this. lint-staged allow to run things to all the staged files. Aside we configure the [`pre-commit`](.husky/pre-commit) hook to run lint-staged.

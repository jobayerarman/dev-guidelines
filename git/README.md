# Git Rules
There are a set of rules to keep in mind:

* Perform work in a `feature` branch.

    _Why:_
    >Because this way all work is done in isolation on a dedicated branch rather than the main branch. It allows you to submit multiple pull requests without confusion. You can iterate without polluting the master branch with potentially unstable, unfinished code.

* Branch out from `develop`

    _Why:_
    >This way, you can make sure that code in master will almost always build without problems, and can be mostly used directly for releases (this might be overkill for some projects).

* Never push into `develop` or `master` branch. Make a Pull Request.

    _Why:_
    > It notifies team members that they have completed a feature. It also enables easy peer-review of the code and dedicates forum for discussing the proposed feature.

* Before making a Pull Request, make sure your `feature` branch builds successfully and passes all tests (including code style checks).

    _Why:_
    > You are about to add your code to a stable branch. If your feature-branch tests fail, there is a high chance that your destination branch build will fail too. Additionally, you need to apply code style check before making a Pull Request. It aids readability and reduces the chance of formatting fixes being mingled in with actual changes.

* Protect your `develop` and `master` branch.

    _Why:_
    > It protects your production-ready branches from receiving unexpected and irreversible changes.

* Delete local and remote feature branches after merging.

    _Why:_
    > It will clutter up your list of branches with dead branches. It insures you only ever merge the branch back into (`master` or `develop`) once. Feature branches should only exist while the work is still in progress.

# Git Workflow

The overall Git workflow is:

1. A `develop` branch is created from `master`
2. Feature branches are created from `develop`
3. A PR is created from `feature` branch into the `develop` branch
4. When a `feature` is complete the PR is squashed and merged into the `develop` branch
5. A release branch is created from `develop`
6. When the `release` branch is done it is merged into `develop` and `master`
7. If an issue in `master` is detected a `hotfix` branch is created from `master`
8. Once the hotfix is complete it is merged to both `develop` and `master`

### Feature Branch
#### Steps to Follow:
1. Start with an updated local development branch -- by checking out the dev branch and pulling changes:
```bash
$ git checkout develop
$ git pull origin develop
```

2. Create and checkout a feature branch:
```bash
$ git checkout -b feature/branch-name
```
> *Note: Your branch name should start with feature and then a description of your feature (as above).*

3. Do work in your feature branch, committing early and often:
(Use this [guide](#commit-message-format) to write commit message)
```bash
$ git commit -m "commit message"
```

4. Rebase frequently to incorporate upstream changes:
```bash
$ git fetch origin development
$ git rebase origin/development
```
- or -
```bash
$ git checkout development
$ git pull
$ git checkout feature/branch-name
$ git rebase development
```

5. Optional: Perform an interactive rebase (squash) your commits before pushing the branch:
```bash
$ git fetch origin development
$ git rebase -i origin/development
```

6. Once you have reviewed your changes, and verified formatting and intention, push your changes upstream to origin:
```bash
$ git push -u origin feature/branch-name
```

#### Get Your Code Reviewed (by creating a Pull Request)!
Your code must be reviewed by other developers, and receive +1s from them, in order to be eligible for Merge.

1. Create a Pull Request in github between your feature branch and development.
2. After your code passes Code Review, merge your code into **Development Branch** via the GitHub interface. Delete your branch after merging.

### Bugfix Branch
#### Steps to Follow:
1. Start with an updated local development branch -- by checking out the dev branch and pulling changes:
```bash
$ git checkout develop
$ git pull origin develop
```

2. Create and checkout a bugfix branch:
```bash
$ git checkout -b bugfix/branch-name
```
> *Note: Your branch name should start with bugfix and then a description of your bug (as above).*

### Release Branch
#### Steps to Follow:
1. Start with an updated local development branch -- by checking out the dev branch and pulling changes:
```bash
$ git checkout develop
$ git pull origin develop
```

2. Create and checkout a release branch:
```bash
$ git checkout -b release/v1.0.0
```
> *Note: Your branch name should start with release and then a release version (as above).*

### Hotfix Branch
#### Steps to Follow:
1. Start with an updated local development branch -- by checking out the dev branch and pulling changes:
```bash
$ git checkout develop
$ git pull origin develop
```

2. Create and checkout a hotfix branch:
```bash
$ git checkout -b hotfix/v1.0.1
```
> *Note: Your branch name should start with your hotfix and then a hotfix version (as above).*

# Commit Message Format

Each commit message consists of a **header**, a **body** and a **footer**.  The header has a special
format that includes a **type**, a **scope** and a **subject**.
Extend git commit message from angular style.

All Commit Message Format **MUST** meet this Text Format:

```bash
[:<Emoji>: ][<Type>[(<Scope>)]: ]<Subject>
[<BLANK LINE>]
[<Message Body>]
[<BLANK LINE>]
[<Message Footer>]
```

### Types

| Type          | Description |
|:-------------|-------------|
| `new`         | for new feature implementing commit|
| `feature`     | for new feature implementing commit (equal `new`) |
| `bug`         | for bug fix commit |
| `security`    | for security issue fix commit |
| `performance` | for performance issue fix commit |
| `improvement` | for backwards-compatible enhancement commit |
| `breaking`    | for backwards-incompatible enhancement commit |
| `deprecated`  | for deprecated feature commit |
| `refactor`    | for refactoring commit |
| `docs`        | for documentation commit |
| `examples`    | for example code commit |
| `test`        | for testing commit |
| `dependency`  | for dependencies upgrading or downgrading commit |
| `config`      | for configuration commit |
| `build`       | for packaging or bundling commit |
| `release`     | for publishing commit |
| `update`      | for update commit |
| `wip`         | for work in progress commit |
| `chore`       | for other operations commit |

### Emojis

| Emoji                      | Raw Emoji Code               | Type               | Description |
|:--------------------------:|------------------------------|--------------------|-------------|
| :star:                     | `:star:`                     | `new` or `feature` | add **new feature** |
| :bug:                      | `:bug:`                      | `bug`              | fix **bug** issue |
| :lock:                     | `:lock:`                     | `security`         | fix **security** issue |
| :chart_with_upwards_trend: | `:chart_with_upwards_trend:` | `performance`      | fix **performance** issue |
| :zap:                      | `:zap:`                      | `improvement`      | update **backwards-compatible** feature |
| :boom:                     | `:boom`                      | `breaking`         | update **backwards-incompatible** feature |
| :warning:                  | `:warning:`                  | `deprecated`       | **deprecate** feature |
| :lipstick:                 | `:lipstick:`                 | `update`           | update **UI/Cosmetic** |
| :up:                       | `:up:`                       | `update`           | update **other** |
| :globe_with_meridians:     | `:globe_with_meridians:`     | `update`           | update or fix **internationalization** |
| :shirt:                    | `:shirt:`                    | `refactor`         | remove **linter**/strict/deprecation warnings or **refactoring** or code **layouting** |
| :white_check_mark:         | `:white_check_mark:`         | `test`             | add **tests** |
| :green_heart:              | `:green_heart:`              | `test`             | fix **tests** failur or **CI** building |
| :pencil:                   | `:pencil:`                   | `docs`             | update **documentation** |
| :copyright:                | `:license:`                  | `docs`             | decide or change **license** |
| :lollipop:                 | `:lollipop:`                 | `examples`         | for **example** codes |
| :arrow_up:                 | `:arrow_up:`                 | `dependency`       | upgrade **dependencies** |
| :arrow_down:               | `:arrow_down:`               | `dependency`       | downgrade **dependencies** |
| :pushpin:                  | `:pushpin:`                  | `dependency`       | pin **dependencies** |
| :wrench:                   | `:wrench:`                   | `config`           | update **configration** |
| :package:                  | `:package:`                  | `build`            | **packaging** or **bundling** or **building** |
| :hatching_chick:           | `:hatching_chick:`           | `release`          | **initial** commit |
| :confetti_ball:            | `:confetti_ball:`            | `release`          | release **major** version |
| :tada:                     | `:tada:`                     | `release`          | release **minor** version |
| :sparkles:                 | `:sparkles:`                 | `release`          | release **patch** version |
| :rocket:                   | `:rocket:`                   | `release`          | **deploy** to production enviroment |
| :back:                     | `:back:`                     | `revert`           | **revert** commiting |
| :construction:             | `:construction:`             | `wip`              | **WIP** commiting |
| :twisted_rightwards_arrows:| `:twisted_rightwards_arrows:`| -                  | merge **conflict resolution** |
| :heavy_plus_sign:          | `:heavy_plus_sign:`          | -                  | **add** files, dependencies, ... |
| :heavy_minus_sign:         | `:heavy_minus_sign:`         | -                  | **remove** files, dependencies, ... |
| :on:                       | `:on:`                       | -                  | **enable** feature and something ... |

Ask to Be [Creative](http://www.emoji-cheat-sheet.com/)!

### Examples

new:
```
:star: new(graphite): add 'graphiteWidth' option
```

bug fix:
```
:bug: fix(graphite): stop graphite breaking when width < 0.1

Closes #28
```

improve performance:
```
:chart_with_upwards_trend: performance(graphite): remove graphiteWidth option

The graphiteWidth option has been removed. The default graphite width of 10mm is always used for performance reason.
```

revert:
```
:back: revert: new: add 'graphiteWidth' option

This reverts commit 667ecc1654a317a13331b17617d973392f415f02.
```

[Git Commit Message Convention](https://github.com/kazupon/git-commit-message-convention)

# Gitflow CLI Commands

## Initialize
```bash
$ git flow init [-fd]
```
**-d** use default branch names

**-f** force

Initialize a new git repo with support for the branching model.


## Feature

```bash
$ git flow feature [list] [-v]
```

**-v** verbose (more) output

Lists existing features

```bash
$ git flow feature start [-F] \<name> [\<base>]
```
**-F** fetch from $ORIGIN before performing local operation

Start new feature _\<name>_, optionally basing it on _\<base>_ instead of _\<develop>_

```bash
$ git flow feature finish [-rFkDS] \<name|nameprefix>
```
**-r** rebase instead of merge

**-F** fetch from $ORIGIN before performing finish

**-k** keep branch after performing finish

**-D** force delete feature branch after finish

**-S** squash feature during merge

Finish feature _\<name>_

```bash
$ git flow feature publish \<name>
```

Start sharing feature _\<name>_ on $ORIGIN

```bash
$ git flow feature diff [\<name|nameprefix>]
```

Show all changes in _\<name>_ that are not in _\<develop>_

```bash
$ git flow feature rebase [-i] [\<name|nameprefix>]
```

**-i** do an interactive rebase

Rebase _\<name>_ on _\<develop>_

```bash
$ git flow feature checkout [\<name|nameprefix>]
```

Switch to feature branch _\<name>_

```bash
$ git flow feature pull \<remote> [\<name>]
```

Pull feature _\<name>_ from _\<remote>_


## Release

```bash
$ git flow release [list] [-v]
```
**-v** verbose (more) output

Lists existing releases

```bash
$ git flow release start [-F] \<version>
```
**-F** fetch from $ORIGIN before performing local operation

Start new release named _\<version>_

```bash
$ git flow release finish [-Fsumpkn] \<version>
```
**-F** fetch from $ORIGIN before performing finish

**-s** sign the release tag cryptographically

**-u** use the given GPG-key for the digital signature (implies -s)

**-m** use the given tag message

**-p** push to $ORIGIN after performing finish

**-k** keep branch after performing finish

**-n** don't tag this release

**-S** squash release during merge

Finish release _\<version>_

```bash
$ git flow release publish \<name>
```
Start sharing release _\<name>_ on $ORIGIN

```bash
$ git flow release track \<name>
```
Start tracking release _\<name>_ that is shared on $ORIGIN


## Hotfix
```bash
$ git flow hotfix [list] [-v]
```
**-v** verbose (more) output

Lists existing hotfixes
```bash
$ git flow hotfix start [-F] \<version> [\<base>]
```
**-F** fetch from $ORIGIN before performing local operation

Start new hotfix named _\<version>_, optionally base it on _\<base>_ instead of _\<master>_
```bash
$ git flow hotfix finish [-Fsumpkn] \<version>
```
**-F** fetch from $ORIGIN before performing finish

**-s** sign the release tag cryptographically

**-u** use the given GPG-key for the digital signature (implies -s)

**-m** use the given tag message

**-p** push to $ORIGIN after performing finish

**-k** keep branch after performing finish

**-n** don't tag this release

Finish hotfix _\<version>_


## Support
```bash
$ git flow support [list] [-v]
```
**-v** verbose (more) output

Lists existing support branches
```bash
$ git flow support start [-F] \<version> \<base>
```
**-F** fetch from $ORIGIN before performing local operation

Start new support branch named _\<version>_ based on _\<base>_

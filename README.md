# commitlint-config-emoji-convention

[![npm latest][version-img]][pkg-url]
[![download][download-img]][pkg-url]
[![MIT][license-img]](LICENSE)

Shareable commitlint configuration that enforces conventional commits and adds emoji support.
Use with [commitlint](https://www.npmjs.com/package/@commitlint/cli).

## Getting Started

```sh
npm install --save-dev @commitlint/cli commitlint-config-emoji-convention

echo "module.exports = { extends: ['emoji-convention'] }" > .commitlintrc.js
```

The official [commitlint documentation](https://commitlint.js.org/guides/local-setup.html) recommends using [Husky](https://typicode.github.io/husky/) to validate commit messages.

```sh
npm install --save-dev husky
npx husky init

echo "npx --no -- commitlint --edit \$1" > .husky/commit-msg
```

The above configuration will validate commit messages, but requires manual emoji inclusion. To automatically prepend emojis based on commit prefixes, perform the following steps:

```sh
touch .husky/prepare-commit-msg

# Add the following script:

msg=$(cat "$1")

msg=$(echo $msg | sed -e "s/^init/🎉 init/")
msg=$(echo $msg | sed -e "s/^feat/✨ feat/")
msg=$(echo $msg | sed -e "s/^fix/🐛 fix/")
msg=$(echo $msg | sed -e "s/^docs/📚 docs/")
msg=$(echo $msg | sed -e "s/^style/💎 style/")
msg=$(echo $msg | sed -e "s/^refactor/📦 refactor/")
msg=$(echo $msg | sed -e "s/^perf/🚀 perf/")
msg=$(echo $msg | sed -e "s/^test/🚨 test/")
msg=$(echo $msg | sed -e "s/^build/🛠 build/")
msg=$(echo $msg | sed -e "s/^ci/⚙️ ci/")
msg=$(echo $msg | sed -e "s/^chore/♻️ chore/")
msg=$(echo $msg | sed -e "s/^revert/🗑 revert/")

echo $msg > $1
```

## Format

```text
<emoji> <type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

### Examples

```text
✨ feat(blog): add comment section
```

```text
🐛 fix: resolve null pointer exception
```

```text
📚 docs(README): add contribution guidelines

- Added code of conduct
- Updated PR template

Issue: #123
```

## Rules

Commit message rules follow the [Conventional Commits](https://www.conventionalcommits.org) specification.

Supported commit types:

- **🎉 init**: Project initialization
- **✨ feat**: A new feature
- **🐛 fix**: A bug fix
- **📚 docs**: Documentation only changes
- **💎 style**: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
- **📦 refactor**: A code change that neither fixes a bug nor adds a feature
- **🚀 perf**: A code change that improves performance
- **🚨 test**: Adding missing tests or correcting existing tests
- **🛠 build**: Changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm)
- **⚙️ ci**: Changes to our CI configuration files and scripts (example scopes: Travis, Circle, BrowserStack, SauceLabs)
- **♻️ chore**: Other changes that don't modify src or test files
- **🗑 revert**: Reverts a previous commit

## Credits

- The initial inspiration for this project was [commitlint-config-git-commit-emoji](https://github.com/ccnnde/commitlint-config-git-commit-emoji), including the `parserPreset` configuration and README structure
- Emoji list and rules sourced from [@commitlint/config-conventional](https://commitlint.js.org/reference/prompt.html)
- The `prepare-commit-msg` hook script was adapted from [Hubert Olender's gist](https://gist.github.com/olenderhub/053faaf522e83783456f3d575e8fe572)

## License

[MIT](LICENSE) © João Vitor

<!-- badge url -->

[pkg-url]: https://www.npmjs.com/package/commitlint-config-emoji-convention
[version-img]: https://img.shields.io/npm/v/commitlint-config-emoji-convention?color=deepgreen&style=flat-square
[download-img]: https://img.shields.io/npm/dm/commitlint-config-emoji-convention?style=flat-square
[license-img]: https://img.shields.io/badge/license-MIT-blue?style=flat-square

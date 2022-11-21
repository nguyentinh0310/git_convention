# Git Conventional

## Introduce

- [Git Conventional](#git-conventional)
  - [Introduce](#introduce)
  - [git commit convention](#git-commit-convention)
    - [Commit Formats](#commit-formats)
      - [Types](#types)
      - [Scopes](#scopes)
      - [Subject](#subject)
      - [Body](#body)
      - [Footer](#footer)
    - [Rules](#rules)
    - [Examples In reality](#examples-in-reality)
  - [git branch convention](#git-branch-convention)
    - [Branch Formats](#branch-formats)
    - [Branch Rules](#branch-rules)

## git commit convention

### Commit Formats

Default

<pre>
<b><a href="#types">&lt;type&gt;</a></b>(<b><a href="#scopes">&lt;optional scope&gt;</a></b>): <b><a href="#subject">&lt;subject&gt;</a></b>
<sub>empty separator line</sub>
<b><a href="#body">&lt;optional body&gt;</a></b>
<sub>empty separator line</sub>
<b><a href="#footer">&lt;optional footer&gt;</a></b>
</pre>

Merge

<pre>
Merge branch '<b><a href="#branch-formats">&lt;branch name&gt;</a></b>'
</pre>

#### Types

- `feat` A new feature
- `fix` A bug fix
- `refactor` A code change that neither fixes a bug nor adds a feature
- `perf` A code change that improves performance
- `docs` Documentation only changes
- `style` Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
- `test` Adding missing tests or correcting existing tests
- `build` Changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm)
- `ci` Changes to our CI configuration files and scripts (example scopes: ci pipeline, Travis, Circle, BrowserStack, SauceLabs)
- `chore` Other changes that don't modify src or test files. modifying `.gitignore`
- `revert` Reverts a previous commit

#### Scopes

The `scope` provides additional contextual information.

- Is an **optional** part of the format
- Allowed Scopes depends on the specific project
- Don't use issue identifiers as scopes

#### Subject

The `subject` contains a succinct description of the change.

- Is a **mandatory** part of the format
- Use the imperative, present tense: "change" not "changed" nor "changes"
  - Think of `This commit will <subject>`
- Don't capitalize the first letter
- No dot (.) at the end

#### Body

The `body` should include the motivation for the change and contrast this with previous behavior.

- Is an **optional** part of the format
- Use the imperative, present tense: "change" not "changed" nor "changes"
- This is the place to mention issue identifiers and their relations

#### Footer

The `footer` should contain any information about **Breaking Changes** and is also the place to **reference Issues** that this commit refers to.

- Is an **optional** part of the format
- **optionally** reference an issue by its id.
- **Breaking Changes** should start with the word `BREAKING CHANGES:` followed by space or two newlines. The rest of the commit message is then used for this.

### Rules

- type-enum: `feat, fix, refactor, perf, docs, style, test, build, ci, chore, revert`

```diff
# fails
- git commit -m "foo(USERSITE-1): some message"
# passes
+ git commit -m "fix(USERSITE-1): some message"
```

- type-case: `lowerCase`

```diff
# fails
- git commit -m "FIX(USERSITE-1): some message"
# passes
+ git commit -m "fix(USERSITE-1): some message"
```

- type-empty

```diff
# fails
- git commit -m ": some message"
- git commit -m "(USERSITE-1): some message"
# passes
+ git commit -m "fix(USERSITE-1): some message"
```

- subject-case: `lowerCase` (don’t capitalize first letter)

```diff
# fails
- git commit -m "fix(USERSITE-1): Some message"
- git commit -m "fix(USERSITE-1): Some Message"
- git commit -m "fix(USERSITE-1): SomeMessage"
- git commit -m "fix(USERSITE-1): SOMEMESSAGE"
# passes
+ git commit -m "fix(USERSITE-1): some message"
+ git commit -m "fix(USERSITE-1): someMessage Hi!"
```

- subject-empty

```diff
# fails
- git commit -m "fix(USERSITE-1):"
# passes
+ git commit -m "fix(USERSITE-1): some message"
```

- subject-full-stop `'.'`

```diff
# fails
- git commit -m "fix(USERSITE-1): some message."
# passes
+ git commit -m "fix(USERSITE-1): some message"
+ git commit -m "fix(USERSITE-1): remove unused dependency lodash.camelcase"
+ git commit -m "build(release): version to 1.0.0"
```

header-max-length (max length 100)

```diff
# fails
- git commit -m "fix(USERSITE-1): some message that is way too long and breaks the line max-length by several characters"
# passes
+ git commit -m "fix(USERSITE-1): some message"
```

body-leading-blank

```diff
# warning
! git commit -m "fix(USERSITE-1): some message
! This is message body."
# passes
+ git commit -m "fix(USERSITE-1): some message
+
+ This is message body."

# tips: commit body
+ git commit -m "fix(USERSITE-1): some message" -m "This is message body."
```

body-max-line-length (max length 100)

```diff
# fails
- git commit -m "fix(USERSITE-1): some message
-
- body with multiple lines
- has a message that is way too long and will break the line rule 'line-max-length' by several characters"
# passes
+ git commit -m "fix(USERSITE-1): some message
+
+ body with multiple lines
+ but still no line is too long"

# tips: commit body with multiple lines. ($'' and \n) $'line1\nline2'
+ git commit -m 'fix(USERSITE-1): some message' -m $'body with multiple lines\nbut still no line is too long'
```

footer-leading-blank

```diff
# warning
! git commit -m "fix(USERSITE-1): some message
! BREAKING CHANGE: This is message footer"
# passes
+ git commit -m "fix(USERSITE-1): some message
+
+ BREAKING CHANGE: This is message footer"

# tips: commit footer
+ git commit -m "fix(USERSITE-1): some message" -m "BREAKING CHANGE: It will be significant"
```

footer-max-line-length (max line lenght 100)

```diff
# fails
- git commit -m "fix(USERSITE-1): some message
-
- BREAKING CHANGE: footer with multiple lines
- has a message that is way too long and will break the line rule 'line-max-length' by several characters"
# passes
+ git commit -m "fix(USERSITE-1): some message
+
+ BREAKING CHANGE: footer with multiple lines
+ but still no line is too long"

# tips: commit footer with multiple lines. ($'' and \n) $'line1\nline2'
+ git commit -m 'fix(USERSITE-1): some message' -m $'BREAKING CHANGE: footer with multiple lines\nbut still no line is too long'
```

### Examples In reality

```diff
# bad
- git commit -m "update something"
# good
+ git commit -m "feat(USERSITE-1): add the amazing button"
```

```diff
+ git commit -m "feat: remove ticket list endpoint
+
+ refers to USERSITE-1
+
+ BREAKING CHANGES: ticket enpoints no longer supports list all entites."
```

```diff
+ git commit -m "fix: add missing parameter to service call
+
+ The error occurred because of <reasons>."
```

```diff
+ git commit -m "build(release): bump version to 1.0.0"
```

```diff
+ git commit -m "build: update dependencies"
```

```diff
+ git commit -m "refactor: implement calculation method as recursion"
```

```diff
+ git commit -m "style: remove empty line"
```

## git branch convention

### Branch Formats

Default

<pre>
<b><a>master</a></b>
<b><a>main</a></b>
<b><a>develop</a></b>
</pre>

Others

<pre>
<b><a>feature</a></b><i>/some-things</i>
<b><a>fix</a></b><i>/some-things</i>
<b><a>hotfix</a></b><i>/some-things</i>
<b><a>release</a></b><i>/some-things</i>
</pre>

### Branch Rules

- type-enum: `master, main, develop, feature, fix, hotfix, release`

```diff
# fails
- branch-name-some-thing
- feat/some-thing
# passes
+ master
+ main
+ develop
+ fix/USERSITE-1-some-thing
+ feature/USERSITE-1-some-thing
+ hotfix/some-thing
+ release/some-things
```


# Development standards

Good development standards make for better code.

**Versioning**: We try to adhere to [SemVer](https://semver.org/).

!!!note

    The stipulations below are based on experience, but are still evolving.
    This text is mainly here to provide a starting point for discussion with collaborators.
    <!-- TODO: Look into [Conventional commits](https://www.conventionalcommits.org/en/v1.0.0/#specification) and see if we want to use/adapt their specification. -->

## Commit messages

> A well-cared for (commit) log is a beautiful and useful thing

This quote comes from the following article, which should be considered a mandatory read for anyone maintaining a package:

[https://cbea.ms/git-commit/](https://cbea.ms/git-commit/)

The summary, slightly adapted by personal preferences (indicated in boldface):

* [Separate subject/title from body with a blank line](https://cbea.ms/git-commit/#separate).
* [Limit the subject line to 50 characters](https://cbea.ms/git-commit/#limit-50) **if possible, 72 is a hard limit**.
* [Capitalize the subject line](https://cbea.ms/git-commit/#capitalize) and [do not end it with a period](https://cbea.ms/git-commit/#end).
* [Use the imperative mood in the subject line](https://cbea.ms/git-commit/#imperative).
* [Wrap the body at](https://cbea.ms/git-commit/#wrap-72) **88 characters**.
* [Use the body to explain what and why vs. how](https://cbea.ms/git-commit/#why-not-how).

In addition, try to make [atomic commits](https://www.freshconsulting.com/insights/blog/atomic-commits/) when possible.
We've also taken inspiration from the [MyST parser contribution guide](https://github.com/executablebooks/MyST-Parser?tab=contributing-ov-file#commit-messages).[^1] 

[^1]: Shoutout to my boi [Chris Sewell](https://github.com/chrisjsewell). The man, the legend. The quintessential British b***ard.

Here is an example of the desired format for a commit message:

```
<TYPE-EMOJI> <SCOPE>: Summarize changes in 72 characters or less

More detailed explanatory text, if necessary. Explain the problem that this
commit is solving. Focus on what you are changing, why you are making this
change and why you chose your approach, as opposed to how the change was made
(the code and comments should explain that). Are there side effects or other
unintuitive consequences of this change? Here's the place to explain the
context of your commit to someone else reading your message in the future
(most likely you).

PS: There is no need to mention you also added unit tests when adding a new
    feature. The code diff already makes this clear.
```

Besides being an invaluable resources for future maintainers, writing a commit message forces you to explain your change.
It forces you to stop and think again.
Is this really the best approach to solving the issue?
If it's hard to explain the change, maybe it's a bad idea?

### Specifying the type of change

Specifying the type of change in a commit can be useful for several reasons:

- Understanding the changes of a commit.
- Where to (automatically) put the commit in the changelog, if at all.
- What to include in a support branch for a previous major release.
- Encouraging atomic commits.
- What the priority should be when reviewing open PRs. 

We use **exactly one leading** emoji per commit to indicate the type of change.
Some advantages:

- Only a single character needed!
  Save precious space in the subject line.
- A clear visual indicator of the type of change.
- Clearly separates type from scope/content.
- Language-agnostic.
- They look great. At least on macOS.

!!! important

    Although we are in favor of using leading emojis to indicate the type, we do **not** allow emojis further down the subject line.
    This makes it easier to `grep` for commit types.

The list in the table below is in order of priority, e.g. a backwards-incompatible change might improve an existing feature by breaking its API, but should _not_ be typed as an improvement (👌).
Similarly, if a dependency is changed, it's convenient to quickly spot this, e.g. when updating a conda feedstock.

| Emoji | Meaning                                                          | Similar to [Angular type](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines) | In changelog summary?  |
| ----- | ---------------------------------------------------------------- | ----------------------------------------- | ------------------------- |
| 💥    | introduce a backward-incompatible (breaking) change / remove deprecated code | `\<type>!` (use `!` + `BREAKING CHANGE:`) | **Yes**                   |
| 📦    | add, update or change a dependency                                    | `build`                                   | **Yes**                   |
| ✨    | introduce new features                                           | `feat`                                    | **Yes**                   |
| 👌    | improve an existing code/feature (no breaking)                   | `perf`/`feat`                             | **Yes**                   |
| 🐛    | fix a code bug                                                   | `fix`                                     | **Yes**                   |
| ❌    | mark code as deprecated (note removal version/replacement)       | `refactor`                                | **Yes**                   |
| 📚    | add or adapt documentation                                       | `docs`                                    | No                        |
| 🔄    | refactor existing code with no behavior change                   | `refactor`                                | No                        |
| 🧪    | add or adapt tests                                               | `test`                                    | No                        |
| 🚀    | bump the package version for release                             | `chore`                                   | No                        |
| 🧹    | clean up comments / small formatting                             | `style`                                   | No                        |
| ⏪    | revert a previous commit                                         | `revert`                                  | No                        |
| 🔧    | devops-related changes (pre-commit, CI/CD, etc.)                 | `ci`                                      | No                        |
| 🐭    | minor changes (typos etc.; exclude from changelog)               | `chore`                                   | No                        |
| ❓    | anything not covered above (last resort)                         | `chore`                                   | No                        |

!!!note

    We are aware of other standards like [GitMoji](https://gitmoji.dev/), but limit the number in order to avoid choice overload.
    Too many options make it difficult for contributors to know all of them, makes changelogs too fragmented and leads to decision paralysis.
    Moreover, we avoid emojis that typically have width issues in some terminals.
    <!-- TODO: Also look into and add reference to https://github.com/ahmadawais/Emoji-Log -->

!!!note

    Not everyone likes emojis. In the dropdown below you can find some common concerns.

    ??? "Common concerns"

        > Tooling can’t parse emojis.
        
        We haven't needed to use much tooling so far, and built our own for e.g. the changelog.

        > Search/`grep` is harder.
        
        You can `grep` for emojis too!
        In fact, it's _easier_ to exclusively find the commits you are looking for:

            git log --oneline | grep '[💥✨👌🐛❌📦]'

        Using e.g. `test` to `grep` for the type will likely also find commits of other types.

        > Accessibility / screen readers read ‘sparkles’
        
        This is a fair point.
        In case we start working with collaborators that rely on such tools we will adapt.

        > Rendering/width issues in some terminals.
       
        We selected emojis with default emoji presentation (no variation selector), which render correctly in modern terminals.

        > Ambiguity / overchoice
        
        This just depends on conventions.
        You can have _more_ ASCII keywords to choose from. If we keep a small, fixed set, like the one above, this is not an issue.

        > Not serious/professional.

        The icon is metadata, not decoration.
        It improves triage and doesn’t replace clear subjects/bodies.

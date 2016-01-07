## Contributing to The Art of Command Line

This guide is a [collaborative effort](AUTHORS.md), based on the generous work of dozens contributors.

Contributions of all kinds, including corrections, additions, improvements, and translations, are welcome!

We hope you'll join and help, in small ways or large.
Here are few notes before you jump in.

### Style

- Stay close to the existing style of the document when possible.
- Remember to focus on **brevity**, **specificity**, and **utility**.
- Avoid long explanations and instead prefer links to resources.

### Using issues and PRs

- Please **create and comment on issues freely** to discuss. A lot of the difficulty in accepting PRs is around style and format, and whether changes should be made at all, so rationale or explanations for the change are useful.
- Please **review open issues and pull requests** before submitting a new one, to help reduce duplication.
- To the extent possible, **break up changes into multiple PRs** so they can be approved separately. Large contributions are also welcome, but are harder and slower to approve, as they tend to require discussion or rewriting.

## Translations

Maintaining the guide in several languages is a little confusing, so here is the process:

- This original version and content of the guide is maintained in English. It has been translated to several other languages
- Each translation has a maintainer to update the translation as the original evolves and to review others' changes. This doesn't require a lot of time, but review by the maintainer is important to maintain quality.
- See the [AUTHORS.md](AUTHORS.md) file for current maintainers. (This file is generated from the [authors-info.yml](admin/authors-info.yml) file.)

### Changes to translations

- Changes to content should be made to the English version first, and then translated to each other language.
- Changes that improve translations should be made directly on the file for that language. PRs should only modify one language at a time.
- Submit a PR with changes to the file in that language. Each language has a maintainer, who reviews changes in that language. Then the primary maintainer @jlevy merges it in.
- Prefix PRs and issues with language codes if they are for that translation only, e.g. "es: Improve grammar", so maintainers can find them easily.

### Adding translations to new languages

Translations to new languages are always welcome, especially if you can maintain the translation!

- Check existing issues to see if a translation is in progress or stalled. If so, offer to help.
- If it is not in progress, file an issue for your language so people know you are working on it and we can arrange. Confirm you are native level in the language and are willing to maintain the translation, so it's not orphaned.
- To get it started, fork the repo, then submit a PR with the single file README-xx.md added, where xx is the lowercase language code. (Use standard two-letter ISO language codes, i.e. the same as is used by Wikipedia, not the code for a single country.)
- Invite friends to review if possible. If desired, feel free to invite friends to help your original translation by letting them fork your repo, then merging their PRs.
- When done, indicate on the PR that it's ready to be merged into the main repo.

Further questions on process or want to volunteer to help in some other way?
File an issue or e-mail the original author @jlevy.

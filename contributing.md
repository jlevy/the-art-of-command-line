## Contributing to The Art of Command Line

This guide is a [collaborative effort](AUTHORS.md), based on the generous work of many contributors.

## Questions

[![Ask a Question](https://img.shields.io/badge/%3f-Ask%20a%20Question-ff69b4.svg)](https://airtable.com/shrzMhx00YiIVAWJg)

The simplest thing you can do to help is [**submit any questions you might have**](https://airtable.com/shrzMhx00YiIVAWJg).
The more the better. Questions help identify where the guide needs to be improved.


## Contributions

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

The guide is now available in many languages. Here is the process for maintaining translations:

- This original version and content of the guide is maintained in English.
- *Translations follow the content of the original.* Note this means contributors to a translation must be able to read some English, so that translations do not diverge (unless it is only fixing a typo).
- Each translation has a maintainer to update the translation as the original evolves and to review others' changes. This doesn't require a lot of time, but review by the maintainer is important to maintain quality.
- See the [AUTHORS.md](AUTHORS.md) file for current maintainers. (This file is generated from the [authors-info.yml](admin/authors-info.yml) file.)

### Changes to translations

- Changes to content should be made to the English version first, and then translated to each other language.
- Changes that improve translations should be made directly on the file for that language. PRs should only modify one language at a time.
- Submit a PR with changes to the file in that language. Each language has a maintainer, who reviews changes in that language. Then the primary maintainer @jlevy merges it in.
- Prefix PRs and issues with language codes if they are for that translation only, e.g. "es: Improve grammar", so maintainers can find them easily.

### Adding a translation to a new language

Translations to new languages are always welcome! Keep in mind a transation must be maintained, so it's needed to have one person maintain each translation.

- Check existing issues to see if a translation is in progress or stalled. If so, offer to help.
- Do you have time to be a maintainer for the new language? Please say so so we know we can count on you in the future.
- If it is not in progress, file an issue for your language so people know you are working on it and we can arrange. Confirm you are native level in the language and are willing to maintain the translation, so it's not orphaned.
- To get it started, fork the repo, then submit a PR with the single file README-xx.md added, where xx is the language code. Use standard [IETF language tags](https://www.w3.org/International/articles/language-tags/), i.e. the same as is used by Wikipedia, *not* the code for a single country. These are usually just the two-letter lowercase code, for example, `fr` for French and `uk` for Ukrainian (not `ua`, which is for the country). For languages that have variations, use the shortest tag, such as `zh-Hant`.
- *Invite friends to review* if possible. Tranlsations are difficult and usually have erros others need to find. If desired, feel free to invite them to help your original translation by letting them fork your repo, then merging their PRs.
- Add links to your translation at the top of every README*.md file. (For consistency, the link should be added in alphabetical order by ISO code, and the anchor text should be in the native language.)
- When done, indicate on the PR that it's ready to be merged into the main repo.

### Further questions

Unsure of the process?
Or do you have skills and inclination to help in a more substantial way?
File an issue or e-mail the original author [@jlevy](https://github.com/jlevy).

# Cuvette adapters

This repository is the registry of community adapters for [Cuvette](https://github.com/elparko/cuvette). An adapter connects Cuvette to one science program. It gives the tools, the decisions that can change a result, the skills and the known-answer tests.

## Install an adapter from the registry

```
cuvette adapter list --registry
cuvette adapter add <name>
```

Cuvette reads `index.json` from this repository. It shows a card with the program, the commands, the shipped code, the network use and the license. It asks before it installs. An adapter from the registry has the trust label Checked.

## Submit an adapter

1. Fork this repository.
2. Add the folder `adapters/<name>/`. The folder name must be the adapter name in `adapter.yaml`.
3. Put a `LICENSE` file in the folder. Any license that the Open Source Initiative (OSI) approves is accepted.
4. Run `cuvette adapter check adapters/<name> --run-tests` on your computer. Fix every error.
5. Open a pull request. Complete the checklist in the template.

The pull request starts two jobs:

1. `checks` runs the lint and the known-answer tests that need no window and no external program. It has no secrets.
2. `claude-review` reads the files as data and runs no code. Claude checks the adapter against the checklist, reads all shipped code for unsafe behavior, and posts one comment with a verdict. It runs for a maintainer, or after a maintainer adds the label `safe-to-review`.

A maintainer reads the code and the review, then decides. The review is advice. It does not replace the maintainer.

After a merge to `main`, the job `build-index` builds `index.json` again. The index lists an adapter only if it passes the lint and all tests that ran.

## More information

- The registry layout and the index format: `docs/adapter-registry.md` in the Cuvette repository.
- The review checklist: `.github/review-prompt.md`.
- The trust labels Reviewed, Checked and Unlisted: https://cuvette.ai/community.html

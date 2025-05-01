# zizmor-bug-726

This repo exists solely to provide a repro case for
[zizmor#726].

[zizmor#726]: https://github.com/woodruffw/zizmor/issues/726


Behavior: `zizmor` should collect all the workflows and actions defined
in this repository, even the ones defined in wonky places:

- `.github/workflows/hello.yml` is a normal workflow defined in
  the normal place.
- `arbitrary/subdir/.github/workflows/hello.yml` is a normal workflow defined
  in a arbitrary subdirectory. GitHub Actions won't find and run this workflow,
  but `zizmor` collects it (on the theory that the user might be generating
  workflows for use elsewhere, and they want us to scan them).
- `arbitrary/subdir/custom-action/action.yml` is a normal action definition
  defined in the normal way.
- `.github/actions/custom-action/action.yml` is a normal action definition,
  within the `.github` directory. GitHub Actions accepts this, so we should too.
- `.github/workflows/custom-action/action.yml` is a normal action definition,
  but defined as a subdirectory of the workflows directory. GitHub Actions
  accepts this, so we should too.
- `.github/workflows/actions/custom-action/action.yml` is a normal action definition,
  but defined within a nested subdirectory of the workflows directory. GitHub Actions
  accepts this, so we should too.

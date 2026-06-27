# Github Custom Actions and Reusable Worklows For Engineers in a Hurry

## How Can I Use/Consume a Github Action or Workflow in a Private Repository

Go to `Settings > Actions > General`, scroll-down and check the box allowing
other repositories (from the same Org) to use/consume the repository as
an Action/Workflow

## Secrets can be Shared with Reusable Workflows But NOT Variables

Github allows us to setup two kind of **Repository Environment Data**:

- Secrets: accessed as `${{ secrets.xyz }}`

This is reserved for Access/Secret Tokens. Once saved it can only be
overwritten or removed (never recovered in plain text)

- Variables: accessed as `${{ vars.xyz }}`

This one holds it's value as plain text. (zero encryption)

You can share all **Secrets** at once with a **Reusable Workflow** using
the: secrets: inherit

```yaml
# Example
jobs:
  call-reusable:
    uses: org/repo/.github/workflows/reusable-workflow.yml@main
    secrets: inherit  # <--
```

## Can All the Variables (vars) also be Shared with Reusable Workflows?

Weirdly enough, No!

Based on the official documentation you would need to pass each Variable
(vars) in a separated argument (defined on the Workflow's yaml file):

```yaml
# Example
jobs:
  call-reusable:
    uses: org/repo/.github/workflows/reusable-workflow.yml@main
    with:
      my-arg-a: ${{ vars.MY_ARG_A }}
      my-arg-b: ${{ vars.MY_ARG_B }}
```

But if you try to pass any values from `vars` it will be passed as blanks.

Why? I do not know.

Based on the scope list of available contexts the `vars` context should be
available: https://docs.github.com/en/actions/reference/workflows-and-actions/contexts

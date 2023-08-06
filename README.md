🌓 GitHub action that checks for changes between nightly CI jobs

### Example Usage

```yml
name: "Nightly Build"

on:
  schedule:
    - cron: "0 2 * * *"

jobs:
  check:
    runs-on: ubuntu-latest
    steps:
      - id: nightly-check
        name: Check for changes since last nightly
        uses: lukecarr/nightly-check@v0.2.0

  nightly:
    runs-on: ubuntu-latest
    needs: check
    if: ${{ needs.check.outputs.changes == 'false' }}
    steps:        
      # ... your steps here
```

In the above example, we declare the `check` job which runs this action. The `nightly` job will then subsequently run **if** no changes have been made to the repository in the past 24 hours.

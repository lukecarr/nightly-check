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
    outputs:
      changes: ${{ steps.nightly-check.outputs.changes }}
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

### Custom duration

If you want to look for changes within a duration different to the default (24 hours), you can configure the `within` input parameter in the action:

```yml
...

jobs:
  check:
    runs-on: ubuntu-latest
    outputs:
      changes: ${{ steps.nightly-check.outputs.changes }}
    steps:
      - id: nightly-check
        name: Check for changes in the last two days
        uses: lukecarr/nightly-check@v0.2.0
        with:
          within: 48 hrs
...
```

### Contributors

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tbody>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://www.carr.sh"><img src="https://avatars.githubusercontent.com/u/24438483?v=4?s=100" width="100px;" alt="Luke Carr"/><br /><sub><b>Luke Carr</b></sub></a><br /><a href="https://github.com/lukecarr/nightly-check/commits?author=lukecarr" title="Code">💻</a> <a href="https://github.com/lukecarr/nightly-check/commits?author=lukecarr" title="Documentation">📖</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://shirinmi1520.github.io/"><img src="https://avatars.githubusercontent.com/u/33322926?v=4?s=100" width="100px;" alt="Y.C.Huang"/><br /><sub><b>Y.C.Huang</b></sub></a><br /><a href="https://github.com/lukecarr/nightly-check/issues?q=author%3AShiriNmi1520" title="Bug reports">🐛</a></td>
    </tr>
  </tbody>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!

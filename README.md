# Potential Duplicates

> A Github Action to search for potential issue duplicates using [Damerau–Levenshtein](https://en.wikipedia.org/wiki/Damerau%E2%80%93Levenshtein_distance) algorithm.

## Usage

Create `.github/workflows/potential-duplicates.yml` in the default branch:

```yaml
name: Potential Duplicates
on:
  issues:
    types: [opened, edited]
jobs:
  run:
    runs-on: ubuntu-latest
    steps:
      - uses: bubkoo/label-commands@v1
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          # Label to set, when potential duplicates are detected.
          label: potential-duplicate
          # Get issues with state to compare. Supported state: 'all', 'closed', 'open'.
          state: all
          # If similarity is higher than this threshold([0,1]), issue will be marked as duplicate.
          threshold: 0.6
          # Reactions to be add to comment when potential duplicates are detected.
          # Available reactions: "-1", "+1", "confused", "laugh", "heart", "hooray", "rocket", "eyes"
          reactions: 'eyes, confused'
          # Comment to post when potential duplicates are detected.
          comment: >
            Potential duplicates:  {{#issues}}
              - [#{{ number }}] {{ title }} ({{ accuracy }}%)
            {{/issues}}
```

## License

The scripts and documentation in this project are released under the [MIT License](LICENSE)

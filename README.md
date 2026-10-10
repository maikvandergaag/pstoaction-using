# pstoaction-using

Example repository that consumes the [`maikvandergaag/pstoaction`](https://github.com/maikvandergaag/pstoaction)
GitHub Action, pinned to a version published through GitHub Releases.

## Usage

The workflow lives in [`.github/workflows/repo-standards.yml`](.github/workflows/repo-standards.yml)
and runs on every push to `main`, on pull requests, and on manual dispatch.

```yaml
- name: Run repo standards check
  uses: maikvandergaag/pstoaction@v1
  with:
    path: .
    required-files: |
      README.md
      LICENSE
      .gitignore
    required-readme-sections: |
      Usage
      License
    forbidden-patterns: |
      *.pfx
      *.pem
    fail-on-error: 'true'
    job-summary: 'true'
    report-path: repo-standards.json
```

### Versioning

`@v1` resolves to the moving major tag that the `pstoaction` repository publishes with each
GitHub Release. To pin to an exact release, use the full tag (for example `@v1.0.0`), or pin
to the commit SHA of that release for immutability:

```yaml
uses: maikvandergaag/pstoaction@<commit-sha> # v1.0.0
```

### Outputs

| Output | Description |
| --- | --- |
| `result` | `passed` or `failed` |
| `checks-total` | Number of checks that ran |
| `checks-passed` | Number of checks that passed |
| `checks-failed` | Number of checks that failed |
| `report-json` | Full result as JSON |
| `report-path` | Path of the JSON report |

The JSON report is uploaded as the `repo-standards-report` workflow artifact.

## License

Licensed under the [MIT License](LICENSE).

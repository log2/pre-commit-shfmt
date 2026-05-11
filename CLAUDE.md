# shfmt-common — development guide

## Purpose

Pre-commit hook that runs `shfmt` on shell scripts. Thin wrapper: no custom logic, no argument translation — consumers pass native shfmt flags directly.

## How it works

```yaml
- id: shfmt
  name: shfmt
  language: system       # uses shfmt from PATH (e.g. via asdf)
  entry: shfmt -w        # -w: rewrite in place
  types: [shell]         # pre-commit's identify library detects shell files
```

`types: [shell]` catches `.sh`, `.bash`, `.bats`, `.envrc`, and no-extension scripts with a shell shebang — all detected by pre-commit's `identify` library.

## Requirements

`shfmt` must be on PATH. Recommended: install via asdf:
```bash
asdf plugin add shfmt
asdf install shfmt 3.13.1
```

## Usage in consumers

```yaml
- repo: https://github.com/log2/shfmt-common
  rev: v0.2.0
  hooks:
    - id: shfmt
      args: [-i, "4", -bn, -ci, -fn]
```

Native shfmt flags: `-i N` (indent), `-bn` (binary ops on new line), `-ci` (case indent), `-s` (simplify), `-fn` (func brace on new line).

## Releasing

```bash
git tag v<x.y.z>
git push origin master --tags
```

## Migration from v0.1.x

v0.1.x used `language: script` with a custom wrapper (`shfmt.sh`) that translated `--indent=4` style args. v0.2.0 uses `language: system` and native shfmt flags:

| v0.1.x arg | v0.2.0 equivalent |
|-----------|------------------|
| `--indent=4` | `-i "4"` |
| `-ci` | `-ci` (unchanged) |
| `-bn` | `-bn` (unchanged) |
| `-fn` | `-fn` (unchanged) |
| `-s` | `-s` (unchanged) |

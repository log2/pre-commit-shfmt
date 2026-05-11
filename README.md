# shfmt-common

[pre-commit](https://pre-commit.com/) hook that runs **[shfmt](https://github.com/mvdan/sh)** on shell scripts.

`shfmt` must be installed and available on `PATH` (e.g. via `asdf`, `brew`, or `apt`).

## Usage

Add to your `.pre-commit-config.yaml`:

```yaml
-   repo: https://github.com/log2/shfmt-common
    rev: v0.2.0
    hooks:
      -   id: shfmt
```

Pass any native `shfmt` flags via `args`:

```yaml
      -   id: shfmt
          args: [-i, "4", -ci, -s]
```

Common flags:

| Flag | Meaning |
|------|---------|
| `-i N` | indent with N spaces (0 = tabs) |
| `-ci` | indent switch cases |
| `-s` | simplify the code |
| `-bn` | binary ops like `&&` and `\|\|` start a new line |
| `-fn` | function opening braces on next line |

See `shfmt --help` for the full list.

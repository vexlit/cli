# VEXLIT

**Stop missing real vulnerabilities.**

Most security scanners use pattern matching.
VEXLIT tracks how data flows through your code.

Find issues across functions, not just lines.

## Try in 10 seconds

```bash
npm install -g @vexlit/cli
vexlit scan .
```

No config required. Works out of the box.

## Example

```js
// Input
const userInput = req.query.q;
const safe = sanitize(userInput);
eval(transform(safe));
```

**Most scanners:** No issues found

**VEXLIT:** Potential injection detected (sanitization bypass) — tracks data flow across `sanitize()` → `transform()` → `eval()`

## What it does

- **Taint Analysis** — Tracks how input moves across functions, not just lines
- **6,200+ Security Rules** — SQL Injection, XSS, Command Injection, Path Traversal, SSRF, and more
- **34 Languages** — JavaScript, TypeScript, Python, Java, Go, C#, PHP, Ruby, Rust, Kotlin, Swift, and more
- **440+ Secret Detection** — API keys, tokens, passwords across all file types
- **Zero Configuration** — No setup, no config files, just scan

## Usage

```bash
# Scan current directory
vexlit scan .

# Output as SARIF (GitHub Security tab)
vexlit scan . --format sarif -o results.sarif

# Scan only changed files (fast CI checks)
vexlit scan --diff

# Fail on high severity (CI/CD gate)
vexlit scan . --fail-on high
```

## CI/CD

Works with any CI/CD platform. Add one command to your pipeline.

### GitHub Actions

```yaml
- name: VEXLIT Security Scan
  run: npx @vexlit/cli scan . --format sarif -o results.sarif
- name: Upload SARIF
  uses: github/codeql-action/upload-sarif@v3
  with:
    sarif_file: results.sarif
```

### Any other CI

```bash
npx @vexlit/cli scan . --fail-on high
```

## Output Formats

| Format | Flag | Use Case |
|--------|------|----------|
| Table | `--format table` | Human-readable terminal output |
| JSON | `--format json` | Programmatic consumption |
| SARIF | `--format sarif` | GitHub Security tab, CI/CD |

## Why I built this

Most tools I tried either:
- cost $25K+/year (enterprise only)
- or missed real-world vulnerabilities (regex-based)

So I built something focused on how data actually flows through code.

## Links

- Website: [vexlit.ai](https://vexlit.ai)
- Documentation: [vexlit.ai/docs](https://vexlit.ai/docs)
- VSCode Extension: [Marketplace](https://marketplace.visualstudio.com/items?itemName=vexlit.vexlit)
- GitHub Action: [vexlit/action](https://github.com/vexlit/action)

## License

MIT

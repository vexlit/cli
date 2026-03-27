# VEXLIT

Most security scanners miss real vulnerabilities.

They catch `eval(userInput)`.
They miss how data flows across functions.

VEXLIT tracks data flow — not just patterns.

## Try in 10 seconds

```bash
npm install -g @vexlit/cli
vexlit scan .
```

No config required. Works out of the box.

## What you'll see

```
🚨 Found 2 potential issues:

[HIGH] Possible injection via user input
app.js:12

[MEDIUM] Unsafe input usage
utils.js:45
```

Tracks how data flows across multiple functions.

## Why this works

Most scanners:
→ pattern matching

VEXLIT:
→ tracks how data flows through your code

That's how it catches real-world issues.

## What it does

- Tracks data flow across functions (taint analysis)
- Finds vulnerabilities most tools miss
- Works instantly (no setup required)

## Example

```js
const userInput = req.query.q;
const safe = sanitize(userInput);
eval(transform(safe));
```

**Most scanners:** No issues

**VEXLIT:** 🚨 Injection detected (sanitization bypass)

## Why I built this

Most tools I tried either missed real issues
or were too complex to actually use.

So I built something simple that works.

## Next

Run with more details:

```bash
vexlit scan . --details
```

## CI/CD

Works with any CI/CD platform. Add one command:

```bash
npx @vexlit/cli scan . --fail-on high
```

### GitHub Actions

```yaml
- name: VEXLIT Security Scan
  run: npx @vexlit/cli scan . --format sarif -o results.sarif
- name: Upload SARIF
  uses: github/codeql-action/upload-sarif@v3
  with:
    sarif_file: results.sarif
```

## Links

- Website: [vexlit.ai](https://vexlit.ai)
- Docs: [vexlit.ai/docs](https://vexlit.ai/docs)

## License

MIT

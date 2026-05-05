# Termux troubleshooting: `command not found` while creating `package.json`

If you paste raw JSON directly into the shell, Termux tries to execute each JSON key as a command (`categories:`, `icon:`, `activationEvents:`, etc.).

That is why you see repeated errors like:
- `categories:: command not found`
- `pricing:: command not found`
- `activationEvents:: command not found`

## Correct way to create `package.json`

Use a heredoc so the JSON is written to a file instead of executed:

```bash
cat > package.json <<'JSON'
{
  "name": "watchdog-ops",
  "displayName": "Watchdog Ops",
  "description": "Tactical dashboard-style VS Code extension UI",
  "version": "0.0.1",
  "engines": {
    "vscode": "^1.90.0"
  },
  "categories": [
    "Other"
  ],
  "activationEvents": [
    "onStartupFinished"
  ],
  "main": "./out/extension.js",
  "scripts": {
    "vscode:prepublish": "npm run compile",
    "compile": "tsc -p ./"
  },
  "devDependencies": {
    "@types/vscode": "^1.90.0",
    "typescript": "^5.6.0"
  },
  "license": "MIT",
  "homepage": "https://example.com",
  "repository": {
    "type": "git",
    "url": "https://example.com/repo.git"
  },
  "bugs": {
    "url": "https://example.com/issues",
    "email": "you@example.com"
  }
}
JSON
```

## `generator.py` not found in Termux

This error means the file does not exist in your current working directory:

```text
python: can't open file '/data/data/com.termux/files/home/generator.py': [Errno 2] No such file or directory
```

Check your directory and file location:

```bash
pwd
rg --files | rg 'generator.py'
```

If nothing is returned, create the script first or move to the directory where it exists.

## Reproducing your target visual style

For a neon tactical look similar to your mockup:

- Use dark cyan/teal background with bright aqua accents.
- Add thin glowing borders, HUD-style labels, and compact uppercase typography.
- Prefer layered charts: area + line + annotation markers.
- Reserve bright lime/yellow only for key signals (target locks, alerts, triggers).

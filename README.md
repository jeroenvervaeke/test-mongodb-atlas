# MongoDB Atlas GitHub Action - Command Injection POC

This repository demonstrates command injection vulnerabilities in `mongodb/atlas-github-action@v0.2.0`.

## ⚠️ Security Warning

This repository contains proof-of-concept workflows that demonstrate security vulnerabilities. Only use this in a test repository you control.

## Vulnerability

The MongoDB Atlas GitHub Action has command injection vulnerabilities due to unquoted inputs in shell commands. See [POC-README.md](POC-README.md) for details.

## POC Workflows

Check the `.github/workflows/` directory for POC workflows that demonstrate the vulnerability.

## Quick Start

1. The workflows are already set up in `.github/workflows/`
2. Go to the Actions tab in GitHub
3. Run any of the POC workflows
4. Check the logs to see the command injection in action

## Documentation

- [POC-README.md](POC-README.md) - Detailed vulnerability explanation
- [SETUP.md](SETUP.md) - Setup instructions

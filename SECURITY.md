# Security Policy

## Supported Versions

| Version | Supported |
|---------|-----------|
| 1.0.x   | Yes       |

## Reporting a Vulnerability

If you discover a security vulnerability, please report it responsibly:

1. **Do not** open a public issue
2. Email can4hou6joeng4@163.com with details
3. Include steps to reproduce if possible
4. You will receive a response within 72 hours

## Scope

This project is a Claude Code skill that generates static HTML/CSS/JS files. The primary security considerations are:

- **Preview server** (`run_preview.py`): Binds to `127.0.0.1` only (localhost), not exposed to network
- **Template injection**: Placeholders use simple string replacement, no eval/exec
- **No user data storage**: The skill does not persist any user data

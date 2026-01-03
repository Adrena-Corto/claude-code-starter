# Claude Code Starter Kit

A starter template for Rust/Solidity projects using [Claude Code](https://claude.ai/code).

## What's Included

- **CLAUDE.md** - Project guidelines that Claude Code reads automatically. Contains coding standards, workflow rules, and language-specific best practices.
- **.claude/settings.local.json** - Pre-approved commands that Claude Code can run without prompting (read-only and safe commands).

## Quick Start

1. Copy these files to your project root:
   ```bash
   cp -r .claude CLAUDE.md /path/to/your/project/
   ```

2. Customize `CLAUDE.md`:
   - Update the "Project Structure" section
   - Update the "Environment Setup" section
   - Add any project-specific guidelines

3. Start using Claude Code in your project

## Pre-Approved Commands

The `.claude/settings.local.json` file allows Claude Code to run these commands without asking:

**General:**
- `echo`, `ls`, `find`, `cat`, `head`, `tail`, `grep`, `wc`, `pwd`, `which`, `whoami`, `awk`, `tokei`, `make`

**Git (read-only):**
- `git log`, `git status`, `git diff`, `git branch`, `git show`

**Rust/Cargo:**
- `cargo build`, `cargo test`, `cargo check`, `cargo fmt`, `cargo clippy`
- `cargo run`, `cargo doc`, `cargo clean`, `cargo search`, `cargo tree`
- `rustc --version`, `rustup --version`

**Foundry (Solidity):**
- `forge build`, `forge test`, `forge clean`, `forge fmt`
- `cast` read-only operations (chain-id, block-number, balance, call, sig, abi-decode/encode)

## Customization

### Adding More Allowed Commands

Edit `.claude/settings.local.json` to add more commands:

```json
{
  "permissions": {
    "allow": [
      "Bash(your-command:*)"
    ]
  }
}
```

### Adding Project-Specific Guidelines

Edit `CLAUDE.md` to add:
- Architecture documentation
- API references
- Domain-specific rules
- Team conventions

## Philosophy

These guidelines enforce:

1. **Lean code** - Delete unused code, avoid over-engineering
2. **Fail fast** - No silent failures, explicit error handling
3. **Quality gates** - Format, lint, and test before committing
4. **Explicit > implicit** - Clear code over clever code

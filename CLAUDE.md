# CLAUDE.md

*Customize this file to fit your project*

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## About This Repository

*Customize this section for your project*

This is a **Claude Code Starter Kit** - a template for Rust/Solidity projects. It includes:
- Pre-configured coding standards and workflow rules
- Pre-approved commands in `.claude/settings.local.json`
- 15 specialized agent definitions in `agents/` for multi-agent workflows

## Commands

### Rust/Cargo
```bash
cargo build           # Compile project
cargo test            # Run all tests
cargo test <name>     # Run specific test
cargo check           # Fast compilation check
cargo fmt             # Format code (run before commit)
cargo clippy          # Lint (run before commit)
cargo run             # Execute binary
cargo doc --open      # Generate and view docs
```

### Solidity/Foundry
```bash
forge build           # Build contracts
forge test            # Run tests
forge test -vvv       # Run tests with verbose output
forge fmt             # Format contracts (run before commit)
forge test --gas-report  # Gas usage report
```

## Code Style

### Keep the Codebase Lean
- **Delete unused code** - No dead code, unused imports, or commented-out code
- **Avoid over-engineering** - Only add what's needed for the current task
- **Prefer editing over creating** - Edit existing files rather than creating new ones

### Fail Fast, Fail Loudly
- **No silent failures** - Prefer explicit errors over fallbacks that mask problems
- **No panics in production** - Use `Result` types in Rust, handle errors gracefully
- **Validate at boundaries** - Check inputs at system boundaries, trust internal code

### Be Explicit
- **Explicit over implicit** - Explicit type conversions, explicit error handling
- **Document the "why"** - Comments should explain *why* when reason isn't obvious

## Workflow

### Before Completing Any Task
1. Run the formatter (`cargo fmt`, `forge fmt`)
2. Run the linter (`cargo clippy`)
3. Run tests - all must pass
4. Check CI if it exists

### Git Hygiene
- Meaningful commit messages explaining what and why
- Never commit secrets, `.env` files, or private keys
- Keep PRs focused and reviewable

## Rust Guidelines

- **No `unwrap()` in library code** - Use `?` operator or explicit error handling
- **No `unwrap()` on user input** - Always validate and handle errors
- **`unwrap()` acceptable in**: tests, examples, or when invariant is proven
- **Prefer `expect("reason")` over `unwrap()`** - If you must panic, explain why
- **Use `thiserror`** for library error types
- **Use `anyhow`** for application error types

```rust
// Good: Propagate errors
fn do_thing() -> Result<Value, Error> {
    let x = fallible_operation()?;
    Ok(x)
}

// Good: Explicit error with context
let value = map.get(&key)
    .ok_or_else(|| anyhow!("key {} not found", key))?;

// Bad: Silent failure
let value = map.get(&key).unwrap_or_default();
```

## Solidity Guidelines

- **Checks-Effects-Interactions pattern** - State changes before external calls
- **Validate all inputs** - Check for zero addresses, valid ranges
- **Emit events for state changes** - Essential for off-chain tracking
- **Use `require` with messages** - Always explain why a requirement exists
- **Minimize on-chain storage** - Storage is expensive

### Security
- Reentrancy guards for external calls
- Use OpenZeppelin's Ownable or AccessControl
- Use Solidity 0.8+ for overflow protection
- Consider commit-reveal for front-running mitigation
- Use TWAPs for oracle manipulation resistance

## Specialized Agents

The `agents/` directory contains 15 agent definitions for complex tasks:

| Agent | Purpose |
|-------|---------|
| `agent-organizer` | Coordinates multi-agent teams |
| `rust-engineer` | Rust implementation and review |
| `solidity-security-auditor` | Smart contract security auditing (opus) |
| `debugging-specialist` | Root cause analysis |
| `performance-engineer` | Profiling and optimization |
| `test-automator` | Test automation and CI/CD |
| `code-simplifier` | Refactoring and simplification (opus) |
| `architect-reviewer` | Architecture analysis |
| `api-designer` | API design and specification |
| `security-auditor` | General security review |
| `error-detective` | Error handling analysis |
| `refactoring-expert` | Code refactoring |
| `search-specialist` | Information retrieval |
| `task-distributor` | Distributed task management |
| `technical-writer` | Documentation |

### Choosing the Right Agent

| If you need... | Use |
|----------------|-----|
| Code cleanup, reduce complexity | `code-simplifier` |
| Structural/architectural refactoring | `refactoring-expert` |
| Find root cause of bugs | `debugging-specialist` |
| Review error handling patterns | `error-detective` |
| General security review | `security-auditor` |
| Smart contract audit | `solidity-security-auditor` |
| Coordinate multiple agents | `agent-organizer` |

### Model Tiers

Most agents use **sonnet** (fast, capable for most tasks). Two agents use **opus** for complex decision-making:
- `code-simplifier` - Complex refactoring decisions
- `solidity-security-auditor` - High-stakes security analysis

### Customizing Agents

Each agent file has a `## Project Context` section. Add your project-specific details there:
- Key services and their responsibilities
- Critical hot paths or performance requirements
- Domain-specific terminology
- Important contracts or modules to be aware of

## Project Structure

*Customize this section for your project:*

```
src/           # Rust source code
contracts/     # Solidity contracts
tests/         # Integration tests
```

## Environment Setup

*Customize this section for your project:*

```bash
# Install Rust
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Install Foundry
curl -L https://foundry.paradigm.xyz | bash
foundryup
```

# AGENTS.md — qbit.rs

A Rust state-vector quantum circuit simulator, verified against Qiskit, used as a Rust performance playground.

## Commands
- Build: `cargo build --all-targets`
- Test: `cargo test`
- Lint: `cargo clippy --all-targets -- -D warnings` and `cargo fmt --check`
- Benches (when present): `cargo bench`

## Layout
- Planned (repo is a scaffold): `src/` simulator (state vector, gates, circuits) · `tests/` integration tests · `tests/fixtures/` reference amplitudes generated with Qiskit (script in `scripts/`)

## Repo-specific rules
- Every gate is checked against a full-matrix (Kronecker) reference for n ≤ 4 and preserves the norm to 1e-12.
- Qubit ordering convention (little-endian like Qiskit) is stated in docs and must not change silently.
- Performance claims need a bench with machine and toolchain recorded.

## How tasks work
- Tasks are GitHub issues in this repo. Each has **Context**, **Acceptance oracles**, **Allowed files** and a **Kind**.
- Start from `gh issue view <n>`. Restate goal, oracles and allowed files, propose a plan, and wait for approval before editing.
- Behave according to **Kind**:
  - **Plumbing (agent)** – implement it, inside Allowed files only.
  - **Core (by hand)** – the human writes the logic. Do not write implementation code for it. Explain, point to references, review diffs, suggest test cases.
  - **Thinking** – produce the requested document; no code.
- Branch: `task/<n>-<short-slug>`. PR description: `Closes #<n>`, then what you verified (command + result) and what you did **not** verify. Tick only the oracles you actually checked.

## Always
- Run the build, tests and linters below before calling anything done.
- Keep the diff minimal and inside Allowed files.
- Cite the source (book/paper, section or equation) in a comment for any algorithm or equation.

## Ask first
- Adding or upgrading dependencies.
- Changing public APIs, feature flags or CI.
- Anything that needs a file outside Allowed files.

## Never
- Weaken, skip or delete a failing test to make CI pass. Edit existing tests only if the task's Allowed files include them.
- Edit files marked `// HAND-CORE` or `# HAND-CORE`.
- Commit secrets. LLM access goes through OpenRouter with the key in an env var (`OPENROUTER_API_KEY`).

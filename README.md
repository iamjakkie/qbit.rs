# qbit.rs

A Rust state-vector quantum circuit simulator. The state is 2^n complex amplitudes. Gates are checked against a full-matrix reference for small registers and against Qiskit. The crate is also a place to practice SIMD, threads, and `unsafe`.

The Cargo package name is `qbitrs`. Complex linear algebra comes from `numb.rs`.

## Goal

- Represent an n-qubit state vector and apply single-qubit and controlled gates.
- Keep every gate unitary: the state norm stays 1 within 1e-12.
- Match a Kronecker reference for n ≤ 4, and match Qiskit amplitudes to about 1e-12.
- Support seeded measurement, QFT, Grover, and a parallel gate kernel with a scaling study against Qiskit Aer.

## Non-goals

- A Python API or a Qiskit-compatible frontend.
- Pulse control, hardware backends, noise models, error correction, or circuit optimization.
- A general linear-algebra crate. That is `numb.rs`.
- An AVIATO flight or networking component. This crate stands alone.

## Status

Library scaffold. `src/lib.rs` is the crate root so the `cargo new --lib` layout exists. CI on `main` runs rustfmt, clippy `-D warnings`, and tests once `src/` is present. Gate kernels, measurement, QFT, Grover, and the parallel kernel come in later tasks.

## Commands

- `cargo build --all-targets`
- `cargo test`
- `cargo clippy --all-targets -- -D warnings`
- `cargo fmt --check`

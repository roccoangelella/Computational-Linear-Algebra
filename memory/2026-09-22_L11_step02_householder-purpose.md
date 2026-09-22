# Lecture 11 — Householder purpose clarification

status: verified
last-updated: 2026-09-22

Studied and clarified:
- A Householder reflector is constructed from the active column vector, not chosen arbitrarily.
- Its QR purpose is to preserve the Euclidean norm while mapping the active column tail to a multiple of the first coordinate vector.
- Therefore the entries below the active diagonal entry become zero in one transformation.
- In informal terms, the column's length is concentrated into one coordinate; more precisely, an orthogonal transformation changes direction/coordinates while preserving the 2-norm.

# Lecture 11 — Householder realistic QR example

status: studied
last-updated: 2026-09-22

Studied example:
- Use Householder reflection on the first column of a 3x2 matrix as the first step of QR factorization.
- Start from the active column x, construct v = x + sign(x_1)||x|| e_1, then H = I - 2 vv^T/(v^T v).
- Left multiplication by H transforms the first column into a multiple of e_1, zeroing all entries below the first diagonal position in one operation.
- The same H must be applied to the entire matrix, not just the selected column, because QR requires a valid row transformation of the whole matrix.
- This is representative of dense least-squares QR, where Householder reflections are preferred because each reflector can annihilate an entire column tail at once.

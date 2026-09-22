# Lecture 11 — Householder full dense QR example

status: studied
last-updated: 2026-09-22
source_paths:
- knowledge/depth/03-qr-construction-details.md

Example studied:
A = [[4,-4,-3],[4,1,-1],[2,3,2]].

First Householder step:
- active first-column vector x=(4,4,2)^T with ||x||_2=6;
- choose target -6 e1 and v=x+6e1=(10,4,2)^T;
- H1 = I - 2 vv^T/(v^T v) = [[-2/3,-2/3,-1/3],[-2/3,11/15,-2/15],[-1/3,-2/15,14/15]];
- applying H1 to the whole matrix gives R1=[[-6,1,2],[0,3,1],[0,4,3]], so both subdiagonal entries in column 1 are eliminated at once.

Second Householder step:
- work only on the active tail (3,4)^T in column 2;
- embedded reflector has active 2x2 block [[-3/5,-4/5],[-4/5,3/5]];
- applying it gives R=[[-6,1,2],[0,-5,-3],[0,0,1]], which is upper triangular.

Purpose reinforced:
- Householder QR progressively converts a dense matrix into upper triangular form.
- One reflector annihilates the whole active subdiagonal tail of a column, unlike Givens rotations which target entries one at a time.

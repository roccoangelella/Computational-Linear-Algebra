# Lecture 11 — Householder factor 2 clarification

status: verified
last-updated: 2026-09-22

Studied and clarified:
- Decompose x into x_perp + x_parallel relative to the Householder normal direction v.
- Reflection across the hyperplane perpendicular to v leaves x_perp unchanged and sends x_parallel to -x_parallel.
- Since x = x_perp + x_parallel, changing +x_parallel into -x_parallel requires subtracting 2 x_parallel: x_perp + x_parallel - 2 x_parallel = x_perp - x_parallel.
- Because x_parallel = proj_v(x) = (vv^T x)/(v^T v), the reflector is Hx = x - 2(vv^T x)/(v^T v), hence H = I - 2 vv^T/(v^T v).

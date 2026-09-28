# Verification map for the Live review

Use internally. Ask **one question at a time** and adapt.

## A - Dense vs sparse viewpoint
Verify: `nnz`, density/sparsity, computational meaning of sparsity, structured vs unstructured pattern.
Transfer: two matrices have the same `nnz`; why can one be much easier to process?

## B - Storage schemes
Verify DOK/LIL/COO construction logic; CSR/CSC arrays and access direction; MSR/MSC diagonal separation; DIAG offsets and unused slots; ELLPACK aligned rectangular storage and padding.
Synthesis: a matrix is assembled entry-by-entry and then used for thousands of matvecs; what format workflow is appropriate and why?

## C - Sparse operations
Verify COO sorted two-pointer addition, equal-coordinate addition/cancellation, linear work in stored entries once sorted; CSR row-wise matvec and its sparse work.
Transfer: why can the mathematical result be storage-independent while runtime and memory are not?

## D - Reorderings
Verify simultaneous row/column permutation, graph interpretation, bandwidth, Cuthill-McKee purpose and traversal logic, dependence on start vertex, reverse variant, independent-set definition and diagonal upper-left block.
Synthesis: Cuthill-McKee and independent-set ordering both permute rows and columns; what different structural target is each trying to create?

## E - SciPy sparse
Verify recognition and use-cases of DOK, LIL, COO, CSR, CSC, BSR, DIA; conceptual role of sparse identity/random/find; row vs column slicing; structural modifications vs repeated arithmetic.
Transfer: if repeated column slices are needed from a fixed matrix currently in CSR, what would you change and why?

## Final synthesis
Seek one coherent pipeline:
**exploit zeros -> choose storage for the phase -> perform sparse kernels without densifying -> reorder when pattern matters -> choose library format according to access/operation**.

A concept is verified only when the learner can explain, distinguish, reconstruct, predict, or justify a choice without being led.

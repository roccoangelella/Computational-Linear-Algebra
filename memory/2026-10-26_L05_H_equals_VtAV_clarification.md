# Lecture 5 clarification: meaning of H=V^T A V

status: concept explained; learner understanding not yet verified
last-updated: 2026-10-26
source_paths: knowledge/modules/06-krylov-arnoldi-fom-gmres.md; uploaded Lecture5-KrylovSpaces.pdf slides 19-21 and 25

Correct a key misconception: h_ij does not compare a candidate to the residual generally. After initial v1=r0/||r0||, h_ij=v_i^T A v_j measures the component of the candidate A v_j along the existing orthonormal basis direction v_i. The coefficients h_ij comprise H_m. The new orthogonal remainder is w_j, and does not appear within H_m until its normalized direction is added at the next stage. Algebra: multiply A V_m to produce columns A v_j, then multiply by V_m^T to compute their dot products with v_i. Thus entry (i,j) of V_m^T A V_m is v_i^T A v_j=h_ij. H_m acts on reduced coefficients y as V_m^T A(V_m y), i.e. the coordinates of the projected result, not generally the full vector A V_m y.

3x3 example A=[[4,0,1],[0,2,-1],[1,-1,3]], V2=(1/sqrt2)*[[1,1],[1,-1],[0,0]]. A V2=(1/sqrt2)*[[4,4],[2,-2],[0,2]]. Multiplying V2^T yields (1/2)*[[6,2],[2,6]]=[[3,1],[1,3]]=H2. Av1=3v1+v2. Av2=v1+3v2 + [0,0,sqrt2], illustrating that H2 stores existing-space components while the remainder is omitted by left V2^T. FOM determines y from H2 y=V2^T r0, then lifts x=x0+V2 y. No full matrix replacement.

Learner comprehension unverified.
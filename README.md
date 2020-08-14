# Colebrook_White_nonlinear_regression
In this study we compare various existing formulas for calculating pipe friction using Colebrook-White (CW) equation. 

These equations are either explicit or implicit. 

CW equation is used to calculate Darcy-Weisbach (DW) friction factor for turbulent pipe flow (Re>4000). 

There are many papers for calculating f with CW formula & they are kind of obsessed with making the calculation faster but to put matters into perspective, we compare calculation time of f from CW equation with the time it takes to solve a Water Distribution Network (WDN). 

Solving WDNs via the gradient descent node method results in formation of a coefficient matrix with the size equal to the number of nodes (junctions) in the network. For each pipe, the elements in matrix corresponding to start & end nodes have a non-zero value, as well as diagonal elements. All other elements are zero. This results in formation of a sparse coefficient matrix. Then the system is converted to Ah=b, wherein A=coefficient matrix, h=unknown heads, and b=right hand side. 

In order to simplify this procedure, the nodes in the sparse matrix must be reordered. There are many ways to do this. This is basically from the graph theory. The Python package NetworkX has a function called reverse_cuthill_mckee_ordering that does this task. After performing this, the system can solved much faster. 

Here we gathered some input files from EPAnet software with 100 to 140000 nodes. We then computed the time it takes to reorder the matrix A & solve the sparse system 10 times. The reason for this is that most water distribution networks converge after 10 iterations. We also calculated the time it takes to calculate f from CW equations with a reasonable accuracy (for example maximum absolute error of 0.01%). We then compared the time for each one of these. Our results show that solving the system usually takes a lot more time than finding the f values. This is basically true for networks with more than 10000 pipes but even for smaller networks, this can be true if fast C routines are called for calculating f. 

References:
A sixteen decimal places' accurate Darcy friction factor database using non-linear Colebrook's equation with a million nodes: A way forward to the soft computing techniques
https://www.sciencedirect.com/science/article/pii/S2352340919310881



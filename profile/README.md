<p align="center"><img src="https://raw.githubusercontent.com/go-sparse/brand/main/social/go-sparse.png" alt="go-sparse" width="720"></p>

# go-sparse

🌐 **[Website](https://go-sparse.github.io)** · 📚 **[Documentation](https://go-sparse.github.io/docs/)**

**Sparse matrices, fill-reducing orderings and iterative solvers in pure Go (CGO=0), on go-ndarray.**

`sparse` provides the COO, CSR, CSC and DOK formats over `float64` and
`complex128`, Matrix Market I/O, the RCM, AMD and COLAMD orderings, and the
iterative solvers CG, GMRES, BiCGSTAB, MINRES, LSQR and LSMR with their
preconditioners, following `scipy.sparse.linalg`. Its tests replay answers
recorded from SciPy 1.18.1 (and SuiteSparse AMD as a binary oracle): iteration
counts of CG, GMRES, MINRES, LSQR and LSMR equal SciPy's. Sparse direct
factorisations, nested dissection, eigensolvers and algebraic multigrid are
not provided yet; the documentation says so. On one core, SpMV, CG and
GMRES(30) on 2-D Laplacians take 0.56 to 0.98 of SciPy's time.

```go
a := gallery.Laplacian2D(100, 100)           // *sparse.CSR[float64]
b := make([]float64, a.Rows)
ic, _ := iter.NewIC0(a)                      // incomplete Cholesky
res, _ := iter.CG(a, b, &iter.Options{RTol: 1e-8, M: ic})
fmt.Println(res.Info, res.Iterations)        // 0 = converged, as in SciPy
```

## Repositories

| Repo | What it is |
|------|------------|
| [**sparse**](https://github.com/go-sparse/sparse) | released [v0.1.0](https://github.com/go-sparse/sparse/releases/tag/v0.1.0): sparse formats and operations, Matrix Market I/O, RCM/AMD/COLAMD orderings, iterative solvers and preconditioners, matrix gallery |
| [**docs**](https://github.com/go-sparse/docs) | the documentation site (Hugo + Hextra), served at [/docs/](https://go-sparse.github.io/docs/) |
| [**go-sparse.github.io**](https://github.com/go-sparse/go-sparse.github.io) | the landing page (Hugo) |
| [**brand**](https://github.com/go-sparse/brand) | logo, icons and social images |

It is part of an ecosystem with
[go-ndarray](https://github.com/go-ndarray/ndarray) (N-dimensional arrays),
[go-numerics](https://github.com/go-numerics) (optimisation, quadrature, ODE
and special functions),
[go-statistics](https://github.com/go-statistics) (distributions and tests),
[go-plot](https://github.com/go-plot/plot) (figures) and
[go-notebook](https://github.com/go-notebook/notebook) (Go notebooks).

---
title: Eigensolver
description: API reference for qiskit.algorithms.Eigensolver
in_page_toc_min_heading_level: 1
python_api_type: class
python_api_name: qiskit.algorithms.Eigensolver
---

# Eigensolver

<span id="qiskit.algorithms.Eigensolver" />

`qiskit.algorithms.Eigensolver`[GitHub](https://github.com/qiskit/qiskit/tree/stable/0.45/qiskit/algorithms/eigen_solvers/eigen_solver.py "view source code")

Bases: [`ABC`](https://docs.python.org/3/library/abc.html#abc.ABC "(in Python v3.12)")

Deprecated: Eigensolver Interface.

The Eigensolver interface has been superseded by the [`qiskit.algorithms.eigensolvers.Eigensolver`](qiskit.algorithms.eigensolvers.Eigensolver "qiskit.algorithms.eigensolvers.Eigensolver") interface. This interface will be deprecated in a future release and subsequently removed after that.

Algorithms that can compute eigenvalues for an operator may implement this interface to allow different algorithms to be used interchangeably.

<Admonition title="Deprecated since version 0.24.0" type="danger">
  The class `qiskit.algorithms.eigen_solvers.eigen_solver.Eigensolver` is deprecated as of qiskit 0.24.0. It will be removed no earlier than 3 months after the release date. Instead, use the interface `qiskit.algorithms.eigensolvers.Eigensolver`. See [https://qisk.it/algo\_migration](https://qisk.it/algo_migration) for a migration guide.
</Admonition>

## Methods

### compute\_eigenvalues

<span id="qiskit.algorithms.Eigensolver.compute_eigenvalues" />

`abstract compute_eigenvalues(operator, aux_operators=None)`

Computes eigenvalues. Operator and aux\_operators can be supplied here and if not None will override any already set into algorithm so it can be reused with different operators. While an operator is required by algorithms, aux\_operators are optional. To ‘remove’ a previous aux\_operators array use an empty list here.

**Parameters**

*   **operator** ([*OperatorBase*](qiskit.opflow.OperatorBase "qiskit.opflow.OperatorBase")) – Qubit operator of the Observable
*   **aux\_operators** (*ListOrDict\[*[*OperatorBase*](qiskit.opflow.OperatorBase "qiskit.opflow.OperatorBase")*] | None*) – Optional list of auxiliary operators to be evaluated with the eigenstate of the minimum eigenvalue main result and their expectation values returned. For instance in chemistry these can be dipole operators, total particle count operators so we can get values for these at the ground state.

**Returns**

EigensolverResult

**Return type**

[EigensolverResult](qiskit.algorithms.EigensolverResult "qiskit.algorithms.EigensolverResult")

### supports\_aux\_operators

<span id="qiskit.algorithms.Eigensolver.supports_aux_operators" />

`classmethod supports_aux_operators()`

Whether computing the expectation value of auxiliary operators is supported.

**Returns**

True if aux\_operator expectations can be evaluated, False otherwise

**Return type**

[bool](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)")

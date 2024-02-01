---
title: QAOA
description: API reference for qiskit.algorithms.minimum_eigensolvers.QAOA
in_page_toc_min_heading_level: 1
python_api_type: class
python_api_name: qiskit.algorithms.minimum_eigensolvers.QAOA
---

# QAOA

<span id="qiskit.algorithms.minimum_eigensolvers.QAOA" />

`qiskit.algorithms.minimum_eigensolvers.QAOA(sampler, optimizer, *, reps=1, initial_state=None, mixer=None, initial_point=None, aggregation=None, callback=None)`[GitHub](https://github.com/qiskit/qiskit/tree/stable/0.45/qiskit/algorithms/minimum_eigensolvers/qaoa.py "view source code")

Bases: [`SamplingVQE`](qiskit.algorithms.minimum_eigensolvers.SamplingVQE "qiskit.algorithms.minimum_eigensolvers.sampling_vqe.SamplingVQE")

The Quantum Approximate Optimization Algorithm (QAOA).

QAOA is a well-known algorithm for finding approximate solutions to combinatorial-optimization problems \[1].

The QAOA implementation directly extends [`SamplingVQE`](qiskit.algorithms.minimum_eigensolvers.SamplingVQE "qiskit.algorithms.minimum_eigensolvers.SamplingVQE") and inherits its optimization structure. However, unlike VQE, which can be configured with arbitrary ansatzes, QAOA uses its own fine-tuned ansatz, which comprises $p$ parameterized global $x$ rotations and $p$ different parameterizations of the problem hamiltonian. QAOA is thus principally configured by the single integer parameter, `reps`, which dictates the depth of the ansatz, and thus affects the approximation quality.

An optional array of $2p$ parameter values, as the [`initial_point`](#qiskit.algorithms.minimum_eigensolvers.QAOA.initial_point "qiskit.algorithms.minimum_eigensolvers.QAOA.initial_point"), may be provided as the starting $\beta$ and $\gamma$ parameters for the QAOA ansatz \[1].

An operator or a parameterized quantum circuit may optionally also be provided as a custom [`mixer`](#qiskit.algorithms.minimum_eigensolvers.QAOA.mixer "qiskit.algorithms.minimum_eigensolvers.QAOA.mixer") Hamiltonian. This allows in the case of quantum annealing \[2] and QAOA \[3], to run constrained optimization problems where the mixer constrains the evolution to a feasible subspace of the full Hilbert space.

The following attributes can be set via the initializer but can also be read and updated once the QAOA object has been constructed.

<span id="qiskit.algorithms.minimum_eigensolvers.QAOA.sampler" />

### sampler

The sampler primitive to sample the circuits.

**Type**

[BaseSampler](qiskit.primitives.BaseSampler "qiskit.primitives.BaseSampler")

<span id="qiskit.algorithms.minimum_eigensolvers.QAOA.optimizer" />

### optimizer

A classical optimizer to find the minimum energy. This can either be a Qiskit [`Optimizer`](qiskit.algorithms.optimizers.Optimizer "qiskit.algorithms.optimizers.Optimizer") or a callable implementing the [`Minimizer`](qiskit.algorithms.optimizers.Minimizer "qiskit.algorithms.optimizers.Minimizer") protocol.

**Type**

[Optimizer](qiskit.algorithms.optimizers.Optimizer "qiskit.algorithms.optimizers.Optimizer") | [Minimizer](qiskit.algorithms.optimizers.Minimizer "qiskit.algorithms.optimizers.Minimizer")

<span id="qiskit.algorithms.minimum_eigensolvers.QAOA.reps" />

### reps

The integer parameter $p$. Has a minimum valid value of 1.

**Type**

[int](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)")

<span id="qiskit.algorithms.minimum_eigensolvers.QAOA.initial_state" />

### initial\_state

An optional initial state to prepend the QAOA circuit with.

<span id="qiskit.algorithms.minimum_eigensolvers.QAOA.mixer" />

### mixer

The mixer Hamiltonian to evolve with or a custom quantum circuit. Allows support of optimizations in constrained subspaces \[2, 3] as well as warm-starting the optimization \[4].

**Type**

[QuantumCircuit](qiskit.circuit.QuantumCircuit "qiskit.circuit.QuantumCircuit") | BaseOperator | [PauliSumOp](qiskit.opflow.primitive_ops.PauliSumOp "qiskit.opflow.primitive_ops.PauliSumOp")

<span id="qiskit.algorithms.minimum_eigensolvers.QAOA.aggregation" />

### aggregation

A float or callable to specify how the objective function evaluated on the basis states should be aggregated. If a float, this specifies the $\alpha \in [0,1]$ parameter for a CVaR expectation value.

**Type**

[float](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)") | Callable\[\[[list](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.12)")\[[float](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)")]], [float](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)")] | None

<span id="qiskit.algorithms.minimum_eigensolvers.QAOA.callback" />

### callback

A callback that can access the intermediate data at each optimization step. These data are: the evaluation count, the optimizer parameters for the ansatz, the evaluated value, the the metadata dictionary, and the best measurement.

**Type**

Callable\[\[[int](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"), np.ndarray, [float](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)"), [dict](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)")\[[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"), Any]], None] | None

**References**

**\[1]: Farhi, E., Goldstone, J., Gutmann, S., “A Quantum Approximate Optimization Algorithm”**

[arXiv:1411.4028](https://arxiv.org/abs/1411.4028)

**\[2]: Hen, I., Spedalieri, F. M., “Quantum Annealing for Constrained Optimization”**

[PhysRevApplied.5.034007](https://doi.org/10.1103/PhysRevApplied.5.034007)

**\[3]: Hadfield, S. et al, “From the Quantum Approximate Optimization Algorithm to a Quantum**

Alternating Operator Ansatz” [arXiv:1709.03489](https://arxiv.org/abs/1709.03489)

**\[4]: Egger, D. J., Marecek, J., Woerner, S., “Warm-starting quantum optimization”**

[arXiv: 2009.10095](https://arxiv.org/abs/2009.10095)

**Parameters**

*   **sampler** ([*BaseSampler*](qiskit.primitives.BaseSampler "qiskit.primitives.BaseSampler")) – The sampler primitive to sample the circuits.
*   **optimizer** ([*Optimizer*](qiskit.algorithms.optimizers.Optimizer "qiskit.algorithms.optimizers.Optimizer")  *|*[*Minimizer*](qiskit.algorithms.optimizers.Minimizer "qiskit.algorithms.optimizers.Minimizer")) – A classical optimizer to find the minimum energy. This can either be a Qiskit [`Optimizer`](qiskit.algorithms.optimizers.Optimizer "qiskit.algorithms.optimizers.Optimizer") or a callable implementing the [`Minimizer`](qiskit.algorithms.optimizers.Minimizer "qiskit.algorithms.optimizers.Minimizer") protocol.
*   **reps** ([*int*](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)")) – The integer parameter $p$. Has a minimum valid value of 1.
*   **initial\_state** ([*QuantumCircuit*](qiskit.circuit.QuantumCircuit "qiskit.circuit.QuantumCircuit") *| None*) – An optional initial state to prepend the QAOA circuit with.
*   **mixer** ([*QuantumCircuit*](qiskit.circuit.QuantumCircuit "qiskit.circuit.QuantumCircuit")  *| BaseOperator |*[*PauliSumOp*](qiskit.opflow.primitive_ops.PauliSumOp "qiskit.opflow.primitive_ops.PauliSumOp")) – The mixer Hamiltonian to evolve with or a custom quantum circuit. Allows support of optimizations in constrained subspaces \[2, 3] as well as warm-starting the optimization \[4].
*   **initial\_point** (*np.ndarray | None*) – An optional initial point (i.e. initial parameter values) for the optimizer. The length of the initial point must match the number of `ansatz` parameters. If `None`, a random point will be generated within certain parameter bounds. `QAOA` will look to the ansatz for these bounds. If the ansatz does not specify bounds, bounds of $-2\pi$, $2\pi$ will be used.
*   **aggregation** ([*float*](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)") *| Callable\[\[*[*list*](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.12)")*\[*[*float*](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)")*]],* [*float*](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)")*] | None*) – A float or callable to specify how the objective function evaluated on the basis states should be aggregated. If a float, this specifies the $\alpha \in [0,1]$ parameter for a CVaR expectation value.
*   **callback** (*Callable\[\[*[*int*](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)")*, np.ndarray,* [*float*](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)")*,* [*dict*](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)")*\[*[*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)")*, Any]], None] | None*) – A callback that can access the intermediate data at each optimization step. These data are: the evaluation count, the optimizer parameters for the ansatz, the evaluated value, the metadata dictionary.

## Attributes

<span id="qiskit.algorithms.minimum_eigensolvers.QAOA.initial_point" />

### initial\_point

Return the initial point.

## Methods

### compute\_minimum\_eigenvalue

<span id="qiskit.algorithms.minimum_eigensolvers.QAOA.compute_minimum_eigenvalue" />

`compute_minimum_eigenvalue(operator, aux_operators=None)`

Compute the minimum eigenvalue of a diagonal operator.

**Parameters**

*   **operator** (*BaseOperator |* [*PauliSumOp*](qiskit.opflow.primitive_ops.PauliSumOp "qiskit.opflow.primitive_ops.PauliSumOp")) – Diagonal qubit operator.
*   **aux\_operators** (*ListOrDict\[BaseOperator |* [*PauliSumOp*](qiskit.opflow.primitive_ops.PauliSumOp "qiskit.opflow.primitive_ops.PauliSumOp")*] | None*) – Optional list of auxiliary operators to be evaluated with the final state.

**Returns**

A [`SamplingMinimumEigensolverResult`](qiskit.algorithms.minimum_eigensolvers.SamplingMinimumEigensolverResult "qiskit.algorithms.minimum_eigensolvers.SamplingMinimumEigensolverResult") containing the optimization result.

**Return type**

[SamplingMinimumEigensolverResult](qiskit.algorithms.minimum_eigensolvers.SamplingMinimumEigensolverResult "qiskit.algorithms.minimum_eigensolvers.SamplingMinimumEigensolverResult")

### supports\_aux\_operators

<span id="qiskit.algorithms.minimum_eigensolvers.QAOA.supports_aux_operators" />

`classmethod supports_aux_operators()`

Whether computing the expectation value of auxiliary operators is supported.

If the minimum eigensolver computes an eigenstate of the main operator then it can compute the expectation value of the aux\_operators for that state. Otherwise they will be ignored.

**Returns**

True if aux\_operator expectations can be evaluated, False otherwise

**Return type**

[bool](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)")
